---
title: Multi-node OpenStack Folsom devstack
author: mestery
layout: post
date: 2013-01-11
url: /multi-node-openstack-folsom-devstack/
tmac_last_id:
  - 544156005152862208
categories:
  - Open Source
  - OpenStack
tags:
  - Open Source
  - OpenStack
---
Recently, I had a need to create a multi-node OpenStack Folsom deployment with Quantum. I needed to test out some deployment scenarios for a customer. To make things even more interesting, I wanted to test it out with the recent VXLAN changes in Open vSwitch which <a title="VXLAN Changes in Open vSwitch" href="http://openvswitch.org/pipermail/git/2012-December/003400.html" target="_blank">went upstream</a>. I thought others may be interested in this as well. I&#8217;m planning to document this for Grizzly as well, but the steps should be mostly the same. Also, I&#8217;ve opened a <a title="VXLAN Support in Open vSwitch Plugin" href="https://blueprints.launchpad.net/quantum/+spec/ovs-vxlan-tunnel" target="_blank">blueprint</a> for the Grizzly release to enable the selection of either GRE or VXLAN tunnels when using the Open vSwitch plugin with Quantum.

## First Steps

To get started, you&#8217;ll need to setup two machines you can use for this. I chose Fedora 17, but Ubuntu 12.04 will work just as nicely. I also chose to install Fedora 17 into virtual machines. And just a quick plug for deployment options here: If you&#8217;re not using something like Cobbler in your lab to automate Linux installs, you really need to. I&#8217;ve got Cobbler setup to automate installs of Ubuntu 12.04, CentOS 6.3, and Fedora 17 in my lab. I can PXE boot VM images or physical machines and with a simple menu selection walk away and come back 30 minutes later to a fully installed system. When you&#8217;re spinning up a large number of devstack installs, this turns out to be very handy. Colin McNamara has a great <a title="Cobbler by Colin McNamara" href="http://www.colinmcnamara.com/setting-up-cobbler-pxe-auto-deployment-for-ubuntu-server-12-04-precise/" target="_blank">blog post</a> to get you started with Cobbler.

Make sure to give each VM 2 virtual interfaces, if you go that route, or that your physical hosts have 2 interfaces. The first one will be used for management traffic, the second one will be used for the external network to access your tenant VMs. I&#8217;ll assume eth0 and eth1 here.

At this point you should have your 2 VMs or physical hosts up and running with Fedora 17 or Ubuntu 12.04.

## Upgrading Open vSwitch on Your Hosts

To enable VXLAN tunnels in Open vSwitch, you need to pull the latest from master, build it, and install it. I&#8217;ll show the instructions for Fedora 17 below, which include building RPMs, but for Ubuntu it should be similar except for the RPM building part. I did this as root, to build the kernel module that seems to work best.

<pre>yum install rpm-build
mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}
git clone git://openvswitch.org/openvswitch
cd openvswitch
./configure --with-linux=/lib/modules/$(uname -r)/build
make dist
cp openvswitch-1.9.90.tar.gz ~/rpmbuild/SOURCES
rpmbuild -bb rhel/openvswitch.spec && rpmbuild -bb -D "kversion $(uname -r)" -D "kflavors default" rhel/openvswitch-kmod-rhel6.spec
rpm -Uhv ~/rpmbuild/RPMS/x86_64/kmod-openvswitch-1.9.90-1.el6.x86_64.rpm ~/rpmbuild/RPMS/x86_64/openvswitch-1.9.90-1.x86_64.rpm</pre>

At this point, reboot your host and you should have the latest Open vSwitch installed. Copy the RPMs from this build host over to your other host, install them the same way, and reboot that host. On each host, the output of &#8220;ovs-vsctl show&#8221; should indicate 1.9.90 as below:

<pre>[root@km-dhcp-64-217 ~]# ovs-vsctl show
55bd458a-291b-4ee6-9ff1-1a3383779e02
    Bridge "br1"
        Port "eth1"
            Interface "eth1"
        Port "br1"
            Interface "br1"
                type: internal
    Bridge "br2"
        Port "vxlan3"
            Interface "vxlan3"
                type: vxlan
                options: {key=flow, remote_ip="192.168.1.13"}
        Port "br2"
            Interface "br2"
                type: internal
    ovs_version: "1.9.90"
[root@km-dhcp-64-217 ~]#</pre>

## devstack

Getting devstack installed and running is pretty easy. Here&#8217;s how to do it. Make sure you do this as a non-root user. Make sure you add passwordless sudo access for this user as well (add &#8220;<username> ALL=(ALL)      NOPASSWD: ALL&#8221; to /etc/sudoers before running devstack).

<pre>git clone git://github.com/openstack-dev/devstack.git
git checkout stable/folsom</pre>

At this point, you should have a Folsom version of devstack setup. You now need to populate your localrc files for both your control node as well as your compute node. See examples below:

### Control node localrc

<pre>#OFFLINE=True
disable_service n-net
enable_service q-svc
enable_service q-agt
enable_service q-dhcp
enable_service q-l3
enable_service quantum
#enable_service ryu

HOST_NAME=$(hostname)
SERVICE_HOST_NAME=${HOST_NAME}
SERVICE_HOST=192.168.64.188

FLOATING_RANGE=192.168.100.0/24
Q_PLUGIN=openvswitch

#LIBVIRT_FIREWALL_DRIVER=nova.virt.firewall.NoopFirewallDriver

Q_HOST=$SERVICE_HOST
Q_USE_NAMESPACE=False
ENABLE_TENANT_TUNNELS=True
MYSQL_HOST=$SERVICE_HOST
RABBIT_HOST=$SERVICE_HOST
GLANCE_HOSTPORT=$SERVICE_HOST:9292
KEYSTONE_AUTH_HOST=$SERVICE_HOST
KEYSTONE_SERVICE_HOST=$SERVICE_HOST

MYSQL_PASSWORD=mysql
RABBIT_PASSWORD=rabbit
SERVICE_TOKEN=service
SERVICE_PASSWORD=admin
ADMIN_PASSWORD=admin

SCHEDULER=nova.scheduler.simple.SimpleScheduler

# compute service
NOVA_BRANCH=stable/folsom

# volume service
CINDER_BRANCH=stable/folsom

# image catalog service
GLANCE_BRANCH=stable/folsom

# unified auth system (manages accounts/tokens)
KEYSTONE_BRANCH=stable/folsom

# quantum service
QUANTUM_BRANCH=stable/folsom

# django powered web control panel for openstack
HORIZON_BRANCH=stable/folsom</pre>

### compute node localrc:

<pre>#OFFLINE=true
disable_all_services
enable_service rabbit n-cpu quantum q-agt

HOST_NAME=$(hostname)
SERVICE_HOST_NAME=km-dhcp-64-188
SERVICE_HOST=192.168.64.188

FLOATING_RANGE=192.168.100.0/24
Q_PLUGIN=openvswitch

#LIBVIRT_FIREWALL_DRIVER=nova.virt.firewall.NoopFirewallDriver

Q_HOST=$SERVICE_HOST
Q_USE_NAMESPACE=False
ENABLE_TENANT_TUNNELS=True
MYSQL_HOST=$SERVICE_HOST
RABBIT_HOST=$SERVICE_HOST
GLANCE_HOSTPORT=$SERVICE_HOST:9292
KEYSTONE_AUTH_HOST=$SERVICE_HOST
KEYSTONE_SERVICE_HOST=$SERVICE_HOST

MYSQL_PASSWORD=mysql
RABBIT_PASSWORD=rabbit
SERVICE_TOKEN=service
SERVICE_PASSWORD=admin
ADMIN_PASSWORD=admin

# compute service
NOVA_BRANCH=stable/folsom

# volume service
CINDER_BRANCH=stable/folsom

# image catalog service
GLANCE_BRANCH=stable/folsom

# unified auth system (manages accounts/tokens)
KEYSTONE_BRANCH=stable/folsom

# quantum service
QUANTUM_BRANCH=stable/folsom

# django powered web control panel for openstack
HORIZON_BRANCH=stable/folsom</pre>

For the compute localrc, make sure you change SERVICE\_HOST to be the IP on your control node you want to use. Also, pick an appropriate floating IP range if you want to use floating IP addresses. On the compute node, make sure to change SERVICE\_HOST and SERVICE\_HOST\_NAME appropriately. Also, once you&#8217;ve run devstack on each host, you can uncomment the &#8220;OFFLINE=True&#8221; to speed it up on subsequent runs.

## Post devstack tasks

I had to do the following tasks on my setup to workaround a few things. Fedora 17 does not come with nodejs installed by default, so Horizon will not work out of the box. To install nodejs, follow these instructions. I performed these as root as well, but sudo would work with the &#8220;make install&#8221; step as well.

<pre>yum install -y gcc-c++
git clone git://github.com/joyent/node.git
cd node
./configure
make && make install</pre>

Next, to work around a Nova metadata issue I was having, I added some IP configuration to eth1 by doing &#8220;sudo ifconfig eth1 up 169.254.169.254&#8243;. I also added eth1 to br-ext on the control node. This is the interface which will be used for external access to your tenant VMs via their floating IP addresses.

You will also need to apply a small patch to Quantum on the control node. This is to make Quantum create VXLAN tunnels instead of GRE tunnels. The patch is below and you should be able to apply it manually quite easily:

<pre>[kmestery@km-dhcp-64-188 quantum]$ git diff quantum/agent/linux/ovs_lib.py

diff --git a/quantum/agent/linux/ovs_lib.py b/quantum/agent/linux/ovs_lib.py
index ec4194d..a0f6bbf 100644
--- a/quantum/agent/linux/ovs_lib.py
+++ b/quantum/agent/linux/ovs_lib.py
@@ -159,7 +159,7 @@ class OVSBridge:

     def add_tunnel_port(self, port_name, remote_ip):
         self.run_vsctl(["add-port", self.br_name, port_name])
- self.set_db_attribute("Interface", port_name, "type", "gre")
+ self.set_db_attribute("Interface", port_name, "type", "vxlan")
         self.set_db_attribute("Interface", port_name, "options:remote_ip",
                               remote_ip)
         self.set_db_attribute("Interface", port_name, "options:in_key", "flow")
[kmestery@km-dhcp-64-188 quantum]$</pre>

## Running devstack

At this point, you should be ready to run devstack. Go ahead and run it on the control node first (cd devstack ; ./stack.sh). Next, run it on the compute host (cd devstack ; ./stack.sh).

To access the consoles of your devstack installs, execute &#8220;screen -r stack&#8221; on each host. This pops you into a screen session with each session handling the output of a particular OpenStack component. To move around in the screen window you can use &#8220;ctrl-a-p&#8221; and &#8220;ctrl-a-n&#8221; to do move to the previous and next windows. &#8220;ctrl-a-ESC&#8221; will freeze the window and let you use vi commands to scroll back. &#8220;ESC&#8221; will unfreeze it.

## Summary: You&#8217;re a Cloud Master Now!

If you&#8217;ve followed this guide, you should have an OpenStack Folsom Cloud running in your lab now with the Open vSwitch Quantum plugin running and VXLAN tunnels between hosts! A followup post will show you how to create multiple tenants and verify Quantum is segregating traffic by utilizing VXLAN tunnels between hosts with a different VNI for each tenant.

Welcome to the world of cloud computing on OpenStack!

<div id="attachment_404" style="width: 202px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/?attachment_id=404" rel="attachment wp-att-404"><img class="size-full wp-image-404" alt="Welcome to Cloud Computing!" src="http://www.siliconloons.com/wp-content/uploads/2013/01/72550243968248291_lnw2Zpyw_b.jpg" width="192" height="178" /></a>
  
  <p class="wp-caption-text">
    Welcome to Cloud Computing
  </p>
</div>

&nbsp;
---
title: Fedora 17 with Open vSwitch
author: mestery
date: 2012-08-07
url: /fedora-17-with-open-vswitch/
socialsharing: true
tmac_last_id:
  - 544156008399273984
categories:
  - Infrastructure
tags:
  - Fedora
  - Linux
  - Networking
  - Open vSwitch
  - Virtualization
---
I&#8217;ve recently decided to move some of the virtual infrastructure in my lab onto Fedora 17. I&#8217;ll be running my VMs on KVM utilizing <a title="libvirt" href="http://libvirt.org/" target="_blank">libvirt</a> to manage the VMs. The great thing about this setup is that in theory, by utilizing libvirt, I can easily move my infrastructure to something like <a title="oVirt" href="http://www.ovirt.org/" target="_blank">oVirt</a> or <a title="OpenStack" href="http://www.openstack.org/" target="_blank">OpenStack</a> in the future. But for now, I plan to simply make use of a combination of virsh and virt-manager. Getting Fedora 17 onto my host was quite easy, I won&#8217;t cover that here. The next thing I wanted to setup was the networking layer.

## The Lay of the Land

Before diving into details of my virtual networking configuration, some background on what the setup in my lab looks like. I have two 3560 switches in my lab, connected via a 4-port port-channel using optical connections. I trunk all my VLANs between the switches and let the 3560s hash based on src-dst-ip. The server I am using for this setup has 6 NICs in it, all Intel Gigabit capable. All 6 NIC ports are connected to a single 3560.

## Virtual Networking on Fedora

I made the choice early on to utilize <a title="Open vSwitch" href="http://www.openvswitch.org/" target="_blank">Open vSwitch</a> for my virtual networking. This has been a part of Fedora since Fedora 16, and the Beefy Miracle release (17) also includes this fine piece of software. I utilize a variety of VLANs in my lab, thus necessitating trunk ports for some configuration. The first thing I decided to do was trunk some of my management VLANs to a bond interface. The VLANs in question were 64, 66, and 67. I utilized 2 physical ports for this bond interface, and setup the port-channel as LACP.

The configuration on the 3560 end looks like this:

![Configuration on the 3560 end of the OVS LACP channel](/Screen-Shot-2012-08-06-at-9.50.43-PM.png)

One the OVS side of things, here is what the configuration looks like in the /etc/sysconfig/networking-scripts/bond0 configuration file. Please note the BOND_IFACES section. This is where you list the physical interfaces you want to be a part of your bond.

![bond0 configuration](/Screen-Shot-2012-08-06-at-9.52.04-PM.png)

The configuration, as shown by ovs-vsctl, looks like this:

![ovs-vsctl output](/Screen-Shot-2012-08-06-at-9.53.02-PM.png)

Once you have the above working, you should now have the physical side of the OVS bridge working. The next step is to configure your management interface. For this, I simply created a mgmt0 interface, added it to the bridge, and setup a configuration file to have it brought up during system boot. You can see in the previous screen shot what this looks like. Below you will find the actual /etc/sysconfig/networking-scripts/ifcfg-mgmt0 file:

![ifcfg-mgmt0 configuration](/Screen-Shot-2012-08-06-at-9.54.05-PM.png)

## One Additional Change

There is one additional change which is needed here. I disabled NetworkManager, and went with the old way of configuring networking. To do this, follow these instructions:

<pre>systemctl stop NetworkManager
systemctl disable NetworkManager</pre>

Before enabling the old network configuration, make a single change to the openvswitch systemctl file. Edit the file located at /usr/lib/systemd/system/openvswitch.service and remove &#8220;network.target&#8221; from the &#8220;After&#8221; section and add a &#8220;Before&#8221; section with &#8220;network.target&#8221;. The end result is something like this:

<pre>After=syslog.target
Before=network.target</pre>

Once you are done with this, make sure to enable both network.service and openvswitch.service:

<pre>systemctl enable network.service
systemctl enable openvswitch.service
systemctl start network.service
systemctl start openvswitch.service</pre>

## Conclusion

The end result of the above is that I now have a LACP port-channel between my 3560 and my OVS bridge on the host. I have trunked some VLANs across this, and setup my management interface on the host as a virtual port on the same OVS bridge. This all works really well, and provides robust networking on your Linux host. Future posts will show how to add virtual machines to this OVS bridge!

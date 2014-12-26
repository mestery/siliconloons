---
title: Getting Started With OpenDaylight and OpenStack
author: mestery
date: 2013-12-16
url: /getting-started-with-opendaylight-and-openstack/
socialsharing: true
tmac_last_id:
  - 544156000492601344
categories:
  - Cloud
  - Open Source
  - OpenFlow
  - OpenStack
tags:
  - IaaS
  - Neutron
  - OpenDaylight
  - OpenStack
  - SDN
---
If you&#8217;re a fan of networking, you are no doubt very excited by all of the recent excitement in the industry as of late. And there is no larger area of innovation in networking at the moment than Open Source networking. Two of the projects at the forefront of Open Source networking innovation are <a title="OpenStack" href="http://openstack.org/" target="_blank">OpenStack</a> <a title="Neutron" href="https://wiki.openstack.org/wiki/Neutron" target="_blank">Neutron</a> and <a title="OpenDaylight" href="http://www.opendaylight.org/" target="_blank">OpenDaylight</a>. OpenStack Neutron is driving an API around networking for Infrastructure as a Service Clouds, and has been very successful at driving mindshare in this area. There are a large number of Plugins and ML2 MechanismDrivers for Neutron in existence already. However, so far, there is no OpenDaylight integration with OpenStack, at least upstream. I am pleased to announce that a team of us are working on making this happen, however. We have a <a title="OpenDaylight Neutron Blueprint" href="https://blueprints.launchpad.net/neutron/+spec/ml2-opendaylight-mechanism-driver" target="_blank">blueprint</a> filed and we are actively working towards the support in OpenDaylight required to support the Neutron APIs. What I&#8217;m going to show you in this blog post is how to take what we currently have for a test run and try it out yourself.

## OpenDaylight Integration with OpenStack: The Details

OpenDaylight is a highly scalable controller written in Java. It is designed from the start to be modular. Perhaps the best way to understand the Modular nature of OpenDaylight is to look at an architecture diagram of it:

<div id="attachment_534" style="width: 970px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2013/12/OpenDaylight_OpenStack_Icehouse_Summit-1.png"><img class="size-full wp-image-534" alt="OpenDaylight Hydrogen Release" src="http://www.siliconloons.com/wp-content/uploads/2013/12/OpenDaylight_OpenStack_Icehouse_Summit-1.png" width="960" height="720" /></a>
  
  <p class="wp-caption-text">
    OpenDaylight Hydrogen Release Architecture Diagram
  </p>
</div>

You can see all the pieces of OpenDaylight, and there are quite a few. Because of the modular nature of OpenDaylight it makes heavy use of the <a title="OSGI Framework" href="http://en.wikipedia.org/wiki/OSGi" target="_blank">OSGI framework</a>. I&#8217;m not going to go into extreme details of how this works, but suffice to say it allows for anyone to write a bundle which can run and interact with other bundles in OpenDaylight.

As part of this, there exists a few bundles which are relevant to the OpenStack integration efforts:

  * <a title="NeutronAPIService" href="https://wiki.opendaylight.org/view/OpenDaylight_Controller:Neutron_Interface" target="_blank">NeutronAPIService</a>
  * <a title="OpenDaylight OVSDB" href="https://wiki.opendaylight.org/view/Project_Proposals:OVSDB-Integration" target="_blank">OVSDB</a>
  * <a title="OpenDaylight OpenFlow" href="https://wiki.opendaylight.org/view/OpenDaylight_OpenFlow_Plugin:Main" target="_blank">OpenFlow</a>

Each of those bundles provides a necessary component in the OpenStack integration. The NeutronAPIService provides an abstraction of the Neutron APIs into OpenDaylight. It caches all of the Neutron objects inside of OpenDaylight providing access to this information to anything in OpenDaylight which requires it. The OVSDB and OpenFlow OSGI bundles in OpenDaylight provide the code which actually programs things on each compute host. They allow for the creation and deletion of tunnel ports, flow programming for ports as they come and go, and bridge creation and deletion on the host.

The main benefit of the above is that each compute host no longer needs an Open vSwitch Agent running on each host. The combination of OpenFlow and OVSDB provide the equivalent functionality as the Open vSwitch Agent.

## OpenDaylight and OpenStack: Getting Started

To test out the latest OpenDaylight Modular Layer2 MechanismDriver, you will need the following:

  * A machine to run the OpenDaylight Controller
  * A machine to run the OpenStack control software
  * At least one machine to run the OpenStack Compute service to run virtual machines

Now, you can combine some of the things above, and you should most certainly run all of the above as virtual machines. I personally run all of the above as virtual machines on VMware Fusion and have one VM in which I run OpenDaylight, one VM in which I run the OpenStack control software, and 3 other VMs in which I run OpenStack compute services. A fairly minimum setup would be 3 VMs, however: One to run the OpenDaylight controller, one to run OpenStack control and compute services, and another one to run only OpenStack compute services.

In either case, your topology will look very similar to the following diagram:

<div id="attachment_528" style="width: 970px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2013/12/OpenStack+OpenDaylight-1.png"><img class="size-full wp-image-528" alt="OpenStack+OpenDaylight" src="http://www.siliconloons.com/wp-content/uploads/2013/12/OpenStack+OpenDaylight-1.png" width="960" height="720" /></a>
  
  <p class="wp-caption-text">
    OpenStack and OpenDaylight Integration
  </p>
</div>

## OpenDaylight and OpenStack: Building and Installing OpenDaylight

Lets get started with the actual configuration of the system now. The first piece is your OpenDaylight VM. To build and install this, follow the steps below. I should note a much larger view of building the controller is on the wiki page <a title="Building the OpenDaylight Controller" href="https://wiki.opendaylight.org/view/OpenDaylight_Controller:Pulling,_Hacking,_and_Pushing_the_Code_from_the_CLI" target="_blank">here</a>, the instructions below are mostly meant to get you going very fast without having to read that wiki page in detail.

<pre>mkdir ~/odl
cd odl
git clone https://git.opendaylight.org/gerrit/p/controller.git
cd opendaylight/distribution/opendaylight/
mvn clean install
cd ~/odl
git clone https://git.opendaylight.org/gerrit/p/ovsdb.git
cd ovsdb</pre>

At this point, you can cut and paste the script below as &#8220;build_ovsdb.sh&#8221; and use that to build OVSDB and copy the bundles over to the controller:

<pre>#!/bin/sh
git pull
cd neutron
echo "Refreshing ovsdb/neutron.."
pwd
mvn clean install
cd ../northbound/ovsdb/
echo "Refreshing northbound/ovsdb.. "
pwd
mvn clean install
cd ../../ovsdb
echo "Refreshing ovsdb/ovsdb.."
pwd
mvn clean install
cd ..
cp ~/odl/ovsdb/neutron/target/ovsdb.neutron-0.5.0-SNAPSHOT.jar ~/odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage/opendaylight/plugins/
cp ~/odl/ovsdb/northbound/ovsdb/target/ovsdb.northbound-0.5.0-SNAPSHOT.jar ~/odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage/opendaylight/plugins/
cp ~/odl/ovsdb/ovsdb/target/ovsdb-0.5.0-SNAPSHOT.jar ~/odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage/opendaylight/plugins/
echo "done!"</pre>

Once you&#8217;ve created the script, simply make sure it has execute permissions (chmod +x build_ovsdb.sh) and run it and you will have the OVSDB bundles created and installed into the plugins directory. To verify they are there, look in the following location:

  * odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage/opendaylight/plugins

The next step is to modify the &#8220;of.address&#8221; variable in the &#8220;configuration/config.ini&#8221; file. This file is relative to the odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage directiory. Fire up vi and add the management IP address for your ODL instance as the value for of.address.

Now it&#8217;s time to fire up your controller! To do that, execute the following:

<pre>cd ~/odl/controller/opendaylight/distribution/opendaylight/target/distribution.opendaylight-osgipackage/opendaylight
./run.sh</pre>

Once the controller is running, you will want to disable the SimpleForwarding Application, so do the following:

  * In the OSGI console, run &#8220;lb | grep simple&#8221; to find the bundle ID of the simpleforwarding application.
  * Run &#8220;stop <bundle ID>&#8221; to disable simpleforwarding.
  * Run &#8220;lb | grep simple&#8221; to verify it is in the &#8220;Resolved&#8221; state.

The entire thing looks like below:

<pre>osgi&gt; lb | grep simple
 132|Active | 4|samples.simpleforwarding (0.4.1.SNAPSHOT)
 true
 osgi&gt; stop 132
 osgi&gt; lb | grep simple
 132|Resolved | 4|samples.simpleforwarding (0.4.1.SNAPSHOT)
 true
 osgi&gt;</pre>

## OpenStack and OpenDaylight: Readying the devstack nodes

At this point, you have an OpenDaylight controller running. Now it&#8217;s time to fire up your devstack nodes. You will need at least two virtual machines ready for this. They can run anything which devstack supports. I am ardent user of Fedora Linux, so that&#8217;s what I use, but Ubuntu works fine as well. Note if you&#8217;re using Ubuntu 12.04 LTS, that particular variant of Ubuntu is using OVS 1.4, which is quite a bit old. Fedora 19 uses a much newer version of OVS.

One thing to note is that you should make sure you have passwordless &#8220;sudo&#8221; access setup for the account you&#8217;re running devstack as.

So, the next thing to do on each node is to checkout devstack:

<pre>cd ~/
git clone git://github.com/openstack-dev/devstack.git
cd devstack
git remote add opendaylight https://github.com/CiscoSystems/devstack.git
git fetch opendaylight
git checkout opendaylight</pre>

Run the above on each devstack node. It will checkout the customer OpenDaylight devstack branch. Now to configure your local.conf files.

On the control node, your local.conf will look like the below:

<pre>[[local|localrc]]
LOGFILE=stack.sh.log
#SCREEN_LOGDIR=/opt/stack/data/log
#LOG_COLOR=False
#OFFLINE=True
RECLONE=yes

# Only uncomment the below two lines if you are running on Fedora
disable_service rabbit
enable_service qpid
disable_service n-cpu
enable_service n-cond
disable_service n-net
enable_service q-svc
enable_service q-dhcp
enable_service q-l3
enable_service q-meta
enable_service quantum
enable_service tempest

Q_HOST=$SERVICE_HOST
HOST_IP=192.168.64.193

Q_PLUGIN=ml2
Q_ML2_PLUGIN_MECHANISM_DRIVERS=opendaylight,logger
ENABLE_TENANT_TUNNELS=True
NEUTRON_REPO=https://github.com/CiscoSystems/neutron.git
NEUTRON_BRANCH=odl_ml2

VNCSERVER_PROXYCLIENT_ADDRESS=192.168.64.193
VNCSERVER_LISTEN=0.0.0.0

HOST_NAME=km-dhcp-64-193.kmestery.cisco.com
SERVICE_HOST_NAME=${HOST_NAME}
SERVICE_HOST=192.168.64.193

FLOATING_RANGE=192.168.210.0/24
PUBLIC_NETWORK_GATEWAY=192.168.75.254
MYSQL_HOST=$SERVICE_HOST
RABBIT_HOST=$SERVICE_HOST
GLANCE_HOSTPORT=$SERVICE_HOST:9292
KEYSTONE_AUTH_HOST=$SERVICE_HOST
KEYSTONE_SERVICE_HOST=$SERVICE_HOST

MYSQL_PASSWORD=mysql
RABBIT_PASSWORD=rabbit
QPID_PASSWORD=rabbit
SERVICE_TOKEN=service
SERVICE_PASSWORD=admin
ADMIN_PASSWORD=admin

[[post-config|/etc/neutron/plugins/ml2/ml2_conf.ini]]
[agent]
minimize_polling=True

[ml2_odl]
url=http://192.168.64.131:8080/controller/nb/v2/neutron
username=admin
password=admin</pre>

You should note in the above you will want to change the following:

  * HOST_IP: This is the management IP of the control host itself.
  *  VNCSERVER\_PROXYCLIENT\_ADDRESS: The management IP address of the control node itself.
  * HOST_NAME: The host name of the control node.
  * SERVICE_HOST: The management IP of the control node.
  * The &#8220;url&#8221; parameter in the ml2_odl section near the bottom: Make sure the url and credentials match your OpenDaylight configuration. If you didn&#8217;t change the default username password for ODL, you can leave those bits alone.

Once you have that done, the next step is to setup your local.conf for the compute nodes:

<pre>[[local|localrc]]
LOGFILE=stack.sh.log
#LOG_COLOR=False
#SCREEN_LOGDIR=/opt/stack/data/log
#OFFLINE=true
RECLONE=yes

disable_all_services
enable_service neutron nova n-cpu quantum n-novnc qpid

HOST_NAME=km-dhcp-64-197.kmestery.cisco.com
HOST_IP=192.168.64.197
SERVICE_HOST_NAME=km-dhcp-64-193.kmestery.cisco.com
SERVICE_HOST=192.168.64.193
VNCSERVER_PROXYCLIENT_ADDRESS=192.168.64.197
VNCSERVER_LISTEN=0.0.0.0

FLOATING_RANGE=192.168.210.0/24

NEUTRON_REPO=https://github.com/CiscoSystems/neutron.git
NEUTRON_BRANCH=odl_ml2
Q_PLUGIN=ml2
Q_ML2_PLUGIN_MECHANISM_DRIVERS=opendaylight,linuxbridge
ENABLE_TENANT_TUNNELS=True
Q_HOST=$SERVICE_HOST

MYSQL_HOST=$SERVICE_HOST
RABBIT_HOST=$SERVICE_HOST
GLANCE_HOSTPORT=$SERVICE_HOST:9292
KEYSTONE_AUTH_HOST=$SERVICE_HOST
KEYSTONE_SERVICE_HOST=$SERVICE_HOST

MYSQL_PASSWORD=mysql
RABBIT_PASSWORD=rabbit
QPID_PASSWORD=rabbit
SERVICE_TOKEN=service
SERVICE_PASSWORD=admin
ADMIN_PASSWORD=admin

[[post-config|/etc/neutron/plugins/ml2/ml2_conf.ini]]
[agent]
minimize_polling=True

[ml2_odl]
url=http://192.168.64.131:8080/controller/nb/v2/neutron
username=admin
password=admin</pre>

Again, the parts to edit above on the compute nodes are:

  * HOST_NAME: The host name of each compute node.
  * HOST_IP: The management IP address of each host.
  * SERVICE\_HOST\_NAME: The hostname of the control node.
  * SERVICE_HOST: The management IP of the control node.
  * ml2_odl: Modify the IP address there for the ODL controller.

Each local.conf file should be saved in the ~/devstack directory on each control and/or compute host.

Now you should be able to run &#8220;stack.sh&#8221; on all of the nodes (control and each compute) by doing this:

  * cd ~/devstack
  * ./stack.sh

Once that completes, you should have a functioning OpenStack setup with OpenDaylight.

### Possible Issues With devstack on Fedora

One possible issue you may hit if you&#8217;re using a fresh VM on Fedora is mysql errors. You will see keystone errors and mysql access errors in the stack.sh run. To get around this, follow the workaround listed in this post <a title="Mysql Errors with devstack on Fedora" href="http://www.tikalk.com/alm/blog/solution-mysql-error-1045-access-denied-userlocalhost-breaks-openstack" target="_blank">here</a>. It&#8217;s worked for me every time I hit this error running devstack on Fedora. One other issue with Fedora is that the latest devstack fails to kill all the nova processes when you run &#8220;unstack.sh.&#8221; To workaround this, simply run the following after &#8220;unstack.sh&#8221;:

  * killall nova-api nova-cert nova-scheduler nova-consoleauth nova-api nova-conductor

## OpenStack and OpenDaylight: Verifying The Install

At this point, you should have the entire system up and running. To verify this, you can do the following:

  * Point your web browser at the OpenStack Horizon GUI: 
      * http://<control node IP>/auth/login/
      * Login using &#8220;admin/admin&#8221; and you can see you OpenStack install.
  * Point your web browser at the OpenDaylight GUI: 
      * http://<odl IP>:8080/
      * Login using &#8220;admin/admin&#8221;

You can play around in the GUIs, launch VMs, etc. As you launch VMs, you will see ODL create tunnel ports and links between compute hosts, which will become visible with a refresh in the OpenDaylight GUI.

## OpenStack and OpenDaylight: Getting Help

The most appropriate place to get help at this early stage is on #opendaylight-ovsdb on Freenode. A long list of OpenStack Neutron and OpenDaylight developers hang out there and can provide help. Besides myself (IRC nick &#8220;mestery&#8221;), you can also expect to find the following people online:

  * Madhu Venugopal (IRC Nick &#8220;Madhu&#8221;)
  * Brent Salisbury (IRC Nick &#8220;networkstatic&#8221;)
  * Keith Burns (IRC Nick &#8220;alagalah&#8221;)
  * Florian Otel (IRC Nick &#8220;FlorianOtel&#8221;)

You can ping any of us and we should be able to help you debug any issues. Florian in particular has some VM images which may expedite the process above for folks trying this out for the first time. The instructions above were meant to walk through all of the steps necessary to get this up and running from scratch.

## OpenStack and OpenDaylight: What&#8217;s Next

In a future post, I will walk through debugging this setup and using it see flows and how different pieces interact. In particular, I&#8217;ll walk through debugging this system so you understand exactly how things are done when networks, subnets, ports, routers and other OpenStack Neutron API objects are created and how OpenDaylight handles programming them onto each host.

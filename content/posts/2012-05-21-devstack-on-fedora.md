---
title: devstack on Fedora
author: mestery
date: 2012-05-21
url: /devstack-on-fedora/
socialsharing: true
tmac_last_id:
  - 544156011624673280
categories:
  - Cloud
  - Open Source
tags:
  - devstack
  - Fedora
  - OpenStack
---
So, it should come as no surprise that I&#8217;m a big Fedora user. I&#8217;ve been running Fedora since Core 1 came out years ago, and I&#8217;ve always been a happy user. As my world has converged around OpenStack recently, the easiest way to work in this environment is by using devstack. For a long while, devstack only workd with Ubuntu. It now supports Fedora, as well as using Qpid instead of the regular RabbitMq.

Working with devstack on Fedora is the same as using it on Ubuntu, and I can happily report it works great. I&#8217;ve run multiple copies of Nova compute on different machines even, and it all just works. So go forth and deploy devstack on Fedora with confidence!

For reference, here is the Fedora wiki page detailing <a title="devstack on Fedora" href="http://fedoraproject.org/wiki/OpenStack_devstack" target="_blank">devstack on Fedora</a>. Also, my localrc file looks like this, for reference:

MESSAGING_SYSTEM=qpid  
IMAGE\_URLS=&#8221;http://launchpad.net/cirros/trunk/0.3.0/+download/cirros-0.3.0-x86\_64-uec.tar.gz,http://berrange.fedorapeople.org/images/2012-02-29/f16-x86_64-openstack-sda.qcow2&#8243;  
ENABLED_SERVICES=g-api,g-reg,key,n-api,n-cpu,n-net,n-sch,n-vnc,horizon,mysql,qpid,openstackx,quantum,q-svc,q-agt  
Q_PLUGIN=openvswitch  
USERNAME=admin  
RABBIT_PASSWORD=nova  
MYSQL_PASSWORD=password  
SERVICE_TOKEN=password  
SERVICE_PASSWORD=password  
ADMIN_PASSWORD=password  
HOST\_IP\_IFACE=eth0  
PUBLIC_INTERFACE=eth1  
VLAN_INTERFACE=eth1  
FLAT_INTERFACE=eth1

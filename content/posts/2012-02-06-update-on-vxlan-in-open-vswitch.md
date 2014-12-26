---
title: Update on VXLAN in Open vSwitch
author: mestery
date: 2012-02-06
url: /update-on-vxlan-in-open-vswitch/
socialsharing: true
tmac_last_id:
  - 544156013025591296
categories:
  - Cloud
  - Open Source
  - Programming
tags:
  - Open vSwitch
  - OpenStack
  - Quantum
  - VXLAN
---
So, previously on the <a title="Open@Cisco" href="http://blogs.cisco.com/category/openatcisco/" target="_blank">other site</a> I blog for, I mentioned <a title="VXLAN in OpenStack Quantum" href="http://blogs.cisco.com/openatcisco/integrating-vxlan-in-openstack-quantum/" target="_blank">VXLAN in OpenStack Quantum</a>. The reasons for this are dictated in that post. While we can start working on the segment ID and multicast address management in Quantum, getting VXLAN support into Open vSwitch can be done in parallel. That process has seen renewed interest recently (see the thread <a title="VXLAN thread" href="http://openvswitch.org/pipermail/dev/2012-February/014685.html" target="_blank">here</a>), and I am happy to report I have setup a git repository with the patches from last fall merged into the latest master branch versions of Open vSwitch. To get the code, go <a title="ovs-vxlan" href="https://github.com/mestery/ovs-vxlan" target="_blank">here</a>. At this point, you have to manually configure the tunnel endpoints, but passing traffic should work over the VXLAN tunnels.

I hope to work with other Open vSwitch developers in the coming weeks to get a fully realized and deployable version of VXLAN into Open vSwitch. At the same time, work will start on the management hooks into OpenStack Quantum. Stay tuned for the blueprint proposing this for inclusion into OpenStack Quantum soon.

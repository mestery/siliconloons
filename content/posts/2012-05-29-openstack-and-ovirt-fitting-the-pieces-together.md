---
title: 'OpenStack and oVirt: Fitting the Pieces Together'
author: mestery
date: 2012-05-29
url: /openstack-and-ovirt-fitting-the-pieces-together/
socialsharing: true
tmac_last_id:
  - 544156010105950208
categories:
  - Cloud
  - Open Source
tags:
  - Cloud
  - Open Source
  - OpenStack
  - oVirt
  - Quantum
---
Many readers of this blog, as well as my work on the <a title="Open@Cisco" href="http://blogs.cisco.com/category/openatcisco/" target="_blank">Open@Cisco Blog</a>, will be familiar with both <a title="OpenStack" href="http://www.openstack.org/" target="_blank">OpenStack</a> and <a title="oVirt" href="http://www.ovirt.org/" target="_blank">oVirt</a>. I have written many posts on <a title="OpenStack Posts" href="http://www.siliconloons.com/?tag=openstack" target="_blank">OpenStack</a> and <a title="oVirt Posts" href="http://blogs.cisco.com/tag/ovirt/" target="_blank">oVirt</a>, but what I want to do with this post is compare the two. Examining where each project has it&#8217;s roots, as well as it&#8217;s current status and how the two Open Source projects may converge in the future, is a worthy exercise.

## OpenStack

OpenStack comes to us by way of Rackspace Cloud and NASA. It has as it&#8217;s origins a very ambitious goal: Allowing anyone to run a cloud computing infrastructure on whatever hardware you have in your data center. OpenStack has quickly consumed a large amount of industry attention, garnering support from a large swath of datacenter vendors as well as service providers. OpenStack has had many successful <a title="OpenStack Releases" href="http://en.wikipedia.org/wiki/OpenStack#Release_history" target="_blank">releases</a>, and the developers are currently working towards a fall release of the IaaS software called &#8220;Folsom&#8221;.

## oVirt

oVirt came into existence when Red Hat decided to Open Source the final piece of it&#8217;s Qumranet acquisition. Qumranet had built a datacenter virtualization management application using Microsoft&#8217;s .NET framework. Red Hat spent a large amount of time porting this code over to Java. The result is oVirt, which was released to the world at a <a title="oVirt Kickoff Workshop" href="http://blogs.cisco.com/openatcisco/ovirt-kickoff-workshop/" target="_blank">Kickoff Workshop</a> hosted by Cisco, the company I work for. The <a title="oVirt First Release Email" href="http://lists.ovirt.org/pipermail/announce/2012-February/000019.html" target="_blank">first release</a> of oVirt came about on February 9, 2012. The oVirt team is hard at work on the next release at this time.

## OpenStack and oVirt: Apples and Oranges?

From a distance, it&#8217;s easy to look at oVirt and OpenStack and think they may somehow be competing projects, both looking to solve the same problem. But once you dig into them, it becomes clear their short-term goals are very different. OpenStack, by virtue of it&#8217;s IaaS roots, is trying to solve the mulit-tenant datacenter problem. By focusing on massive scale, both in terms of nodes as well as tenants, it wants to let you run an AWS scale IaaS cloud in your own datacenter. oVirt, on the other hand, is focusing on a scale much smaller. It wants to let you manage a pool of resources so you can distribute your virtual workloads across them in an efficient manner. By focusing on a different set of users, the two technologies currently each have an important place in the datacenter. Their intersection may not be obvious currently, but OpenStack Quantum may be the first bridge between the two projects.

## OpenStack Quantum: Bridging the Gap

One area where a bridge appears to be forming between the two technologies is with <a title="Quantum" href="http://wiki.openstack.org/Quantum" target="_blank">Quantum</a>. Quantum is the networking technology, incubating in OpenStack, which will be used to construct rich network topologies for OpenStack clouds. It has broad vendor support, and will allow for networking vendors to plug their technology underneath to implement Quantum&#8217;s network and port constructs. When the Folsom release of OpenStack appears this fall, Quantum should become the default networking option in OpenStack.

In the fall of 2011 during the OpenStack Kickoff Workshop, the subject of Quantum and how it relates to oVirt was approached. I blogged about this <a title="Quantum in the Context of oVirt" href="http://blogs.cisco.com/openatcisco/openstack-quantum-at-the-ovirt-kickoff-workshop/" target="_blank">here</a>, noting at the time:

> Now that the oVirt Kickoff Workshop is over, watching how the networking story with oVirt evolves will be interesting. The success of oVirt will be the result of the community around it, and the ecosystem for third party vendors it creates. With regards to networking in oVirt, the interactions between the Quantum community and the oVirt community have only just begun, and the future looks like a very collaborative affair between the two projects.

Those words ended up being very prescient, as there has been recent work to integrate <a title="Quantum and oVirt" href="http://www.ovirt.org/wiki/Quantum_and_oVirt" target="_blank">Quantum into oVirt</a> as a POC. This work has been done by some engineers at Red Hat, and the interesting thing about the work is how the network is the first technology being abstracted out of both OpenStack and oVirt via Quantum.

## Future Interactions

In a <a title="Open Source Cloud and Virtualization Technologies for VMware Users" href="http://www.siliconloons.com/?p=71" target="_blank">previous post</a>, I had compared oVirt to VMware vSphere, and OpenStack to vCloud Director. Once you make this comparison, it&#8217;s easy to see how you could at some point see OpenStack managing oVirt clusters. OpenStack has various virtualization drivers in Nova to handle interacting with virtualization platforms such as Xen, KVM, and Hyper-V. Adding a new driver to interact with oVirt would allow for an interesting interaction between the two technologies. Allowing OpenStack to schedule tenant workloads across oVirt clusters sounds interesting, and may be worth exploring in the future. Perhaps as the two projects converge in the middle, more interesting ideas will surface around these two vibrant Open Source projects.

## Conclusion

As oVirt nears it&#8217;s second release, and OpenStack roles towards the projects sixth release, understanding where the projects exist today is important in looking at how their paths may cross in the future. OpenStack Quantum is acting as the first bridge between the two projects. But as the worlds of datacenter virtualization come together with IaaS cloud computing, the two projects fates may twist together to provide ultimate value for developers, users, and customers.

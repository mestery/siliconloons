---
title: 'Ryu and OpenStack: Like Peanut Butter and Jelly'
author: mestery
layout: post
date: 2012-11-21
url: /ryu-and-openstack-like-peanut-butter-and-jelly/
tmac_last_id:
  - 544156006067208192
categories:
  - Cloud
  - SDN
tags:
  - Open Source
  - Open vSwitch
  - OpenStack
  - Ryu
---
<div id="attachment_345" style="width: 310px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/11/openstack-logo5.png"><img class="size-medium wp-image-345" title="OpenStack" src="http://www.siliconloons.com/wp-content/uploads/2012/11/openstack-logo5-300x300.png" alt="OpenStack" width="300" height="300" /></a>
  
  <p class="wp-caption-text">
    OpenStack
  </p>
</div>

&nbsp;

Increasingly, I&#8217;ve been spending more and more time playing around with and utilizing <a title="OpenStack" href="http://www.openstack.org/" target="_blank">OpenStack</a>. If you&#8217;re looking for a highly configurable and quickly maturing cloud operating system, you can&#8217;t go wrong with OpenStack. One of the more interesting parts of OpenStack to a networking guy like me is <a title="OpenStack Quantum" href="http://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CE8QFjAA&url=http%3A%2F%2Fwiki.openstack.org%2FQuantum&ei=JjatUNyNKanYigKP2ID4DA&usg=AFQjCNEIL-Lhj6bSWPI25h_u7GLBu3cJ_A&sig2=xa17Len-gDy1Pi0T0ooSOg" target="_blank">Quantum</a>. Quantum allows you to create rich topologies of virtual networks, encompassing as much or as little as you want by utilizing different plugins. The plugin architecture is a nice design point, because it allows open source projects as well as vendors the chance to add value and differentiate themselves at this layer. Rather than boiling things down to a commodity, Quantum provides for extensions so each plugin can expose additional information above and beyond the core API.

<div id="attachment_348" style="width: 277px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/11/ryu_portrait3.gif"><img class="size-medium wp-image-348" title="Ryu: Street Fighter" src="http://www.siliconloons.com/wp-content/uploads/2012/11/ryu_portrait3-267x300.gif" alt="Ryu from Street Fighter" width="267" height="300" /></a>
  
  <p class="wp-caption-text">
    Ryu from Street Figher Fame
  </p>
</div>

<p style="text-align: left;">
  Ryu and OpenStack<a title="Ryu Network Operating System" href="http://osrg.github.com/ryu/" target="_blank">Ryu</a> is a network operating system for Software Defined Networks. (Note: Don&#8217;t confuse Ryu the network operating system with the image above, which is of the character <a title="Ryu from Street Fighter" href="http://en.wikipedia.org/wiki/Ryu_(Street_Fighter)" target="_blank">Ryu</a> from <a title="Street Fighter" href="http://en.wikipedia.org/wiki/Street_Fighter" target="_blank">Street Fighter</a> fame.) Ryu aims to provide a logically centralized control platform for your network, with well defined APIs at the top which make this easy to manage and to build rich applications on top. If this sounds like something you&#8217;ve heard before, perhaps it&#8217;s because it&#8217;s very similar to what <a title="Big Switch Networks" href="http://www.bigswitch.com/" target="_blank">Big Switch Networks</a> is doing with their <a title="Floodlight" href="http://floodlight.openflowhub.org/" target="_blank">Floodlight</a> platform. One of the main differences between Ryu and Floodlight is that Ryu is written in Python, as opposed to Floodlight which is written in Java. Also, Ryu is fully compliant with OpenFlow 1.0, 1.2, and the Nicira extensions in <a title="Open vSwitch" href="http://www.openvswitch.org/" target="_blank">Open vSwitch</a>. Ryy is started and maintained by the <a title="NTT laboratories OSRG group" href="http://www.osrg.net/" target="_blank">NTT laboratories OSRG group</a>. Ryu is licensed under the Apache 2.0 license.
</p>

There is of course a Quantum plugin for Ryu, and it&#8217;s upstream and supports both the recent Folsom release, as well as the upcoming Grizzly release of OpenStack. Instructions for deploying the plugin are available on the Ryu webpage <a title="Ryu and OpenStack: VM Images" href="https://github.com/osrg/ryu/wiki/OpenStack" target="_blank">here</a>. You can quite quickly download a Ryu image and load it on your favorite hypervisor and be up and running in not much time. I&#8217;ve loaded and run these images on VMware ESX, VMware Fusion and VirtualBox. The images are tested on Ubuntu with KVM, but they operate just fine with other systems as well.

## Running the Ryu images on your Mac

As I mentioned above, the Ryu images run just fine out of the box on Ubuntu with KVM. But I wanted to run them on my Macbook Pro. I initially wanted to use VirtualBox, but later wanted to switch them over to VMware Fusion. To start with, I needed to get them on VirtualBox. To get the images running with VirtualBox, I used qemu-img convert to convert the images into a format which VirtualBox would understand. Something like this should work:

<pre>qemu-img convert -O vmdk ryuvm2.qcow2 ryuvm2.vmdk</pre>

With that conversion, I was able to easily boot the VMs in VirtualBox. Running them in Fusion would have been as simple as copying over the converted image and importing it, but I had already configured and had the image running on VirtualBox. I moved the image to Fusion to take advantage of nested virtualization (which VirtualBox <a title="VirtualBox Nested Virtualization" href="https://www.virtualbox.org/ticket/4032" target="_blank">doesn&#8217;t support</a>). So I ended up converting the images one more time before importing the VirtualBox images. I used this command:

<pre>BoxManage clonehd ~/VirtualBox\ VMs/RyuVXLANController/Snapshots/\{e5aa0713-93d1-4a06-b367-c488f29a060e\}.vmdk RyuVXLAN-d1.vmdk --format VMDK</pre>

Once I did that, I now had my configured Ryu images running under VMware Fusion, with full nested virtualization support to run nested VMs at (near) full speed.

## Ryu: Segmentation

The real power with Ryu is it&#8217;s ability to segment traffic amongst tenants by using OpenFlow rules on the hosts. For VM to VM traffic across hosts it uses GRE tunnels by default. So effectively, without burning VLANs, you are now able to create rich network topologies scaling to very high tenant limits. For something like OpenStack, this is very useful, as typically OpenStack deployments have many tenants, and this allows for scaling tenant networks on demand.

## Summary

In summary, Ryu is a great platform for virtual networks when deployed with OpenStack Quantum. Scaling tenant networks utilizing a combination of OpenFlow and GRE tunnels is not only very cool, but very practical. Plus, how cool is it to be able to say you&#8217;re running an Open Source IaaS Cloud Operating System and utilizing an Open Source SDN Operating System for your networking needs? I think that&#8217;s a pretty awesome scenario.

<div id="attachment_362" style="width: 310px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/11/peanut-butter-and-jelly-sandwich_0.jpg"><img class="size-medium wp-image-362" title="peanut-butter-and-jelly-sandwich_0" src="http://www.siliconloons.com/wp-content/uploads/2012/11/peanut-butter-and-jelly-sandwich_0-300x205.jpg" alt="Peanut Butter and Jelly" width="300" height="205" /></a>
  
  <p class="wp-caption-text">
    Ryu and OpenStack: Like Peanut Butter and Jelly
  </p>
</div>

&nbsp;
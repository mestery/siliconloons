---
title: LinuxCon Wrapup
author: mestery
date: 2013-09-24
url: /linuxcon-wrapup/
socialsharing: true
tmac_last_id:
  - 544156001859940353
categories:
  - Open Source
tags:
  - Linux
  - LinuxCon
  - OpenDaylight
  - OpenStack
---
Last week I was in New Orleans for <a title="LinuxCon" href="http://events.linuxfoundation.org/events/linuxcon-north-america" target="_blank">LinuxCon</a>. This was my first LinuxCon event, and it was pretty awesome. The event was co-located with a smattering of other Open Technology events as well:

  * <a title="CloudOpen" href="http://events.linuxfoundation.org/events/cloudopen-north-america" target="_blank">CloudOpen</a>
  * <a title="Linux Plumbers Conference" href="http://www.linuxplumbersconf.org/2013/" target="_blank">Linux Plumbers Conference</a>
  * <a title="Xen Project User Summit" href="http://events.linuxfoundation.org/events/linuxcon-north-america/program/xen-project-user-summit" target="_blank">Xen Project User Summit</a>
  * <a title="OpenDaylight Mini Summit" href="http://events.linuxfoundation.org/events/cloudopen-north-america/program/opendaylight-mini-summit" target="_blank">OpenDaylight Mini Summit</a>
  * Gluster Workshop 2013
  * ENEA North America Hacker Event
  * <a title="UEFI Plugfest" href="http://www.uefi.org/events/" target="_blank">UEFI Plugfest</a>
  * <a title="Linux Wireless Summit" href="http://wireless.kernel.org/en/developers/Summits/New-Orleans-2013" target="_blank">Linux Wireless Summit</a>
  * <a title="Linux Security Summit" href="http://kernsec.org/wiki/index.php/Linux_Security_Summit_2013" target="_blank">Linux Security Summit</a>

As you can see, that&#8217;s a lot of events to pack into a single week. I was focused on participating in the LinuxCon keynotes and sessions for the early part of the week. I also worked the OpenDaylight and OpenStack booths for a while on both Monday and Tuesday. It was great to meet so many people and to have amazing conversations around all of the spectacular Open Source technologies I have the pleasure of being involved with. People were very interested in talking about Open Source SDN technologies and how they relate to cloud environments. I had many great discussions around the integration of OpenDaylight with OpenStack Neutron as well.

<div id="attachment_511" style="width: 1034px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2013/09/ian_kyle.jpg"><img class="size-full wp-image-511" alt="Ian and Kyle with the Linux Penguin" src="http://www.siliconloons.com/wp-content/uploads/2013/09/ian_kyle.jpg" width="1024" height="768" /></a>
  
  <p class="wp-caption-text">
    Ian and Kyle with the Linux Penguin
  </p>
</div>

# Panels and Presentations

Wednesday was the day I was on the OpenDaylight Panel, which opened the OpenDaylight Mini-Summit. I was joined by Chris Wright, Dave Meyer, James Bottomley, and Chiradeep Vittal. The topics during the panel were pretty awesome! The audience had lots of great questions. I find a really enjoy panel discussions because it allows for maximum audience participation, and really delivers the exact topics the audience wants to discuss. A great summary of the panel can be found <a title="OpenDaylight Panel Summary" href="http://www.enterprisenetworkingplanet.com/datacenter/linuxcon-is-the-future-of-opendaylight-about-applications.html" target="_blank">here</a> by the Enterprise Networking Planet site. The key takeaway from me, as captured by the summary, is this:

  * *&#8220;We need to start thinking in terms of applications,&#8221; Mestery said. &#8220;But clearly we have a lot of work to do.&#8221;*

&nbsp;

<div id="attachment_514" style="width: 559px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2013/09/odl_panel.jpg"><img class="size-large wp-image-514" alt="OpenDaylight Panel" src="http://www.siliconloons.com/wp-content/uploads/2013/09/odl_panel-1024x768.jpg" width="549" height="411" /></a>
  
  <p class="wp-caption-text">
    OpenDaylight Panel
  </p>
</div>

I also presented at the Linux Plumbers Conference on the topics of LISP and NSH in Open vSwitch. The <a title="LISP and NSH in OVS" href="http://www.slideshare.net/mestery/lisp-and-nsh-in-open-vswitch" target="_blank">slides for this presentation</a> are now on Slideshare. My co-presenter for this discussion was Vina Ermagan. This was a very technical discussion which took place during the net-virt track of the Plumbers Conference. Overall, the feedback was very well received. And not long afterwards, the work we&#8217;ve been doing on NSH in OVS was <a title="NSH Patches for OVS" href="http://openvswitch.org/pipermail/dev/2013-September/032036.html" target="_blank">posted to the OVS mailing list</a> by Pritesh Kothari, another member of my team at Cisco. We believe the work around NSH and LISP is just another example of open protocols being contributed back into Linux and Open vSwitch.

# Podcasts

While at LinuxCon, I had the please to be on two podcasts with the wonderful hosts of <a title="The CloudCast" href="http://www.thecloudcast.net/" target="_blank">The Cloudcast</a>, <a title="Aaron Delp Twitter" href="http://twitter.com/aarondelp" target="_blank">Aaron Delp</a> and <a title="Brian Gracely" href="http://twitter.com/bgracely" target="_blank">Brian Gracely</a>. Aaron and Brian do a great job with The Cloudcast, and I felt like the two podcasts I was a part of were a great way to spread the word of both OpenStack Neutron and OpenDaylight. The podcasts I was a part of were:

  * <a title="OpenDaylight and SDN Evolution" href="http://www.thecloudcast.net/2013/09/the-cloudcast-105-opendaylight-sdn.html" target="_blank">OpenDaylight and SDN Evolution</a>: This podcast was a great venue for myself, <a title="Chris Wright Twitter" href="https://twitter.com/kernelcdub" target="_blank">Chris Wright</a>, and <a title="Brent Salisbury Twitter" href="https://twitter.com/networkstatic" target="_blank">Brent Salisbury</a> to talk about OpenDaylight for people who may not be familiar with it. We also talked a a lot about how it will likely integrate into OpenStack Neutron. That work is ongoing right now. Below is a video of what this integration will look like:



  * <a title="OpenStack Neutron and SDN" href="http://www.thecloudcast.net/2013/09/the-cloudcast-108-openstack-neutron-and.html" target="_blank">OpenStack Neutron and SDN</a>: In this podcast, the discussion revolved around what to expect out of OpenStack Neutron in the Havana release of OpenStack, along with the future of OpenStack Neutron post Havana. I was joined by <a title="Mark McClain Twitter" href="https://twitter.com/gtwmm" target="_blank">Mark McClain</a>, PTL for OpenStack Neutron, and <a title="Ian Wells Twitter" href="https://twitter.com/lan_wan_ian" target="_blank">Ian Wells</a>, my colleague from Cisco.

<div id="attachment_516" style="width: 1034px" class="wp-caption aligncenter">
  <a href="http://www.siliconloons.com/wp-content/uploads/2013/09/odl_convo.jpg"><img class="size-full wp-image-516" alt="OpenDaylight Roundtable" src="http://www.siliconloons.com/wp-content/uploads/2013/09/odl_convo.jpg" width="1024" height="768" /></a>
  
  <p class="wp-caption-text">
    OpenDaylight Roundtable
  </p>
</div>

# Summary

Overall, LinuxCon was a great event. Spending time with people who you normally interact with on IRC, mailing lists, and conference calls is always a good thing. Hashing out complex technical problems is always somehow easier when it&#8217;s done over beers at the end of a long day. I look forward to attending future LinuxCons!

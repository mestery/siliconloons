---
author: mestery
Description: "OpenSwitch Revisionist History: Redux"
socialsharing: true
url: ""
categories:
  - OpenSwitch
  - Open Networking
  - Open Source
  - Network Operating System
  - networking
  - SDN
  - SONiC
  - OCP
  - Open Networking Linux
tags:
  - OpenSwitch
  - Open Networking
  - Open Source
  - Network Operating System
  - networking
  - SDN
  - SONiC
  - OCP
  - Open Networking Linux
title: "OpenSwitch Revisionist History: Redux"
date: 2020-05-13T08:08:01-05:00
---

It seems we have another curious case of revisionist history around the
[OpenSwitch](https://www.openswitch.net) network operating system, this time in
an [article](https://www.nextplatform.com/2020/05/12/is-microsofts-sonic-winning-the-war-of-the-noses/)
from [The Next Platform](https://www.nextplatform.com/):

> In January 2016, only months before Microsoft dropped the SONiC bomb, Dell
> open sourced its own FTOS OS10 network operating system, which it got by
> virtue of its acquisition of switch maker Force10 Networks in the summer of
> 2011. Dell kept its hand in the OpenSwitch (OPX) project it spawned; it also
> participated in the SONiC community started by Microsoft and was an early
> adopter of Cumulus Linux on its switch gear.

Dell did not, in fact, spawn the OpenSwitch project. I've
[written about this before](https://blog.siliconloons.com/posts/2018-03-09-openswitch-libreswitch/),
so you might want to go and read that post. The 'tl;dr' is that OpenSwitch
was launched in 2015 by HPE, and by 2016 it had left the project. The
original HPE code was forked and in fact is
[still on github](https://github.com/libreswitch) under the LibreSwitch
moniker.

But, back to The Next Platform article. This quote from Drew Schulke, VP of
networking at Dell Technologies, stands out in the article:

> We didn’t drop OpenSwitch like a bad habit, but spun it into the Linux
> Foundation and made it part of the broader Open Networking Linux project. 

Dell did indeed take over the hole that HPE left in the OpenSwitch projet. But
much like HPE before it, Dell has pretty much abandoned OpenSwitch.

It seems to me that indeed Microsoft Sonic is getting the majority of the
mindshare around open network operating systems for switches. But we should not
forget to accurately capture the history of these projects when writing
articles about them.

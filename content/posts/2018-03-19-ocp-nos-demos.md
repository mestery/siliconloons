---
author: mestery
Description: "NOS Demos At OCP"
socialsharing: true
url: ""
categories:
  - open source
  - Network Operating System
  - networking
  - SDN
  - OCP
tags:
  - open source
  - Network Operating System
  - networking
  - SDN
  - OCP
title: "NOS Demos At OCP"
date: 2018-03-19T15:02:45-05:00
---

From [sdxcentral][1]:

> Facebook, Google, and Big Switch Networks at this week’s Open Compute
> Project (OCP) Summit will demonstrate three approaches to network
> operating systems all built with Open Network Linux (ONL) and all
> running on OCP switch hardware.

All built with [ONL][3] is interesting to me. This is making the case
ONL is simply an underlying Linux distribution. Why this wasn't clear to
me before is because of the poor messaging around all of these projects.
You can see from my previous posts [here][4], [here][5] and [here][6]
some of the confusion.

Looking further in the article from [sdxcentral][2]:

> “ONL is increasingly becoming the de facto standard for switch hardware
> platform-level code,” Forster wrote in an email to SDxCentral. “With this
> demo, it is now public that it is getting used in Facebook’s FBOSS and
> Google’s Stratum projects, the largest end-user open source network
> projects in the industry.”

OK, so ONL is really the underlying Linux, that's clear to me now.

> Tomorrow, at the annual OCP Summit in San Jose, California, teams from all
> three companies will demo Google’s network operating system (NOS) supporting
> P4 Runtime, Facebook’s FBOSS-based NOS, and Big Switch’s BGP-based concept
> NOS. All three can perform Layer-3 networking, according to Big Switch.
>
> Specifically, the Google demo shows this with centralized software-defined
> networking (SDN) controllers and P4 programming; the Facebook demo shows
> this with the Thrift protocol; and the Big Switch demo shows this with an
> industry-standard BGP protocol.

There's a lot to unpack here, so lets start with the fact that Google and
Facebook will now be showing off their own control stack on top of ONL. The
lower layer is now officially being commoditized, and the fact they are all
building on top of ONL shows this.

It's also interesting to note here there are 3 different control stacks
which will be shown here: Google will use SDN controllers and P4, Facebook
will use Thrift, and Big Switch shows off BGP. Each has taken a different
approach around control, and this also shows the real value is much higher
up the stack than the commoditized underlying operating system. Also note
Google and Facebook are likely using 100% implementation specific controllers
for their own environments, making them less useful for anyone other than
Google or Facebook. Big Switch's attempt to use BGP may make it more
useful to a broader audience.

The last thing I'll note is that the one absence from this demonstration
is AT&T's dNOS. It's a notable omission, as even SONIC from Microsoft
shows up on the ONL website as using ONL as the underlying operating system.

The [OCP Summit][7] next week will be an interesting event as we look to
see these demonstrations.

[1]: https://www.sdxcentral.com/articles/news/facebook-google-and-big-switch-demo-open-network-hardware/2018/03/
[2]: https://www.sdxcentral.com
[3]: http://www2.opennetlinux.org/
[4]: https://blog.siliconloons.com/posts/2018-03-12-stratum-switch-operating-system/
[5]: https://blog.siliconloons.com/posts/2018-03-14-dnos-and-openswitch/
[6]: https://blog.siliconloons.com/posts/2018-03-15-open-source-nos-response/
[7]: http://www.opencompute.org/ocp-u.s.-summit-2018/

---
author: mestery
Description: "Microsoft SONiC and Barefoot Networks At The OCP Summit"
socialsharing: true
url: ""
categories:
  - Open Source
  - Network Operating System
  - Networking
  - SDN
  - OCP
  - SONiC
  - Open Networking Linux
tags:
  - Open Source
  - Network Operating System
  - Networking
  - SDN
  - OCP
  - SONiC
  - Open Networking Linux
title: "Microsoft SONiC and Barefoot Networks At The OCP Summit"
date: 2018-03-22T13:57:59-05:00
---

From an [article at The Register][1] regarding [Microsoft's SONiC][2]
network operating systems:

> Microsoft coordinated a bunch of announcements at the Open Compute Project
> summit this week, centred around its SONiC open switch software platform.

[SONiC][2], as you may recall, is Microsoft's Debian based network
operating system which it has donated to the Open Compute Project. Worth
noting SONiC has now attracted [Barefoot Networks][3]:

> Barefoot's another fan, folding SONiC into a variety of its Tofino-based
> bare metal switches. The company said SONiC will bring advanced capabilities
> like data plane telemetry.

It looks like Barefoot has contributed support into SAI for their Tofino-based
switching platforms from Wistron and Edgecore. This is an interesting
development, as it helps embolden Barefoot as they look to expand their
Tofino-based platforms, and give's Microsoft's SONiC platform something
interesting to use for network telemetry.

It's worth noting that SONiC is different than [Open Network Linux][4],
which itself is also hosted in the Open Compute Project, and is backed by
operators such as Google and Facebook, and vendors including Big Switch.
The two are different network operating systems, my assumption is OCP is
simply a home for both. Choice is good, until it isn't.

[1]: https://www.theregister.co.uk/2018/03/22/networking_news_roundup/
[2]: https://azure.github.io/SONiC/
[3]: https://barefootnetworks.com
[4]: http://opennetlinux.org

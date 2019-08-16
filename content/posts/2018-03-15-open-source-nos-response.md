---
author: mestery
Description: "Open Source NOS: Response"
socialsharing: true
url: ""
categories:
  - open source
  - Network Operating System
  - networking
  - SDN
tags:
  - open source
  - Network Operating System
  - networking
  - SDN
title: "Open Source NOS: Response"
date: 2018-03-15T07:18:31-05:00
---

My [blog post on dNOS][2] caused some interesting discussions to happen. My
thinking was most people, be they open source people or networking people,
don't care about open source network operating systems. I have my theories
as to why, and this Twitter thread contains my thoughts:

*Edit: Since deleted twitter thread once found here.

Reactions from others were all over the map. [Bill Koss][3] had the first
snarky reply, which also rings true:

{{< tweet 974034817208725504 >}}

[Mike Dvorkin][4]'s reply was also right on the money:

{{< tweet 974069553977114624 >}}

[Pete Lumbis][5] tackled it from an interesting angle, indicating the big
players already have their own, which is true, and that it's a hard problem
to solve:

{{< tweet 974041351816794112 >}}

There are other replies on the thread as well, the discussion will hopefully
continue on. I also received an email from [Bert Vermeulen][1]. Bert had
the pleasure of being involved with [OpenSwitch][6] and [LibreSwitch][7]
from the start. He was one of the very few individual contributors to both
projects. Bert had some of his own thoughts on why these open source network
operating systems never take off.

> What killed OpenSwitch was, obviously, it being overly reliant on HPE,
> which cancelled (the open source side of) the project -- and thus taking
> away all the momentum and 99% of the people, and it duly died.
> Libreswitch was an effort to Continue without HP, but as Diego told you,
> there just wasn't enough interest.
> 
> But you can't blame HPE -- Libreswitch also didn't work, and the newer
> OpenSwitch codebase is just a do-over which will fail, and ONL has never
> taken off, and now Stratum will repeat the mistake, and dNOS etc etc.
> 
> The reason these all fail is because they're corporate-driven projects,
> which inevitably fail to build a community around the project. These
> companies see value in sharing development resources, i.e. people, from
> a financial point of view, but are entirely clueless about what makes
> open source projects work at all.

Bert is right. These projects always come from corporations which have their
own agenda. Open Source becomes a tool, to some extent. The real problem
is that this can work as long as you have a strong leader at the sponsoring
corporation who truly believes in Open Source and can champion it. If that
strong leader loses their resolve or leaves, then all bets are off.

However, another reason these projects fail is around the closed hardware
ecosystem, stemming from the ASICs in many of these switches and routers:

> The reason that all of these open NOS projects are corporate-driven is
> because the network chips are all so damn closed -- that world never
> caught on to the "open" revolution of the 90s -- and the gear itself is
> out of reach for passionate hobbyists to play with.

Bert offered some hope to me, however:

> Where the gear *is* in reach of hobbyists -- SOHO routers -- an open
> source community has indeed formed: OpenWRT, and it's a roaring success.
> The project, for all its warts, now supports broadly every damn thing in
> scope, and a lot (if not most) products in this market ship with a
> vendor-supplied version of OpenWRT. That's the kind of success these
> corporate-driver NOS projects are chasing, but will never reach.

[OpenWRT][8] is an amazing project, and it has done some great things over
the years. I remember first using OpenWRT over 15 years ago, and it is still
going strong! OpenWRT is an example of an open source network operating
system which grew from community roots, and has built a strong contributor
base, and is now used by manufacturers of wired and wireless products. It
gives me hope that perhaps in the future there can be a datacenter network
operating system which can trace it's roots to a strong open source
community.

[1]: https://www.linkedin.com/in/bert-vermeulen-13539b/
[2]: https://blog.siliconloons.com/posts/2018-03-14-dnos-and-openswitch/
[3]: https://twitter.com/WR_Koss
[4]: https://twitter.com/nikrovd
[5]: https://twitter.com/PeteCCDE
[6]: https://www.openswitch.net
[7]: https://github.com/libreswitch
[8]: https://openwrt.org

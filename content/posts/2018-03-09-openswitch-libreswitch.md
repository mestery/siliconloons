---
author: mestery
Description: "LibreSwitch: The OpenSwitch Fork Which Almost Made It"
socialsharing: true
url: ""
categories:
  - Open Source
  - OpenSwitch
  - LibreSwitch
  - Networking
tags:
  - Open Source
  - OpenSwitch
  - LibreSwitch
  - Networking
title: "LibreSwitch: The OpenSwitch Fork Which Almost Made It"
date: 2018-03-09T13:04:21-06:00
---

Some of you may be aware of [OpenSwitch][4], the Linux Foundation's open
network operating system which describes itself as:
```
* Linux-based network operating system (NOS) platform
* Open source, vendor-neutral royalty-free model
* Large ecosystem of industry leader support
* Rapid onboarding of new platforms, protocols and applications
* Viable option for open networking switch disaggregation
```

While I was at HP, I was heavily involved in this project at the time. This
was around 2015. We had big intentions with the project, it was fun to see
something like this happen. Fast forward to the fall of 2016, and as was
[written at the time][5], OpenSwitch moved to a new codebase. But what
happened to the original code that made up OpenSwitch?

It may surprise you to learn that a [fork][3] of that codebase happened,
and the [LibreSwitch][1] project was started. (Note the certificate for
[https://www.libreswitch.org/][2] has expired, so proceed there with
caution.) LibreSwitch is the original code from OpenSwitch, still on
github.

I had a discussion on twitter yesterday around this, where one of the
original OpenSwitch engineers, [Diego Dompe][7], confirmed LibreSwitch
never took off:

{{< tweet 971865036972085248 >}}
{{< tweet 971877926567374849 >}}

The [code][1] is still there in case anyone wants to pick it up, play
with it, and give it a shot. In the meantime, the [new OpenSwitch code][6]
is also on github.

[1]: https://github.com/libreswitch
[2]: https://www.libreswitch.org/
[3]: https://lists.openswitch.net/pipermail/ops-dev/2017-February/014599.html
[4]: https://www.openswitch.net
[5]: https://www.sdxcentral.com/articles/news/openswitch-moves-away-hpe-embracing-dell-snaproute/2016/10/
[6]: https://github.com/open-switch
[7]: https://twitter.com/ddompe?lang=en

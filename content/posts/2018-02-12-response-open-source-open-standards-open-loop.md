---
author: mestery
Description: "Response: Open Standards, Open Source, Open Loop"
socialsharing: true
url: ""
categories:
  - Open Source
  - Networking
tags:
  - Open Source
  - Networking
title: "Response: Open Source Open Standards Open Loop"
date: 2018-02-12T19:35:46Z
---

[Dave Ward][2] recently wrote a [blog post][1] evaluating some thoughts
around Open Standards and Open Source. It's a great read, I encourage
you to spend some time reading it and digesting it. There are many good
points in there, I'll highlight a few below with my own comments around
his ideas here.

> About three years ago, at IETF 91, I gave a presentation on the state
> of SDOs like the IETF and Open Source networking communities and the
> industry trend of innovators (vendors, operators, entrepreneurs,
> developers) regardless of affiliation coming together to form developer
> communities in the open.   At that time, I reflected on whether an SDO
> like the IETF would remain relevant in a rapidly expanding environment
> of Open Source Software (OSS) projects.  I made outrageous claims that
> were proven only with emphatic assertion about the relationship between
> Open Standards and Open Source. Summarized; developers in the open
> communities are setting the pace and trajectory of the industry and not
> the publication of paper standards.  Honestly, it was at the beginning
> of the era. Networking related open source communities had just formed
> and established themselves. The early days of software defined
> networking (SDN) and network function virtualization (NFV) had finally
> moved to post-hype phase and protocol and product work were well
> underway.

Similar to Dave, I also wondered about the relationship between standards
organizations and open source. Four years ago, I thought that in the
future open source organizations would eclipse SDOs. This obviously has
not happened, and in fact SDOs are moving in the direction of OSS
projects.

> My real bottom line here is that innovators can’t go faster than their
> customers and customers can’t go faster than their own understanding of
> the technology and integration, deployment and operational
> considerations. And, we need to reduce the fracturing of the industry
> because, in this interim period, a technology landscape has evolved
> that is littered with “Stacks”, “Controllers”, and “Virtual Fubars”.

This point really hit home with me. The OSS landscape is littered with
many projects, many of which were developed in a vacuum, and many of
which require integration with other projects to produce a solution
for a customer. OSS projects are now realizing this, and you're seeing
them try to coalesce things together, such as with new overarching
projects such as the [LF Networking Fund][3]. Trying to produce
harmonized solutions from all the piece is the future of meaningful
OSS work.

> On the “foundation” side it has turned into a situation where every
> new community forming felt they needed their own foundation,
> misunderstanding the function of a board and application of money
> raised. Many new communities we formed were cost-free, no (mega)
> boards and some had 503c’s (foundations) some focused not only on
> code, but on code guarantees of performance and scale (spending
> foundation dues on infrastructure and test platforms). Back in 2012
> when I started in OpenSource developer community building and
> focusing on contribution of code; I was completely and utterly
> green. Several years later, I can claim a lot of scars and experience,
> met and learned from a lot of very smart people; and that code is the
> answer and that a healthy community is built and not launched. The
> exercise reified the earlier understanding from many years as a
> developer and standards person, the best standards come from running
> code.

Foundation overload. I think many of us in open source have felt this
for the past few years. Every piece of code doesn't need a board, a
TSC, and a heavyweight process. Perhaps the heavyweight process does
make sense when integrating all the pieces, though.

> In looking at our current state, I am convinced that APIs, platforms
> and frameworks WILL be the future standards front for software driven
> network architectures.  The same standardization reasoning applies to
> these higher-level concepts as did to our original protocol
> specification efforts – consistent system design, interoperability, and
> choice.  And, the “Collaborative Loop” I described at IETF 91 (Figure
> 1) requires (minimally) tooling built to have standards and dependencies
> in a RCS that is open and accepts contributions.

This is 100% correct. The networking industry, both in terms of open
source as well as proprietary, is moving in this direction at a rapid
pace.

> The “normative reference” discussion (in sum, a standard needs to be able
> to refer to an open source development effort) remains unresolved at this
> point, primarily because of fundamental differences in orientation of the
> parties around documentation.  For an OSS community, code is quite often
> the documentation.  The quality and type of what an SDO may consider
> documentation is community dependent.  It is also unclear how projects
> will be picked as being viable for a reference in a standard, how to
> measure health and longevity of prospective communities and what aspects
> of the projects are to be referenced (entire project, subproject, schemas,
> specific implementations, code versions, libraries, …, ???).

This alludes to how do OSS and SDO organizations work together. Over the
past four years, I've seen this attempted a few times. It's clearly where
things needs to land, but how best to get there without crushing the things
which make OSS and SDO organizations independently successful and
meaningful? It's a difficult question I should answer in a future blog post.

> At the same time, we need to remain balanced and accept our roles as
> technologists – that what we are creating has a very specific role in a
> larger ecosystem.  What gets me excited as an engineer is getting my
> technology out there and being used in multiple new and different ways.

This is what makes all engineers I know get up and work hard everyday.
Ensuring this level of excitement is what moves things forward by leaps
and bounds, and pushes the entire industry forward to the future.

[1]: https://blogs.cisco.com/sp/three-years-on-open-standards-open-source-open-loop
[2]: https://twitter.com/drrcranium?lang=en
[3]: https://www.linuxfoundation.org/projects/networking/

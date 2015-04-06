+++
Description = "Neutron Kilo Retrospective and a Look Toward Liberty"
author = "mestery"
categories = ["OpenStack", "Neutron", "Development", "Open Source"]
date = "2015-04-06T08:56:06-05:00"
socialsharing = true
tags = ["OpenStack", "Neutron", "Development", "Open Source"]
title = "Neutron Kilo Retrospective and a Look Toward Liberty"
url = ""

+++

As we near the end of the [OpenStack Kilo release][1], I wanted to take a moment to write about a few things around Neutron's
Kilo release. In a lot of ways, Kilo was all about continuing to scale the development model for Neutron going forward. We
did accomplish some feature work, as well as a lot of technical debt repayment. But the main focus was on how to continue
evolving Neutron the *platform*. Before I get into that, lets take a peek at where we landed for Kilo.

kilo-1 Milestone
----------------

The [kilo-1][2] milestone was very early in the Kilo release, December 18 to be exact. This was a week after the Neutron
mid-cycle meeting in Lehi, Utah. The first milestone of each release always come very fast, and this one was no different.
The team completed 3 BPs and 164 bugs. The BP count was low, but the [services split][6] was a lot of work and took the focus
of a lot of the team. Ideally we would have closed out more BPs, but the low BP count seems indicative of the majority of
the first milestones of a release.

kilo-2 Milestone
----------------

The [kilo-2][3] milestone saw the team complete 8 BPs and address 140 bugs. We saw increased momentum for this release, but
we didn't quite close out as many BPs as I had hoped. Focusing a bit more on reviewing and closing out specs in the second
milestone as well as the first is something I'd like the review team to work on during Liberty.

kilo-3 Milestone
----------------

The [kilo-3][4] milestone saw a razor-sharp focus on BPs, as we closed out 21 BPs and 139 bugs. This milestone is where the
rubber starts to meet the road, so to speak. The review team became extra focused on BPs at this point. We pushed as many
BPs as we could over the finish line, but still ended up with more than I wanted with Feature Freeze Exceptions (FFEs) for
the RC release.

kilo-rc1 Milestone
----------------

Our first (and hopefully only) [RC candidate][5] saw us close out 12 BPs and, at the time of writing this, somewhere around 65
bugs. We pushed a lot of specs into the RC, which wasn't necessarily a good thing. We also didn't complete the review and
merge of pluggable IPAM, which would have been great to have in Kilo. More on that later.

Kilo Retrospective
------------------

I'm proud of the work all the Neutron contributors accomplished during the Kilo release. We have done an amazing job continuing
to grow the platform, address bugs, and increase stability. Even better, by dissecting Neutron a bit by [splitting out the
services projects into their own repositories and decomposing plugins][7], we've built the foundation for a scalable development
model for future releases.

On To Liberty
=============

As we look forward to Liberty, the next phase of Neutron evolution is before us. We're already busy planning sessions for the
Design Summit in Vancouver, even as we put the final wraps on the Kilo release. Contributors are busy filing specs for the
upcoming Liberty release. In many ways, time flows on and is indexed by milestones and cutoffs from the OpenStack calendar.

Review and Merge Velocity
-------------------------

We did a great job merging 44 BPs during Kilo. Realistically, we can likely merge around 50 BPs each cycle. What I'm going to
work on during Liberty is better tracking BPs and specs to milestones and ensuring they land in an orderly manner. I think if
we had focused a bit more during the early milestones the later milestones would have gone a bit smoother. I'm going to try
and really look at the work we're doing in Liberty and focusing on matching things up to appropriate milestones, and then
working harder to ensure the review team focuses their efforts on things for each cycle. Once Liberty lands next fall it will
be good to do a post-mortem again and see how the review team did during the cycle vs. Kilo, and even Juno.

Neutron As a Platform
---------------------

One of the bit items on the agenda for the team is to look at spinning out the reference implementation of ML2+\[OVS,LB\] agents
into a separate repository. Why would we consider doing this? The reason is simple: We want Neutron to be a scalable, robust
networking API and DB platform. Over the past few years, we've conflated that with also implementing an Open Source SDN solution.
We've reached the point where there exist enough Open Source SDN backends that continuing to implement one in Neutron based on
agents and RPC calls may not be the best way forward. Projects like [OVN][8], [OpenDaylight][9], [OpenContrail][10], and [Ryu][11]
have teams dedicated to solving SDN problems in the Open. By splitting out the reference Neutron implementation, we will allow
that to evolve independent of Neutron.

Perhaps the Neutron SDN solution will become a viable alternative to the existing options. But at the end of the day, we'll be
continuing to enable Neutron as a platform, which is where we want to evolve it.

[1]: https://wiki.openstack.org/wiki/Kilo_Release_Schedule
[2]: https://launchpad.net/neutron/+milestone/kilo-1
[3]: https://launchpad.net/neutron/+milestone/kilo-2
[4]: https://launchpad.net/neutron/+milestone/kilo-3
[5]: https://launchpad.net/neutron/+milestone/kilo-rc1
[6]: https://blueprints.launchpad.net/neutron/+spec/services-split
[7]: http://siliconloons.com/posts/2014-12-26-neutron-splits-and-spinouts/
[8]: http://networkheresy.com/2015/01/13/ovn-bringing-native-virtual-networking-to-ovs/
[9]: http://www.opendaylight.org
[10]: http://www.opencontrail.org
[11]: http://osrg.github.io/ryu/

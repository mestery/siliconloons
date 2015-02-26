+++
Description = "Scaling OpenStack Neutron Development"
author = "mestery"
categories = ["Neutron", "OpenStack", "Community", "Open Source"]
date = "2015-02-26T14:01:04-06:00"
socialsharing = true
tags = ["Neutron", "OpenStack", "Community", "Open Source"]
title = "Scaling OpenStack Neutron Development"
url = ""

+++
We're nearing the end of the [Kilo](https://wiki.openstack.org/wiki/Kilo_Release_Schedule) development cycle. This is typically
where the rubber meets the road, as we're trying our hardest to merge a lot of code near the end. It's a fairly busy part of
the cycle. I wanted to take a moment to write about two efforts which will help to scale Neutron development in Kilo and beyond.

The Kilo cycle has involved a couple of efforts which are meant to expand and scale the Neutron development community. These
efforts are [Plugin Decomposition](http://specs.openstack.org/openstack/neutron-specs/specs/kilo/core-vendor-decomposition.html)
and the [Advanced Services Split](http://specs.openstack.org/openstack/neutron-specs/specs/kilo/services-split.html). Both of
these were designed to enable a more scalable development environment which will allow for fast code iteration in all the
areas affected. How have we done with these? Lets take a look at each individually.

## Plugin Decomposition
As of the Kilo-2 milestone, Neutron has a total of 48 plugins and drivers. These span everything from basic L2 plugins, L2
ML2 MechanismDrivers, L3 service plugins, and advanced service plugins for FWaaS, LBaaS and VPNaaS. Not only is that a lot
of plugins, it's also by far the largest amount of plugins and drivers for any OpenStack project. Given that Neutron has
only 14 core reviewers, the amount of code required to review across those drivers and plugins was growing by leaps and
bounds. For example, we had around 10 additional plugins/drivers proposed for Kilo. Core reviewers who were reviewing all the
backend logic in these plugins and drivers were left reviewing code for which they had no knowledge of the backend logic,
nor could they test a lot of these due to lack of hardware or software from the various vendors. The model we had when
we started with a small number of plugins and drivers was no longer scaling. Something had to change.

Enter "Plugin Decomposition." The idea here is that all upstream plugins and drivers will leave a small shim in-tree in
the Neutron git repository, and move all their backend logic out. Most chose to move it to [StackForge](https://github.com/stackforge),
with some moving straight to GitHub. The benefit is clear to all parties involved: Neutron core reviewers can now
focus on reviewing core Neutron code, and plugin maintainers can now iterate at their own pace in their plugins and
drivers, releasing when they want. Everyone gets faster merges, greater velocity, and ultimately faster innovation
speed.

## Advanced Services Split
All of the advanced services in Neutron (FWaaS, LBaaS, and VPNaaS) used to have their code in the Neutron git repository.
The teams working on these projects were suffering from a similar fate as the plugins: Lack of reviews by Neutron core
reviewers. They also wanted to iterate faster and drive new features at a fast pace. Thus, the idea of spinning these
into their own git repositories was proposed and ultimately implemented. These git repositories still reside as a part of
Neutron, but they have separate (and sometimes overlapping) core reviewer teams.

Similar to decomposition, this has been a success. The LBaaS team in particular has moved fast and created a new LBaaS
API, the LBaaS V2 API. The VPNaaS team has moved to solidify their testing, including new Tempest scenario tests. And
the FWaaS team is fixing a long-standing issue around deploying multiple FWs per tenant. The early results are very
positive here as well.

## Innovation in Neutron Moving Forward
Neutron is well positioned now moving forward to enable innovation at all the different layers. Plugin and driver maintainers
can now iterate quickly. Advanced services can move at their own pace within the existing release window. And core
Neutron can now continue evolving into a solid API endpoint and DB layer. All of these changes are wins for the end
users of Neutron, and OpenStack in general.

---
title: How to Effectively Contribute to An Open Source Project Such As OpenStack Neutron
author: mestery
layout: post
date: 2014-07-24
url: /how-to-effectively-contribute-to-an-open-source-project-such-as-openstack-neutron/
tmac_last_id:
  - 544155995526934529
categories:
  - Commentary
  - Open Source
tags:
  - Community
  - Open Source
  - OpenStack
---
Since being <a title="Juno PTL Email Announcement" href="http://lists.openstack.org/pipermail/openstack-dev/2014-April/032487.html" target="_blank">elected</a> as the OpenStack Neutron PTL, I&#8217;ve been mostly heads down working to ensure the Neutron project has a successful Juno release. Increasingly, and especially near <a title="Juno Release Schedule" href="https://wiki.openstack.org/wiki/Juno_Release_Schedule" target="_blank">OpenStack Juno milestone deadlines</a>, I&#8217;m seeing frustration from new contributors around their contributions to Neutron. I sent an <a title="Contributing to Neutron email" href="http://lists.openstack.org/pipermail/openstack-dev/2014-July/041136.html" target="_blank">email</a> to the openstack-dev mailing list this morning addressing this in a terse form, this blog is an attempt to expand upon that email.

An increasing concern I see from people who are new contributors is the perceived issues in getting their code merged into Juno. The common concerns come from one of the following possible ideas:

  1. OpenStack Neutron is a &#8220;closed development&#8221; environment where only a select few are allowed to make changes.
  2. OpenStack Neutron is part of some grand conspiracy by *vendor X*, and as I work for *vendor Y,* my changes never get merged.
  3. OpenStack Neutron needs more core developers, this would solve all the velocity problems.

Addressing the above concerns in order, OpenStack Neutron is not a &#8220;closed development&#8221; environment. We do all of our work in the open by using mailing lists andIRC (for both meetings and discussions). Anyone can submit a patch to OpenStack Neutron once you&#8217;ve signed the CLA and followed the process <a title="How to Contribute to OpenStack" href="https://wiki.openstack.org/wiki/How_To_Contribute" target="_blank">here</a>. We welcome new contributors and do our best to work with them! My advice for new contributors, echoed below, is to start small, listen and learn.

The second concern around conspiracy theories comes from people who are frustrated that their specification or blueprint isn&#8217;t prioritized for inclusion into a specific Juno release. They may also work for a competing company of some existing Neutron core developer, and think there is some political machinations going on here. While it&#8217;s true upstream developers work for corporations (we like to get paid and feed our families, it&#8217;s true!), it&#8217;s also true the core team in particular works together as a team. This means that people who work for Cisco do in fact work with people from VMware, as an example. We&#8217;re all working to drive stability and innovation upstream, but we do it in an open and collaborative manner.

The third concern is a tricky one. While adding more core reviewers would certainly help spread the load, we&#8217;re generally picky about adding new ones and have a <a title="Neutron Core Developer Policy" href="https://wiki.openstack.org/wiki/NeutronCore" target="_blank">policy</a> in place around how we do this. The reason we&#8217;re picky is because being a core reviewer is a big responsibility, and we want dedicated developers who can contribute time upstream for the role. We&#8217;re in the process of coming up with a mentoring program to groom Neutron core developers, which will hopefully help here.

I&#8217;d like to reiterate from the email a list of effective ways to contribute to an upstream Open Source project:

  1. Get involved in the ways the project uses to communicate, including IRC, mailing lists, Hangouts, phone calls, whatever they use.
  2. Work upstream to fix some bugs. Documentation bugs and low-hanging fruit bugs are a good place to start.
  3. Understand how the existing team works. It&#8217;s best to understand this before suggesting any changes.
  4. Come to weekly meetings. Make sure you spend a little while listening to understand how the existing team works before jumping in with your own agenda.
  5. Build relationships. Doing the 4 points above will naturally lead you to this point.

An Open Source project is really a large development project being done in the open. To effectively join this project, you need to learn how the project operates and contribute in small ways initially. As in close sourced development, gaining the trust of the existing contributors is key to having influence over the direction of the project. The existing developers for a project such as Neutron (both core and non-core developers) all spend varying amount of time upstream working. But the key point is that they have taken the time to develop their contributions as well as grow relationships with existing upstream developers.

Upstream effectiveness is really about the time you put into your contributions. As existing developers upstream, we&#8217;re responsible for the current and future state of a project like OpenStack Neutron. While we have <a title="Neutron Policies" href="https://wiki.openstack.org/wiki/NeutronPolicies" target="_blank">policies</a> in place dictating how we work, we&#8217;re also responsible for things like gate failures, bug regressions, packaging issues, broad community interaction, and core developer grooming, among other things.

This post isn&#8217;t meant to discourage anyone from being an upstream developer. Quite the contrary, actually. I&#8217;m hoping to highlight effective ways to work upstream, which is beneficial for both new contributors as well as existing contributors. At the end of the day, a project like OpenStack Neutron involves people from across a wide spectrum of companies and interests. As the PTL, it&#8217;s my job to lead these people to a common goal. Growing the base of contributors is part of this responsibility as well. I look forward to seeing new contributors in Neutron and OpenStack in general!
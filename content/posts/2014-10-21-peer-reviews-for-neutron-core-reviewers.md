---
title: Peer Reviews for Neutron Core Reviewers
author: mestery
date: 2014-10-21
url: /peer-reviews-for-neutron-core-reviewers/
socialsharing: true
tmac_last_id:
  - 544155993249439745
categories:
  - OpenStack
tags:
  - Neutron
  - Open Source
  - OpenStack
  - Peer Review
---
As I was recently <a title="Kilo PTL Announcement" href="http://lists.openstack.org/pipermail/openstack-dev/2014-October/047733.html" target="_blank">given the chance</a> to serve as Neutron PTL for a second cycle, I thought it would be a good idea for me to share some insight into what I&#8217;m hoping to achieve upstream in Kilo. I&#8217;ll have some upcoming posts on what we&#8217;re planning on accomplishing, but I wanted to first start with a post about the actual people who are allowed to merge code into Neutron, the core reviewers.

## Core Reviewers

Neutron has 14 total core reviewers. You can see a list of these and also some notes around this on our <a title="Neutron Cores" href="https://wiki.openstack.org/wiki/NeutronCore" target="_blank">wiki</a>. Cores are responsible for reviewing code submissions submitted to Neutron&#8217;s gerrit, as well as merging those code submissions. They are also responsible for other things, most of which fall in a grey zone and aren&#8217;t documented that well. We&#8217;ll come back to this part in a bit.

The Neutron team has added a small handful of cores as the project has gone on, and we&#8217;ve also lost a small handful of people. But for the most part, once you&#8217;re a core, you remain a core forever. While this approach has served it&#8217;s purpose, there are issues with it.

## Improving the Core Experience

OpenStack is always trying to improve things around not only code quality but also governance, so members of the Neutron community have taken it upon themselves to improve the process by which we understand a core&#8217;s responsibilities, and also a process under which we can judge how cores are performing up to that standard. The idea is to allow for the constant and consistent evaluation of existing Neutron cores. The long-term goal is to use the mechanism to also vet potential new cores. It&#8217;s an ambitious goal, and it takes into account more than just reviews, but also the grey zone aspects of being core which are hard to document.

This grey zone includes things such as community leadership, how you interact with the rest of the community, and participation in things like weekly meetings, IRC chats, and mailing list conversations. It includes mentoring of new contributors (something we haven&#8217;t recognized officially, but which happens). It also includes interactions with other OpenStack projects, and the leadership around being a liaison from Neutron into these other projects. It even includes evangelism for Neutron. All of these things are done by Neutron core team members.

## Neutron Core Team Peer Review

The result of this has led us to begin to implement a Peer Review process for Neutron core team members. This is currently documented on an <a title="Neutron Peer Review Etherpad" href="https://etherpad.openstack.org/p/neutron-peer-review" target="_blank">etherpad</a>, and we&#8217;re in the process of collecting one more round of feedback. I&#8217;m highlighting this process here so people can provide input for this process. The goal is to keep this lightweight at first, and collect a good amount of actionable information to relay back to the existing core reviews. See the etherpad link for more info.

The end result of this is that we as a Neutron core team hope to better define what it means to be a Neutron core team member. We also hope to provide actionable feedback to existing members who may have strayed from this definition. A stronger Neutron core team benefits the entire OpenStack ecosystem. I&#8217;m proud of the work our Neutron core team is doing, and I hope we can continue to grow and evolve Neutron cores in the future by using this new Peer Review process.

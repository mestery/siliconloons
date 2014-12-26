---
title: 'Building Value with SDNs: RouteFlow'
author: mestery
date: 2011-11-15
url: /building-value-with-sdns-routeflow/
socialsharing: true
views:
  - 1
tmac_last_id:
  - 544156017571790848
categories:
  - SDN
tags:
  - Open vSwitch
  - OpenFlow
  - RouteFlow
  - SDN
---
With <a title="Open Networking Summit" href="http://opennetsummit.org/past_conferences.html" target="_blank">all of the talk</a> regarding Software Defined Networks (SDN), it&#8217;s easy to get lost trying to understand where the value will be. The general consensus here is that value will be built on top of SDN. SDN is, in essence, a building block.

One interesting project providing value by using SDN as a building block is the <a title="RouteFlow" href="https://sites.google.com/site/routeflow/" target="_blank">RouteFlow</a> project. The goal of the project, taken straight form the front page, is:

> RouteFlow is an open source project to provide virtualized IP routing services over OpenFlow enabled hardware. RouteFlow is composed by an OpenFlow Controller application, an independent RouteFlow Server, and a virtual network environment that reproduces the connectivity of a physical infrastructure and runs IP routing engines (e.g. Quagga).

In this case, RouteFlow is trying to provide an open source virtual IP routing solution. The value lies not in the SDN, but in the routing software sitting on top of the SDN here. SDN is important, in that it allows RouteFlow to specifically program forwarding entries using OpenFlow. But the real value lies in the orchestration layer (in this case the RouteFlow Server) sitting on top, performing the orchestration.

Expect to see more projects, especially open source projects, providing value by using SDN in the future.

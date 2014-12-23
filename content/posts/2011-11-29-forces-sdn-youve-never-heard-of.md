---
title: 'ForCES: SDN You’ve Never Heard Of'
author: mestery
layout: post
date: 2011-11-29
url: /forces-sdn-youve-never-heard-of/
tmac_last_id:
  - 544156017517277184
categories:
  - ForCES
  - OpenFlow
  - SDN
tags:
  - ForCES
  - OpenFlow
  - SDN
---
With all the hoopla surrounding SDN, <a title="OpenFlow not the only path to network revolution" href="http://www.networkworld.com/news/2011/111711-sdn-openflow-253228.html" target="_blank">in all of it&#8217;s forms</a>, I thought it would be interesting to look at a possible predecesor to OpenFlow, at least in spirit: The <a title="ForCES Protocol" href="http://tools.ietf.org/html/rfc5810" target="_blank">ForCES protocol</a>. From RFC 5810, we have the following description of ForCES:

> Forwarding and Control Element Separation (ForCES) defines an architectural framework and associated protocols to standardize information exchange between the control plane and the forwarding plane in a ForCES Network Element (ForCES NE).

For OpenFlow, if we look at wikipedia for a quick definition, we see the below:

> **OpenFlow** is a [communications protocol][1] that gives access to the [forwarding plane][2] of a [network switch][3] or [router][4] over the network.<sup id="cite_ref-0"><a href="http://en.wikipedia.org/wiki/Openflow_Switching_Protocol#cite_note-0">[1]</a></sup> In simpler terms, OpenFlow allows the path-of-network-packets-through-the-network-of-switches to be determined by software running on a separate [server][5]. This separation of the control from the forwarding allows for more sophisticated traffic management than feasible using [access control lists][6] (ACL)s and routing protocols.

In essence, what OpenFlow is proposing (separation of control and forwarding plane), was proposed years earlier by ForCES. While ForCES has been around in the IETF for years (there are even old mailing list archives <a title="ForCES Mailing List Info" href="https://www.ietf.org/mailman/listinfo/forces-protocol" target="_blank">here</a>), it has never achieved OpenFlows level of celebrity. I guess, even for network protocols, timing is everything.

 [1]: http://en.wikipedia.org/wiki/Communications_protocol "Communications protocol"
 [2]: http://en.wikipedia.org/wiki/Forwarding_plane "Forwarding plane"
 [3]: http://en.wikipedia.org/wiki/Network_switch "Network switch"
 [4]: http://en.wikipedia.org/wiki/Router_(computing) "Router (computing)"
 [5]: http://en.wikipedia.org/wiki/Server_computer "Server computer"
 [6]: http://en.wikipedia.org/wiki/Access_control_list "Access control list"
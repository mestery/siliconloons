---
title: What’s New in Neutron for OpenStack Juno
author: mestery
layout: post
date: 2014-10-10
url: /whats-new-in-neutron-for-openstack-juno/
tmac_last_id:
  - 544155993249439745
categories:
  - OpenStack
tags:
  - Neutron
  - OpenStack
---
As of today, we just published the second <a title="Neutron Juno-RC2" href="https://launchpad.net/neutron/+milestone/juno-rc2" target="_blank">Juno release candidate for Neutron</a>. The expectation is this will be the final RC candidate and will become the official 2014.2 release of OpenStack Neutron. I thought I would take a moment to highlight some of the awesome work done by our community during the past 6 months.

## Distributed Virtual Router

By far one of the largest, if not the largest, features we added as a team was the addition of <a title="Distributed Virtual Routing in Neutron" href="https://wiki.openstack.org/wiki/Neutron/DVR" target="_blank">Distributed Virtual Router</a> (DVR) functionality. The team working on this has spent multiple cycles iterating on this code, and it finally landed in Juno. This is an exciting development because in prior versions of Neutron, the default L3 routing behavior was to send all traffic to L3 network nodes for routers. Clearly this presents issues around single points of failure on those L3 network nodes, not to mention the issue around having those L3 nodes become traffic bottlenecks. With DVR, routing functionality is distributed to each compute node, removing the need for a central L3 network node for this functionality. NAT functionality is also distributed in a similar manner. SNAT, however, is still centralized. The reason for this is due to the requirement of burning an IPV4 address on each compute node in a distributed SNAT environment. The wiki listed above has many more details on the DVR architecture.

## IPV6

The Juno release of Neutron will close the gaps on IPV6 support for tenant networks, allowing full IPV6 for tenant networks. We&#8217;ve added the capability for Neutron to manage the RADVD daemon to serve IPV6 RAs when required. For those looking to deploy Neutron in a pure IPV6 environment, you&#8217;ll find Juno allows for such deployments.

## Security Group Enhancements

There are some <a title="Scaling Openstack to 168k instances" href="http://javacruft.wordpress.com/2014/06/18/168k-instances/" target="_blank">well known issues</a> around security group scaling with previous versions of OpenStack Neutron. In Juno, we&#8217;ve addressed these issues with two very important blueprints: The addition of ipset in lieu of iptables to manage security group rules on compute nodes, and the refactoring of the security\_group\_rules\_for\_devices RPC call. Both of these additions are meant to scale and dramatically improve the performance of the security groups implementations of Neutron.

## L3 Agent Improvements

We made some serious <a title="L3 Agent Performance Improvements" href="https://blueprints.launchpad.net/neutron/+spec/l3-agent-responsiveness" target="_blank">performance improvements</a> in the L3 agent during Juno, as well as added the capability to have <a title="HA for L3 Agent" href="https://blueprints.launchpad.net/neutron/+spec/l3-high-availability" target="_blank">HA for the L3 agent.</a> Both of these will help with users deploying the Neutron L3 agent. The HA work in particular means you can now have redundancy for L3 agents. As I mentioned earlier, the L3 agent is still required for SNAT traffic for DVR. So this improvement means there is no longer a single point of failure for that traffic when using the DVR solution. For deployers who choose not to use DVR, now you can have HA for all your L3 routing and NAT traffic as well.

## Summary

I&#8217;ve just highlighted some of the many improvements we&#8217;ve made in Juno for Neutron. For information on more features, including new plugins and drivers, checkout the <a title="Juno Neutron Release Notes" href="https://wiki.openstack.org/wiki/ReleaseNotes/Juno#OpenStack_Network_Service_.28Neutron.29" target="_blank">release notes.</a> We&#8217;re excited by the work the Neutron community has done for Juno, and we&#8217;re looking forward to an exciting development cycle for Kilo as well!
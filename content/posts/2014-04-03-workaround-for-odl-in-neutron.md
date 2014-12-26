---
title: Workaround for ODL in Neutron
author: mestery
date: 2014-04-03
url: /workaround-for-odl-in-neutron/
socialsharing: true
tmac_last_id:
  - 544155997401776128
categories:
  - OpenStack
tags:
  - CI
  - OpenDaylight
  - OpenStack
---
With the Icehouse release of Neutron impending, we&#8217;ve unfortunately uncovered a <a title="ODL Bug" href="https://bugs.launchpad.net/neutron/+bug/1301449" target="_blank">bug</a> which is affecting ODL integration with Neutron. This bug was introduced by <a title="Notify Nova from Neutron" href="https://review.openstack.org/#/c/75253/" target="_blank">this commit</a>, and the reality is better CI for the ODL plugin would have caught this. I&#8217;m going to work to enable this better CI in the near future. The workaround for this is to add the following in your nova.conf:

<pre style="padding-left: 30px;">vif_plugging_&lt;wbr />timeout = 10
vif_plugging_&lt;wbr />is_fatal = False</pre>

I&#8217;m working on fixing this right now. Implementing the fix above in your nova.conf will get you running again with ODL and OpenStack Neutron. Thanks to Simon Pasquire for finding this bug and noting the workaround as well!

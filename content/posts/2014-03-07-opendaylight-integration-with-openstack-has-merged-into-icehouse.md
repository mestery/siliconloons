---
title: OpenDaylight Integration with OpenStack has merged into Icehouse!
author: mestery
date: 2014-03-07
url: /opendaylight-integration-with-openstack-has-merged-into-icehouse/
socialsharing: true
tmac_last_id:
  - 544155999137853440
categories:
  - Open Source
  - OpenStack
tags:
  - Group Policy
  - Open Source
  - OpenDaylight
  - OpenStack
---
As OpenStack marches towards it&#8217;s Icehouse release this spring, some work I&#8217;ve been doing has finally merged upstream. This week, both the <a title="OpenDaylight ML2 MechanismDriver Review" href="https://review.openstack.org/#/c/69775/" target="_blank">OpenDaylight ML2 MechanismDriver</a> and <a title="devstack support for OpenDaylight" href="https://review.openstack.org/#/c/69774/" target="_blank">devstack support for OpenDaylight</a> merged upstream. This was a huge effort which spans the efforts of many people. This was the first step in solidifying the integration of OpenDaylight with OpenStack Neutron, and we have many additional things we can do. To get a first taste of running the two together, please see the <a title="OpenStack Neutron Integration with OpenDaylight" href="http://youtu.be/3MkCiHeH_Fo" target="_blank">video</a> of the OpenDaylight Summit presentation myself, Madhu Venugopal, and Brent Salisbury did in early February.

# Taking OpenDaylight For a Test Run With OpenStack Neutron

Now that the patches have merged upstream, trying this out is extremely simple. If you&#8217;re running a single node, you can simple setup the Neutron portion of your local.conf as follows and OpenDaylight will be downloaded and run as a top-level devstack service:

<pre># ODL WITH ML2
Q_PLUGIN=ml2
Q_ML2_PLUGIN_MECHANISM_DRIVERS=opendaylight,logger
enable_service odl-server odl-compute</pre>

That&#8217;s all that&#8217;s required. When you run &#8220;stack.sh&#8221;, you will see a screen called &#8220;odl-server&#8221; which will be OpenDaylight. And Neutron will use OpenDaylight to satisfy the requirements of virtual tenant networks.

If you&#8217;re trying this with a multi-node setup, you can use the above for your controller. And on your compute nodes, try this addition to local.conf:

<pre>enable_service odl-compute</pre>

That will configure the host to use Open vSwitch and set it up to point at OpenDaylight. It will also ensure Nova is setup to use Neutron for networking API calls.

## Running OpenDaylight Outside of devstack

If you&#8217;re running OpenDaylight outside of devstack, you can configure your control node like this:

<pre>Q_PLUGIN=ml2
Q_ML2_PLUGIN_MECHANISM_DRIVERS=opendaylight,logger
enable_service odl-compute
ODL_MGR_IP=x.x.x.x</pre>

Just replace x.x.x.x in the ODL\_MGR\_IP line with the IP of your running OpenDaylight instance.

For compute hosts, all you need to add is this:

<pre>enable_service odl-compute
ODL_MGR_IP=x.x.x.x</pre>

Again, just replace x.x.x.x in the ODL\_MGR\_IP line with the IP of your running OpenDaylight instance. Your control and compute nodes will now utilize an external OpenDaylight controller.

## Additional Configuration Values

There are some additional things you can configure for OpenDaylight. They are:

  * ODL\_ARGS: This value can be set to options to pass OpenDaylight. The default is &#8220;-XX:MaxPermSize=384m&#8221;. An example would be like this:ODL\_ARGS=&#8221;-Xmx1024m -XX:MaxPermSize=512m&#8221;
  * ODL\_BOOT\_WAIT: This value indicates how long to sleep after starting OpenDaylight before proceeding with the rest of devstack. The default value is 60 seconds. An example is like this:  
    ODL\_BOOT\_WAIT=70

# The Future of Open Source SDN

OpenDaylight is progressing at a very fast pace. The current release being worked on (Helium) is going to stabilize and scale the platform even more. With features like <a title="OpenDaylight Group Policy" href="https://wiki.opendaylight.org/view/Project_Proposals:Application_Policy_Plugin" target="_blank">Group Policy</a> being added, the future looks increasingly awesome for OpenDaylight. And now you can use it to scale your Neutron networks as well. How cool is that?

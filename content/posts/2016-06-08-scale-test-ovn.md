+++
Description = "Scale Testing OVN"
author = "mestery"
categories = ["OVN", "Open Source", "Networking"]
date = "2016-06-08T16:31:26-04:00"
socialsharing = true
tags = ["OVN", "Open Source", "Networking"]
title = "Scale Testing OVN"
url = ""

+++

Recently, I've been spending an increasing amount of time building a virtual
networking layer. Of course, I'm doing this using both [Open vSwitch][1] as
well as [OVN][2]. I've been lucky enough to be a part of a [few talks][3] on
OVN, so I won't go into many details on OVN here. But I will say we've found
it to be a great solution to solving virtual networking at scale. What I'd
like to discuss here is some of the things we're testing with regards to OVN
at scale.

What Is Scale
-------------

Scale means different things to different people. In the case of what I've
been working on, I interpret it to loosely mean a deployment starting in the
hundreds of hypervisors and growing into the thousands of hypervisors. Your
definition of scale may be different. But for the targets we're looking at,
this is a reasonable place to start.

Testing Virtual Networking At Scale
-----------------------------------

Now that we have a good level set on scale, it's worth discussing exactly what
we'll be testing at scale, and what we'll be looking for. In particular, we
want to load the system up with many logical entities. This includes the
following:

* Total number of virtual networks.
* Total number of subnets per network.
* Total number of ports per network and subnet.
* Total number of routers in the system.
* Total number of routers per shared network.
* Total number of routers per provider network.
* Total number of private networks per router.
* Total number of routers per private network.
* Security group scalability.

When it comes to testing virtual networking at scale, the first thing to keep
in mind is that you need to not only test the total scale of your deployment,
but also the rate of change of that environment. In other words, once you load
an environment up, the expectation is it will generally only grow larger. So
with that in mind, the following are all useful to test:

* Ports created and destroyed per minute, noting how long it takes the
  port to become active.
* Networks created and destroyed per minute
* Subnets created and destroyed per minute
* Routers created and destroyed per minute
* Router interfaces added and removed per minute

One thing to note about all of the above is that we are testing and stressing
the OVN control plane. We are not doing any dataplane testing with the above.
This testing is very valid and important, as scaling the control plane and
ensuring it performs adequately while under load ensures a smooth user
experience.

Where Do We Go From Here
------------------------

So, how do we go about testing OVN at some sort of reasonable scale? Obviously
actually deploying a system with hundreds and thousands of hypervisors would be
ideal. But that's somewhat impractical to do when integrating with a CI/CD
system. A more practical choice is to try and emulate this. Thus, the
[ovn-scale-test][4] git repository was born.

The ovn-scale-test repository was created jointly by some great folks at both
IBM and eBay. It's goal is to produce some level of scale testing which can be
emulated. It does this by using OVS sandboxes to emulate the underlying OVS
which runs on hypervisors.

Specifically, we will be using the work done to make all of this run in docker
containers using ansible. A great set of instructions on how to do this exist
[here][5] in the git repository. This makes adding this scale testing and data
collection easy and possible to insert into a CI/CD system. I will go into more
detail on this in a future blog post. Some of the things we want to test need
to be added to this system, for example.

Scale Testing In a CI/CD System: The End Goal
---------------------------------------------

What we've been able to do with the above is integrate scale testing into our
CI/CD system for OVN and OVS. This allows us to collect data as we push
changes, whether those changes are upstream changes or changes we roll locally.
And this data allows us to see performance metrics across versions and builds,
allowing us to make data-backed decisions on rolling code out into production.
Ultimately, this is the goal: Catching changes which introduce performance
degradations into the OVN control plane before they land in production. And
this system lets us get there and make that a reality.

[1]: http://openvswitch.org/
[2]: http://openvswitch.org/support/dist-docs/ovn-architecture.7.html
[3]: https://www.openstack.org/summit/vancouver-2015/summit-videos/presentation/ovn-native-virtual-networking-for-open-vswitch
[4]: https://github.com/openvswitch/ovn-scale-test
[5]: https://github.com/openvswitch/ovn-scale-test/tree/master/ansible

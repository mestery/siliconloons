+++
Description = "Neutron RFE Process"
author = "mestery"
categories = ["OpenStack", "Neutron", "Process"]
date = "2015-06-01T11:02:20-05:00"
socialsharing = true
tags = ["OpenStack", "Neutron", "Process"]
title = "Neutron RFE Process"
url = ""

+++

Starting with the development of the Juno release, the Neutron project moved to
using a [specs repository][1] similar to how other projects were using them. In
our quest to enforce a [waterfall design model][2], we also added an
appropriate [spec template][3] which was filled with things such as "Problem
Description", "REST API Impact", "IPv6 Impact", "Community Impact", and
everyone's favorite sections on "Testing" and "Documentation." We deployed this
with the best of intentions and the greatest of hopes. And we used this process
for both Juno and the Kilo cycle.

How did the process work? At best, it lengthened the pipeline we had in place
to gate the incoming feature fire-hose. At worst, it turned off potential
committers. In the interest of [stepping out of the way][4], it was time to
change the process and refocus on what we really wanted to solve.

Who Are the Users Of Neutron?
-----------------------------

Asking this question was at the heart of what reforming the process. The old
process was not easy for non-developers to contribute to. It required you to
clone a gerrit repository and take the time to actually fill in a lengthy
document, including detailed design decisions. This wasn't going to work for
someone who was not inclined to code. In reality, we had very little feedback
from operators and users on our specs process. I blame the template.

In reality, we would love to get feedback from users. These are the people who
we are designing the software for. The new process had to take this into account
from the start.

The Request For Enhancement (RFE) Process
-----------------------------------------

Over the past month, the Neutron team has been iterating on the new process.
I'm happy to announce we've merged the patches for this and we are now going to
give it a new try. And what is this new process? A quick summary is as follows:

* A [slimmed down spec template][5] which focuses on the "what" instead of the
  "how."
* A process which emphasizes filing [RFE bugs][6] instead of detailed design
  documents.
* The removal of deadlines. No more deadlines for filing RFEs or specs.

The RFE process is meant to allow users to express their desires for new
features using Launchpad. A quick review of these RFE bugs can be done and they
can turn into features should the need arise. The process is streamlined as
well with no additional deadlines. Overall, a win-win for all interested
parties.

The Future
----------

As with most things in OpenStack, the only constant is change. We'll try this
out for the Liberty release and we'll make adjustments during the Mxx release
design summit. But with a focus on allowing users to express their interest in
features, the process is already a vast improvement over the prior way to
submit code into Neutron.

[1]: http://git.openstack.org/cgit/openstack/neutron-specs/
[2]: https://en.wikipedia.org/wiki/Waterfall_model
[3]: https://github.com/openstack/neutron-specs/blob/8630afb8f0aa9be6f3ccbf3be761e054412d3c6a/specs/template.rst
[4]: http://ttx.re/stepping-out-of-the-way.html
[5]: https://github.com/openstack/neutron-specs/blob/master/specs/template.rst
[6]: https://bugs.launchpad.net/neutron/+bugs?field.tag=rfe

+++
Description = ""
author = "mestery"
categories = ["OpenStack", "Open Source"]
date = "2014-12-26T13:22:28-06:00"
socialsharing = true
tags = ["Open Source", "OpenStack", "Neutron"]
title = "Neutron Splits And Spinouts"
url = ""

+++

Now that we're past a very busy December which included the
[Neutron mid-cycle in Lehi, Utah](https://wiki.openstack.org/wiki/Sprints/NeutronKiloSprint),
the [Neutron Spec Proposal and Approval Deadline](http://lists.openstack.org/pipermail/openstack-dev/2014-December/052533.html),
the [Kilo-1 release of Neutron](https://launchpad.net/neutron/+milestone/kilo-1),
as well as some
[holiday's enjoyed around the world in December](http://en.wikipedia.org/wiki/List_of_multinational_festivals_and_holidays#December),
I thought it was time to take a moment and blog about where we are in Neutron, and some of the important
changes coming in the Kilo release. These changes will affect everyone from developers to deployers, from operators to packagers.
I'm hoping the information I'm sharing here will spark some conversations around these ideas for people who may have
only heard passing information on them.

Neutron Services Split
----------------------
Over the years, Neutron's job has grown from providing not only L2 and L3 network services, but also into providing higher-level
abstractions. These have included Load Balancers (LBaaS), Virtual Private Networks (VPNaaS), and Firewalls (FWaaS).
These services have all been formed in the Neutron repository itself, and have gradually expanded the Neutron API
to include these higher level L4-L7 services as a part of it. The services themselves have continued to evolve along with Neutron.
For instance, LBaaS recently worked hard during the Juno cycle to come up with the LBaaS V2 API definition.

During the end of the Juno development cycle, the Neutron core team began to think about how we could continue to scale
and evolve work in Neutron. As the scope of what Neutron would cover began to grow, the project itself continued growing,
including more advanced services sitting above the original L2 and L3 areas Neutron covered. It also became clear the teams
working on FWaaS, LBaaS, and VPNaaS wanted to iterate at their own pace.

The result of this is that during Kilo we've decided to spin these services out of the main Neutron git repository into their
own git repositories. They will share the same [Launchpad project](https://launchpad.net/neutron). This means bugs and blueprints
will be handled in a central location. But the code itself will be in a separate git repository. The core reviewing team for these
new repositories will be separate (though somewhat overlapping) with the base Neutron core reviewing team.

During the Neutron mid-cycle, we performed the actual split. In fact, we released Neutron Kilo-1 with the split repositories.
This meant Neutron now had four tarball files, which will affect packagers. The release itself went smoothly, though we're
still fixing a few issues found during testing post split and post release.

Neutron Plugin Decomposition
----------------------------
The number of plugins and drivers for Open Source and vendor projects has steadily grown in Neutron over the years.
When we released Juno, we had the following stats for plugins and drivers:

* Monolithic plugins: 18
* ML2 drivers: 15
* Service plugins: 13

Of those, we added 9 in the [Juno](https://launchpad.net/neutron/+milestone/2014.2) release itself. With each new release,
there is increasingly more plugins and drivers proposed upstream. As a community, we're thrilled about this. But we've
struggled with the cost of maintaining these drivers and plugins upstream. Notably, the projects and vendors who own
the backends for these plugins and drivers have also struggled. Clearly, something needed to change.

Near the end of Juno, the Neutron core team began to think about we could effectively continue evolving Neutron's ecosystem,
while at the same time providing clear and consistent code reviews of upstream code in a timely manner. The thinking lead
to the publishing and approval of the spec "[Proposal for Neutron core and vendor code decomposition](http://specs.openstack.org/openstack/neutron-specs/specs/kilo/core-vendor-decomposition.html)
(gerrit review [here](https://review.openstack.org/#/c/134680/))". The specs author, [Armando Migliaccio](https://twitter.com/armandomi2001), did a great job iterating on the
spec, taking suggestions and working to build consensus.

The *tl,dr* of the spec is the idea that in-tree plugins should be a thin shim, with the backend logic being out of the
upstream Neutron tree and living somewhere else ([stackforge](https://github.com/stackforge) and
[github](http://www.github.com/) are logical places).

The longer version of what this means is as follows:

1. Plugin owners are encouraged to work at thinning their plugins during the Kilo development cycle.
2. During the "Lxxx" cycle, the Neutron core review team will enforce this thinning, with plugin removal an option for those
who have not started their "thinning."
3. Once a plugin is "thinned", the backend logic will now be under the control of the plugin owner.
4. Code changes in the backend will go through a separate review process, and release process. This process will now be
controlled by the plugin owner.
5. Packagers will be required to package the dependencies of the new "thinned" plugins and drivers.

I should note Armando has done a great job of writing instructions for developers. It's currently under review in
gerrit [here](https://review.openstack.org/#/c/141171/). The instructions paint a clear picture for how an existing upstream,
in-tree plugin or driver can be "thinned" and comply with the decomposition specification.

All of this work is meant to address the concerns around code review time, the size of the neutron code base, and the process
involved with getting your plugin upstream. By enabling plugin and driver owners to iterate at their own pace in their
backend technology, we'll unlock them and let them move at their own pace. We'll also relieve the Neutron team from
reviewing code for these backend plugin and driver implementations, and focus on core Neutron itself.

How Will These Changes Affect Me?
---------------------------------
The Services Split and Plugin Decomposition will affect people in different ways. I've tried to capture this at a high
level below.

1. Developers  
   Developers will be impacted positively by these changes. Those working in the services area will now have their own git
   repository to iterate in. Those working on core Neutron will have less code to review. The groups can now move at their own
   pace with their own focus. The same is true for plugins. Plugin owners can now iterate in their own repository with their own
   team, and not be reliant on Neutron reviewers for getting their backend specific changes upstream.
2. Operators and Deployers  
   Operators and deployers will be impacted if they run any Neutron advanced services (FWaaS, LBaaS, or VPNaaS). Starting from Kilo,
   a new package will need to be installed to retain the usage of these services. Since the new services will utilize the existing
   Neutron API endpoint, no change from a tenant perspective is expected. But upgrades from Juno to Kilo will be impacted, as will
   fresh installs for those used to the pre-Kilo Neutron. From a plugin perspective, the change is expected to be transparent to
   operators and deployers.
3. Packagers  
   Packagers for distributions are likely to be affected by both the services split and the plugin decomposition work. This will
   require them to package additional files in the case of plugin decomposition (the out-of tree bits for the plugins will now have
   their own releases on something like PyPi). For the services split, packaging Neutron will now mean you will need to package four
   tarballs instead of one.

Neutron: The Future Looks Cosmic
--------------------------------
It's still early in the cycle now, but we're already seeing [some](https://git.openstack.org/cgit/stackforge/networking-odl/)
[stackforge](https://git.openstack.org/cgit/stackforge/networking-vsphere/)
[projects](https://git.openstack.org/cgit/stackforge/vmware-nsx/) created by plugin owners. I'm excited at what the future
holds for all of this development. This will allow us to continue evolving and scaling the Neutron community. As with
any change such as this, there will be some churn initially. But as I continually say, one thing that impress me about
the OpenStack community is it's ability to constantly adapt. This is one such example of that in Neutron.

I'm proud to be not only the Neutron Project's PTL, but also a Neutron core team member and an OpenStack ATC. By working
together upstream as a community, and focusing on driving innovation in cloud networking, we've built an amazing piece of
technology. Enabling the development of this technology to grow as the Neutron project grows will be key to it's continued success.
Both the Services Split and Plugin Decomposition will allow this to happen.

I'll have more to say on this once we release
Kilo next spring.

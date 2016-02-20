+++
Description = "Running Openstack and OVN in Vagrant"
author = "mestery"
categories = ["OpenStack", "OVN", "Open vSwitch", "Vagrant"]
date = "2016-02-20T15:06:39-06:00"
socialsharing = true
tags = ["OpenStack", "OVN"]
title = "Running Openstack and OVN in Vagrant"
url = ""

+++

[OVN][1] has been evolving a lot since it was announced over a year ago. The
project is being developed by many developers from VMware, Red Hat, IBM, eBay
and other companies and individuals. If you haven't had a chance to give it a
try, recent work in the [networking-ovn][2] project has resulted in fairly
complex and [realistic deployment topology][3] using [Vagrant][4]. I encourage
you to have a look at the reference architecture referenced above, it's very
realistic and has come from actual production deployments of OVN with
OpenStack.

OVN With Vagrant
----------------

Looking at the [Vagrant][4] setup with OVN, you can see that we deploy for
nodes:

* A database node which runs ovn-northd the NB and SB databases. Eventually
  these will be separate ovsdb-server processes once [this patch][5] merges.
* A controller node for running the OpenStack control plane.
* Two compute nodes running nova compute and ovn-controller.

This is a fairly realistic deployment topology and allows for some realistic
testing in a Vagrant environment. We will even support live migration once
[this patch][6] merges.

Give OVN a Try!
---------------

If you haven't tried OVN with OpenStack yet, go ahead and clone the
[networking-ovn][7] repository and spin-up our Vagrant! If you hit any
issues, find us on #openstack-neutron-ovn on Freenode, or use the [Open
vSwitch mailing list][8] or [OpenStack dev mailing list][9].

[1]: http://networkheresy.com/2015/01/13/ovn-bringing-native-virtual-networking-to-ovs/
[2]: https://launchpad.net/networking-ovn
[3]: http://docs.openstack.org/developer/networking-ovn/refarch.html
[4]: https://github.com/openstack/networking-ovn/tree/master/vagrant
[5]: https://patchwork.ozlabs.org/patch/584834/
[6]: https://review.openstack.org/#/c/280728/
[7]: http://git.openstack.org/cgit/openstack/networking-ovn/
[8]: http://mail.openvswitch.org/mailman/listinfo/dev
[9]: http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack-dev

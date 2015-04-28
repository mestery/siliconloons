+++
Description = "Subnetpools in Neutron"
author = "mestery"
categories = ["OpenStack", "Neutron", "networking"]
date = "2015-04-28T08:41:34-05:00"
socialsharing = true
tags = ["OpenStack", "Neutron", "networking"]
title = "Subnetpools in Neutron"
url = ""

+++

One of the most interesting new features in Neutron for the Kilo release is
the addition of [subnetpools][1] to the API. This work was initially targeted
to integrate nicely with [pluggable IPAM][2]. Unfortunately, this did not
make it into Kilo and is targeted at Liberty. But even without pluggable IPAM
as a consumer, the subnetpools addition is quite useful. Here's an example
of how you might use it.

> neutron net-create webapp  
> neutron subnetpool-create --default-prefixlen 24 --pool-prefix 10.10.0.0/16 webpool  
> neutron subnet-create --subnetpool webpool websubnet  

What I've shown above is the creation of a network, pool, and subnet for an
example web application. The subnetpool was created with a default prefix
length of /24. Thus, when the user creates the subnet 'websubnet', it will
end up with a CIDR such as "10.10.0.0/24".

Creating another subnet from the pool will result in the allocation code
selecting another range:

> neutron subnet-create --subnetpool webpool dbsubnet  

This would result in the subnet 'dbsubnet' having a CIDR of "10.10.1.0/24".

As you can see, the subnetpool code is really powerful because it removes the
need for a user to have to select a CIDR. An admin could create a shared
subnetpool with a large block of addresses and let tenants create subnets
from that. It's a powerful addition to the Neutron API, and will integrate
nicely with the pluggable IPAM addition we expect to land during Liberty.

[1]: http://specs.openstack.org/openstack/neutron-specs/specs/kilo/subnet-allocation.html
[2]: http://specs.openstack.org/openstack/neutron-specs/specs/liberty/neutron-ipam.html

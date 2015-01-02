+++
Description = "An arm based cloud"
author = "mestery"
categories = ["OpenStack", "Cloud Computing"]
date = "2015-01-02T14:42:18-06:00"
socialsharing = true
tags = ["OpenStack", "ARM", "Open Source", "Cloud"]
title = "Test Driving an ARM-based Cloud"
url = ""

+++
By now, most people have probably heard about French telecom Iliad's
[plans](http://venturebeat.com/2014/12/29/why-french-telecom-iliad-is-launching-an-arm-based-cloud-service-and-why-it-matters/)
to build a cloud running servers using [ARM chips](http://en.wikipedia.org/wiki/ARM_architecture). It's an interesting twist on the typical
cloud setup for a few different reasons. Most clouds run on [Intel X86](http://en.wikipedia.org/wiki/X86) processors.  Iliad's cloud
will utilize ARM-based chips in lieu of the X86 processors most public and private clouds use. Will this attract mobile developers,
as Iliad hopes? Time will tell. But thanks to a contact at Iliad, I was lucky enough to be given a test drive of this ARM powered
cloud. My thoughts are below.

An ARM Powered Cloud
--------------------
The dashboard for the online.net cloud is fairly straightforward, and is similar to other cloud dashboards.

<img src="http://blog.siliconloons.com/blog_images/online_net_dashboard.png" alt="Online.net Dashboard" style="width: 600px;">

Creating a new instance is straight forward. You're presented with a single instance type (C1) for now.

<img src="http://blog.siliconloons.com/blog_images/create_instance_1.png" alt="Server Type" style="width: 600px;">

Online.net provides some good image choices.

<img src="http://blog.siliconloons.com/blog_images/create_instance_2.png" alt="Image Choices" style="width: 600px;">

The last step is to add a volume.

<img src="http://blog.siliconloons.com/blog_images/create_instance_3.png" alt="Volume Selection" style="width: 600px;">

Once you've done this, you'll see your instance running. In the example below, I have two instances running.

<img src="http://blog.siliconloons.com/blog_images/online_net_servers.png" alt="Volume Selection" style="width: 600px;">

All of this is fairly straightforward. Online.net provides some impressive [documentation](https://doc.cloud.online.net/),
as well as a great [community forum](https://community.cloud.online.net/) for collaboration with other online.net cloud
users. The APIs for the cloud are great as well, I'm guessing someone will integrate this with vagrant fairly quickly.

What About OpenStack?
---------------------
Since I typically work on OpenStack, I wanted to try and run devstack on my C1 cloud instance. The good news is this
worked out great! Note, I had to utilize the Ubuntu 14.10 Utopic image, as the Trusty one failed as it can't find the
'python-guestfs' package, which nova requires. With Utopic, I had to run devstack with "FORCE=yes" since Utopic isn't
officially supported yet. But it worked! I added the following to my local.conf to make it work with Neutron and to
ensure I had ARM capable Cirros images:

```
IPSEC_PACKAGE=ike
CIRROS_ARCH=arm
```

Conclusions
-----------
An ARM-based cloud is an interesting option. I'm excited to see online.net offering this. It's going to be fun
to see them roll it out for general availability during 2015.

---
author: mestery
Description: "Cloud-Native NFV: Where Art Thou?"
socialsharing: true
url: ""
categories:
  - Open Source
  - Service Mesh
  - Networking
tags:
  - Open Source
  - Service Mesh
  - Networking
title: "Cloud-Native NFV: Where Art Thou?"
date: 2018-06-06T11:54:36-05:00
draft: true
---

<p style="text-align:center;">
<img class="special-img-class" style="width: 500px" title="O Brother, Where Art Thou?" src="/whereartthou.jpg" />
</p>

Cloud-native is the future of application development. It's the latest trend
in the technology industry, moving application developers towards a future
where applications are developed natively using modern methodlogies and
technologies. From a methodology perspective, this includes utilizing agile
development, which shifts the cultural aspects of an engineering organization.
From a technology perspective, this means using public and private clouds, as
well as being API-driven in your development. Pivotal [describes cloud-native
as the following][2]:

> Cloud-native is an approach to building and running applications that exploits
> the advantages of the cloud computing model. 

In another corner of the technology world exists something called [Network
Function Virtualization][3], or as it's typically known, NFV. NFV is built
around the idea that service providers in the communications space can take
advantage of virtualization technologies. Instead of having to deploy physical
appliances for network services, they can instead deploy virtual machine images
of these appliances on commodity hardware. It's a huge shift for the service
provider industry.

As the world has moved forward with cloud-native development, NFV has just
caught up with the world of virtualization. All of those advantages of
cloud-native look pretty appealing to the NFV industry. It's inevitable that
the NFV and service provider industry would want to take advantage of what
cloud-native can provide, and in fact this is exactly what is beginning to
happen.

As these worlds collide, there is a disconnect around how the cloud-native world
has been building technology and what the service provider's interested in
extending NFV want to do. From a networking perspective, cloud-native has been
focused up the stack. In a typical [OSI model][1], this has meant focusing on
Layer 4 (Transport layer) and Layer 7 (Application layer). Service providers
looking to take advantage of NFV are focused more on Layer 2 (Data link layer)
and Layer 3 (Network layer).

<p style="text-align:center;">
<img class="special-img-class" style="width: 800px" title="O Brother, Where Art Thou?" src="/nfv-problem.png" />
</p>

This discrepancy has resulted in some difficult discussions between the two
camps. Kubernetes, the leader in container orchestration, and thus the leader
in cloud-native orchestration, has been loathe to integrate support for L2
and L3 networking. And rightfully so. Base Kubernetes was not designed for
this. Further, the concepts of NFV are not cloud-native by default, and come
from the virtualization view of the world. Objects like "ports", "subnets",
and "networks" have no place in a cloud-native world. Something has to give,
as the systems are not compatible.

But what if there was a way to build a trully cloud-native NFV platform,
something which could support cloud-native functions (CNFs) natively? Given
how extensible Kubernetes is with [custom resource definitions][5], this is
not only possible, it's being developed and worked on today. This project is
called [Network Service Mesh][4]. This project is an attempt to reimagine
NFV in a cloud-native way.

The image below shows the core concepts in Network Service Mesh. Note that the idea here is to abstract this into higher-level concepts which help to move NFV into it's inevitable cloud-native future.

<p style="text-align:center;">
<img class="special-img-class" style="width: 800px" title="O Brother, Where Art Thou?" src="/networkservicemesh-abstractions.png" />
</p>

In future posts, I will go into some detail on Network Service Mesh. It's
very early in it's development lifecycle, but it's been exciting to see the
interest in this from both the Kubernetes community as well as the service
provider NFV community.

_Note: Pictures borrowed from the great presentation given to the Kubernetes Network SIG by Ed Warnicke found [here][6]._

[1]: https://en.wikipedia.org/wiki/OSI_model
[2]: https://pivotal.io/de/cloud-native
[3]: https://en.wikipedia.org/wiki/Network_function_virtualization
[4]: https://github.com/ligato/networkservicemesh
[5]: https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions
[6]: https://docs.google.com/presentation/d/1vmN5EevNccel6Wt8KgmkXhAfnjIli4IbjskezQjyfUE/edit?usp=sharing
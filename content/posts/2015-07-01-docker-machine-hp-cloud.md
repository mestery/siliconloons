+++
Description = "Running Docker Machine on HP Helion Public Cloud"
author = "mestery"
categories = ["Docker", "OpenStack", "Cloud", "Containers"]
date = "2015-07-01T20:29:30-05:00"
socialsharing = true
tags = ["Docker", "OpenStack", "Cloud", "Containers"]
title = "Running Docker Machine on HP Helion Public Cloud"
url = ""

+++

Brent Salisbury, otherwise known as [networkstatic][5], has been doing an
amazing job writing articles on how to run [Docker Machine][6] on various
cloud platforms. He's written about running it on [Microsoft Azure][1],
[Amazon Web Services][2], [Rackspace Public Cloud][3], and [Digital Ocean][4].
He's done an amazing job showing you how you can utilize Docker Machine with
an existing cloud platform to experiment with Docker and even use it in
production running in VMs on public clouds.

Given that Docker Machine supports so many different cloud platform, I thought
I'd help to continue his series and show you how to use Docker Machine with the
[HP Helion Public Cloud][7]. Since the HP Helion Public Cloud is based on
[OpenStack][8], the Docker Machine driver for OpenStack works quite nicely here.
Lets dive in and see how to configure this up.

HP Helion Public Cloud
----------------------
For those interested in following along, you can sign up for a free HP Helion
Public Cloud account and get a credit by using the link [here][9]. Use this to
get access so you can spin up your own instances here. Once you do that,
you can then login and create VMs and try out Docker Machine as below.

Using Docker Machine With HP Helion Public Cloud
------------------------------------------------
There are a few things you'll need to grab before you create your VMs using
Docker Machine:

1. Image Name
2. Flavor Name
3. Tenant ID
4. Auth URL
5. Endpoint Type
6. Region
7. Floating IP Pool
8. Username
9. Password
10. ssh-user

You can acquire this information from the admin panel of your HP Helion Public
Cloud account. Once you have it all, it's a simple matter of adding it to the
commandline of the docker-machine command you run. An example is shown below:

```
mestery$ docker-machine create \
     --driver openstack \
     --openstack-image-name "Ubuntu Server 14.04.1 LTS (amd64 20140927) - Partner Image" \
     --openstack-flavor-name standard.xsmall \
     --openstack-tenant-id <tenant ID> \
     --openstack-auth-url https://region-a.geo-1.identity.hpcloudsvc.com:35357/v2.0/ \
     --openstack-endpoint-type publicURL \
     --openstack-region "region-a.geo-1" \
     --openstack-floatingip-pool Ext-Net \
     --openstack-username <username> \
     --openstack-password <password> \
     --openstack-ssh-user ubuntu \
     test-machine
```

As you can see, we're creating a machine using an extra small flavor with an
Ubuntu 14.04.1 LTS image. You'll want to fill in the details around tenant ID,
username, and password here.

Some Potential Gotchas
----------------------
Note that docker-machine will use port 2376 to communicate with the docker
daemon running on the VM in the HP Helion Public Cloud. To enable this access
remotely, you'll need to add a security group rule to allow this.

Another thing to note is that if you end up reusing the same floating IP across
a few instances, the step where docker-machine logs into the guest and sets up
docker will fail. It's best to ensure the fingerprint for an older host which
was previously using that floating IP is no longer in your ~/.ssh/known_hosts
file.

Using Docker
------------
Now that we've created the virtual machine, lets eval the new host:

```
mestery$ eval "$(docker-machine env docker1)"
```

And for kicks, lets just verify nothing is running on the host:

```
mestery$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
mestery$ 
```

Lets follow some simple examples from [networkstatic][10] and try a few things
out. First, lets just run a simple docker image with busybox and print out
something interesting:

```
mestery$ docker run busybox echo networkstatic is awesome
Unable to find image 'busybox:latest' locally
latest: Pulling from busybox

cf2616975b4a: Pull complete 
6ce2e90b0bc7: Pull complete 
8c2e06607696: Already exists 
busybox:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.

Digest: sha256:38a203e1986cf79639cfb9b2e1d6e773de84002feea2d4eb006b52004ee8502d
Status: Downloaded newer image for busybox:latest
networkstatic is awesome
mestery$ 
```

Pretty cool, right? Now, lets run something a bit more useful:

```
mestery$ docker run -d -p 8000:80 nginx
```

We'll need to add a security group rule to allow port 8000 in so we can get
access to our new nginx container running on this VM in the HP Helion Public
Cloud. Once we do, lets run a curl command to see what's there:

```
mestery$ curl $(docker-machine ip test-machine):8000
```

And you should see something like this:

```
<title>Welcome to nginx!</title>
```

Closing Thoughts
----------------
Docker Machine is a pretty cool tool to explore Docker with. Thanks to
Brent for inspiring me to take a peek at this and how it runs on the HP
Helion Public Cloud! I encourage everyone to give Docker Machine a try on
your public cloud of choice and get familiar with docker and containers.

[1]: http://networkstatic.net/using-docker-machine-to-provision-on-microsoft-azure/
[2]: http://networkstatic.net/docker-machine-provisioning-on-aws/
[3]: http://networkstatic.net/running-docker-machine-on-rackspace-public-cloud/
[4]: http://networkstatic.net/running-docker-machine-on-digital-ocean/ 
[5]: https://twitter.com/networkstatic
[6]: https://github.com/docker/machine
[7]: http://www.hpcloud.com/
[8]: http://www.openstack.org/
[9]: http://www.hpcloud.com/cloud-credit
[10]: http://networkstatic.net/

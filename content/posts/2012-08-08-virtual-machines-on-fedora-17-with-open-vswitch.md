---
title: Virtual Machines on Fedora 17 with Open vSwitch
author: mestery
date: 2012-08-08
url: /virtual-machines-on-fedora-17-with-open-vswitch/
socialsharing: true
tmac_last_id:
  - 544156008399273984
categories:
  - Infrastructure
tags:
  - Fedora
  - KVM
  - libvirt
  - Linux
  - Open vSwitch
  - Virtualization
---
My <a title="Fedora 17 with Open vSwitch" href="http://www.siliconloons.com/?p=239" target="_blank">previous blog post</a> showed you how to setup Open vSwitch (including LACP port-channels) on your Fedora 17 host. Once you have this working, creating virtual machines and adding them to one of your Open vSwitch bridges is the next logical step. For this setup, we will make use of <a title="libvirt" href="http://www.libvirt.org/" target="_blank">libvirt</a> to manage our virtual machines. We&#8217;ll utilize virt-manager (a GUI) and virsh (a CLI) to manage the VMs on the host. But the VMs themselves, once running on Fedora with libvirt and KVM, can easily be migrated into an oVirt setup, for instance. Perhaps a later post will detail how to go about the process of importing them into oVirt.

## The Setup

I&#8217;ll be using a single host running Fedora 17 for this example. The host is running Open vSwitch for virtual networking as well. To make things a bit more complicated, I&#8217;ll also convert a virtual machine from a VMW vmdk format into a libvirt format. This will at least show a partial migration path from VMW hosted virtual machines to Fedora+KVM hosted virtual machines.

Make sure you have the appropriate software installed on your Fedora host. For this, the below command should get you going:

<pre>yum install libvirt qemu virt-manager</pre>

Now, make sure libvirt is started, and also starts at system boot time:

<pre>systemctl start libvirtd.service
systemctl enable libvirtd.service</pre>

## The Process

The first step is to migrate your disk format. For this, I created a directory for my virtual machines (/home/images), and a subdirectory under there for my test virtual machine (fedora17). I copied my existing VMware virtual machine over in that directory, and it looks like this:

<pre>[root@ucs-3 images]# ls
fedora.17.x86-64.20120529.vmdk  fedora.17.x86-64.20120529.vmx
[root@ucs-3 images]#</pre>

The next step is to convert this image into a format which libvirt will understand. I will utilize qemu-img for this, executing the command as below:

<pre>qemu-img convert fedora.17.x86-64.20120529.vmdk fedora17.img</pre>

qemu-img has a lot of options, but the above will perform a basic conversion. The end result is we now have an image suitable for import into libvirt. At this point, we can bring up virt-manager and create our virtual machine. Once you start virt-manager, you should see a simple image like below:

<div id="attachment_284" style="width: 571px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.31.59-AM.png"><img class="size-full wp-image-284" title="virt-manager" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.31.59-AM.png" alt="" width="561" height="577" /></a>
  
  <p class="wp-caption-text">
    virt-manager start screen
  </p>
</div>

We can now start the process of adding our virtual machine. Below are screen shots which show the process.

<div id="attachment_287" style="width: 494px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.39.02-AM.png"><img class="size-full wp-image-287" title="Step1" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.39.02-AM.png" alt="" width="484" height="380" /></a>
  
  <p class="wp-caption-text">
    Step 1
  </p>
</div>

<div id="attachment_288" style="width: 495px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.41.29-AM.png"><img class="size-full wp-image-288" title="Step 2" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.41.29-AM.png" alt="" width="485" height="386" /></a>
  
  <p class="wp-caption-text">
    Step 2
  </p>
</div>

<div id="attachment_289" style="width: 495px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.42.38-AM.png"><img class="size-full wp-image-289" title="Step 3" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.42.38-AM.png" alt="" width="485" height="387" /></a>
  
  <p class="wp-caption-text">
    Step 3
  </p>
</div>

<div id="attachment_290" style="width: 495px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.44.53-AM.png"><img class="size-full wp-image-290" title="Step 4" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.44.53-AM.png" alt="" width="485" height="512" /></a>
  
  <p class="wp-caption-text">
    Step 4
  </p>
</div>

At this point, your VM will show up in virt-manager:

<div id="attachment_291" style="width: 570px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.46.29-AM.png"><img class="size-full wp-image-291" title="VM Imported" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.46.29-AM.png" alt="" width="560" height="576" /></a>
  
  <p class="wp-caption-text">
    Virtual Machine imported in virt-manager
  </p>
</div>

## Virtual Machine Networking

The next step is to configure the virtual machine networking. We want to utilize libvirt&#8217;s integration with Open vSwitch for this next part, so we&#8217;ll utilize virsh (the CLI) to do this. Fire up virsh now in another window:

<pre>[root@ucs-3 images]# virsh 
Welcome to virsh, the virtualization interactive terminal.

Type:  'help' for help with commands
       'quit' to quit

virsh #</pre>

We will want to list the virtual machines, and then edit the XML definition for the virtual machine we just created with virt-manager.

<pre>virsh # list --all
Id Name State
----------------------------------------------------
- Fedora17 shut off

virsh #</pre>

Now run the &#8220;edit&#8221; command, passing the VM name from above. We will want to scroll down to the networking section, which will look something like the below:

<div id="attachment_292" style="width: 670px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.52.48-AM.png"><img class="size-full wp-image-292" title="Interface pre-OVS" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-9.52.48-AM.png" alt="" width="660" height="92" /></a>
  
  <p class="wp-caption-text">
    Network section pre-OVS
  </p>
</div>

Change it to look like the below, substituting the name of your OVS bridge for &#8220;source bridge&#8221; below:

<div id="attachment_293" style="width: 671px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-10.09.39-AM.png"><img class="size-full wp-image-293" title="Network config with OVS" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-10.09.39-AM.png" alt="" width="661" height="122" /></a>
  
  <p class="wp-caption-text">
    Network configuration with OVS
  </p>
</div>

Once you complete this, you will notice if you do a &#8220;dumpxml <VM name>&#8221; that libvirt has automatically added an interfaceid to the parameter section of the virtualport section of the XML. See the picture below.

<div id="attachment_295" style="width: 670px" class="wp-caption alignnone">
  <a href="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-10.13.44-AM.png"><img class="size-full wp-image-295" title="Complete OVS network config" src="http://www.siliconloons.com/wp-content/uploads/2012/08/Screen-Shot-2012-08-08-at-10.13.44-AM.png" alt="" width="660" height="160" /></a>
  
  <p class="wp-caption-text">
    Final libvirt OVS network configuration
  </p>
</div>

At this point, your VM should be all set to fire up and utilize Open vSwitch for virtual networking.

## Caveats

There are a few issues with the above. For one, libvirt only allows setting of 2 parameters in the &#8220;virtalport&#8221; section of the XML: interfaceid and profileid. This means you cannot set a VLAN tag, for instance. However, what this does mean is that by utilizing a profileid, you could take advantage of having all your configuration tied to the profile. This is how advanced networking technologies such as 802.1QBh work.

## Conclusion

Hopefully you now have your virtual machine up and running with a combination of Fedora, libvirt, KVM, and Open vSwitch. Future posts will likely show you how to integrate the above with oVirt for a nice, datacenter virtualization management solution which is fully open source.

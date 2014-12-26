---
title: Open Source Cloud and Virtualization Terminology for VMware Users
author: mestery
date: 2011-12-15
url: /open-source-cloud-and-virtualization-terminology-for-vmware-users/
socialsharing: true
tmac_last_id:
  - 544156014732664832
categories:
  - Open Source
tags:
  - Aeolus
  - Cloud
  - KVM
  - Open vSwitch
  - OpenFlow
  - OpenStack
  - oVirt
  - Virtualization
  - VMware
  - Xen
---
Recently, as I was talking to a friend about OpenStack, oVirt, and other Open Source Cloud and Virtualization technologies, he stopped me and had me back up. This friend has a strong background in VMware technologies, but not so much with their Open Source counterparts. It occurred to me there are others who may be coming from the same VMware background, thus I decided to create a handy cheat sheet for folks new to Open Source Cloud and Virtualization technologies who have a VMware background.

And with that, I present the cheat sheet below:

  * <a title="KVM" href="http://www.linux-kvm.org/page/Main_Page" target="_blank">KVM</a>: KVM is a hypervisor integrated into and utilizing the Linux Kernel. **Comparable VMware technology: The ESXi vmkernel**
  * <a title="Xen" href="http://xen.org/" target="_blank">Xen</a>: Xen is another hypervisor integrated in the Linux kernel. **Comparable VMware technology: The ESXi vmkernel**
  * <a title="Qemu" href="http://wiki.qemu.org/Main_Page" target="_blank">Qemu</a>: A generic Open Source machine emulator and virtualizer. KVM uses this as the virtual machine monitor for running virtual machines. **Comparable VMware technology: ESX virtual machine monitor**
  * <a title="oVirt" href="http://ovirt.org/" target="_blank">oVirt</a>: oVirt is a complete and comprehensive infrastructure and management virtualization platform for the data center. **Comparable VMware technology: vSphere**
  * <a title="ovirt-node" href="http://ovirt.org/wiki/Node" target="_blank">ovirt-node</a>: ovirt-node is a small footprint Linux distribution, running the KVM hypervisor. **Comparable VMware technology: ESXi**
  * <a title="Aeolus" href="http://aeolusproject.org/" target="_blank">Aeolus</a>: Aeolus is a management platform for running virtual machines both in your own datacenter, as well as in a public cloud. **Comparable VMware technology: vCloud Director**
  * <a title="OpenStack" href="http://www.openstack.org/" target="_blank">OpenStack</a>: OpenStack, per the website, &#8220;delivers a massively scalable cloud operating system.&#8221; For the most part, OpenStack itself compares favorably to a vCloud Director setup. **Comparable VMware technology: vCloud Director**
  * <a title="OpenStack Nova" href="http://openstack.org/projects/compute/" target="_blank">OpenStack Nova</a>: Nova is the compute manager for OpenStack. It handles spinning VMs up, bringing them down, and managing resources of the compute nodes. **Comparable VMware technology: Functionality in vCenter**
  * <a title="OpenStack Swift" href="http://openstack.org/projects/storage/" target="_blank">OpenStack Swift</a>: Swift is an object storage system for OpenStack. **Comparable VMware technology: VMFS (to some extent)**
  * <a title="OpenStack Glance" href="http://openstack.org/projects/image-service/" target="_blank">OpenStack Glance</a>: Glance provides virtual machine image management for OpenStack. **Comparable VMware technology: Functionality in vCloud Director**
  * <a title="OpenStack Keystone" href="http://keystone.openstack.org/" target="_blank">OpenStack Keystone</a>: Keystone is an identity management system providing uniform authentication across OpenStack. **Comparable VMware technology: Functionality in vCenter**
  * <a title="Horizon" href="http://wiki.openstack.org/OpenStackDashboard" target="_blank">OpenStack Horizon</a>: Horizon is a GUI designed to allow administrators to work with OpenStack in a self service portal. **Comparable VMware technology: Parts of vCloud Director**
  * <a title="OpenStack Quantum" href="http://wiki.openstack.org/Quantum" target="_blank">OpenStack Quantum</a>: Quantum is a service providing the ability to provision and manage networks in OpenStack. **Comparable VMware technology: Features found in vSphere/vCloud Director**
  * <a title="Open vSwitch" href="http://www.openvswitch.org/" target="_blank">Open vSwitch</a>: Open vSwitch is an open source virtual switch, which can run inside the Linux kernel and work with both KVM and Xen. **Comparable VMware technology: VMware vDS and Cisco Nexus 1000V**
  * <a title="OpenFlow" href="http://www.openflow.org/" target="_blank">OpenFlow</a>**: **While not technically an Open Source project, OpenFlow is essentially an Open Source networking protocol. **Comparable VMware technology: Nothing currently**

<div>
  Hopefully the list above is a good comparison for people new to Open Source Cloud and Virtualization solutions coming from a VMware background.
</div>

---
title: The latest libvirt release is out!
author: mestery
date: 2012-08-31
url: /the-latest-libvirt-release-is-out/
socialsharing: true
tmac_last_id:
  - 544156007845203968
categories:
  - Open Source
tags:
  - libvirt
  - Linux
  - Open vSwitch
  - Programming
  - Virtualization
---
If you read the <a title="libvirt mailing lists" href="http://libvirt.org/contact.html#email" target="_blank">libvirt development mailing list</a>, you will have noticed that libvirt released 2 versions this week, the latest of which is version <a title="Libvirt 0.10.1 released" href="https://www.redhat.com/archives/libvir-list/2012-August/msg02028.html" target="_blank">0.10.1</a>. This version includes a bunch of bug fixes, but between this and the previous 0.10.0, there are some changes in how you work with Open vSwitch virtualport types. I thought I&#8217;d explain some of them here, as they are advantageous and will make deploying libvirt with Open vSwitch easier.

## VLAN Changes

The most important change going into this release of libvirt was around the handling of VLANs, both for Open vSwitch networks, as well as for 802.1Qbg and 802.1Qbh networks. The changes allow you to specify VLANs on networks, portgroups, or as part of the interface definition in the domain XML. For this article, I wanted to focus on, specifically, how this affects the integration of Open vSwitch with libvirt.

For example, to setup a VLAN in a network definition, you would do something like this:

<pre>&lt;network&gt;
  &lt;name&gt;openvswitch-net&lt;/name&gt;
  &lt;uuid&gt;81ff0d90-c92e-6742-64da-4a736edb9a8b&lt;/uuid&gt;
  &lt;forward mode='bridge'/&gt;
  &lt;virtualport type='openvswitch'/&gt;
  &lt;portgroup name='bob' default='yes'&gt;
    &lt;vlan trunk='yes'&gt;
      &lt;tag id='666'/&gt;
    &lt;/vlan&gt;
    &lt;virtualport&gt;
      &lt;parameters profileid='bob-profile'/&gt;
    &lt;/virtualport&gt;
 &lt;/portgroup&gt;
 &lt;portgroup name='alice'&gt;
    &lt;vlan trunk='yes'&gt;
       &lt;tag id='777'/&gt;
       &lt;tag id='888'/&gt;
       &lt;tag id='999'/&gt;
    &lt;/vlan&gt;
    &lt;virtualport&gt;
       &lt;parameters profileid='alice-profile'/&gt;
    &lt;/virtualport&gt;
  &lt;/portgroup&gt;
&lt;/network&gt;</pre>

As you can see from the above, we are creating a network (named &#8220;openvswitch-net&#8221;), and creating 2 portgroup&#8217;s here: &#8220;bob&#8221; and &#8220;alice&#8221;. Each portrgoup has a VLAN trunk defined, although &#8220;bob&#8221; only has a single VLAN in the trunk.

Now, if we wanted to put this configuration directly on the interface itself, it would look liks this:

<pre>&lt;interface type='network'&gt;
  &lt;mac address='00:11:22:33:44:55'/&gt;
  &lt;source network='ovs-net'/&gt;
  &lt;virtualport type='openvswitch'&gt;
    &lt;parameters interfaceid='09b11c53-8b5c-4eeb-8f00-d84eaa0aaa4f' profileid='bob'/&gt;
  &lt;/virtualport&gt;
&lt;/interface&gt;</pre>

Now, because we specified the profileid of &#8220;bob&#8221;, the VLAN trunk information for &#8220;bob&#8221; would be applied when this VM is booted up and it&#8217;s VIF is added to the OVS bridge. But what if we wanted to override this information in the interface definition itself? We can do that too, and here&#8217;s an example of how to do it:

<pre>&lt;interface type='network'&gt;
  &lt;mac address='00:11:22:33:44:55'/&gt;
  &lt;source network='ovs-net'/&gt;
  &lt;vlan trunk='yes'&gt;
    &lt;tag id='42'/&gt;
    &lt;tag id='48'/&gt;
    &lt;tag id='456'/&gt;
  &lt;/vlan&gt;
  &lt;virtualport type='openvswitch'&gt;
    &lt;parameters interfaceid='09b11c53-8b5c-4eeb-8f00-d84eaa0aaa4f' profileid='bob'/&gt;
  &lt;/virtualport&gt;
&lt;/interface&gt;</pre>

Now when this virtual machine is booted, the configuration on the &#8220;interface&#8221; will take precedence, and the virtual machine will have a trunk port with VLANs 42, 48, and 456 passed to it.

## Under the Covers

How does all of this work under the covers? We simply pass additional parameters to &#8220;ovs-vsctl&#8221; to ensure the port is trunked (trunk=VLAN1,VLAN2) or setup as an access port (tag=VLAN1). This is added to the command line libvirt uses when adding these ports to the OVS bridge.

## Conclusion

If you have read my <a title="Configuring Virtual Machines with OVS and libvirt" href="http://www.siliconloons.com/?p=277" target="_blank">previous article</a> on configuring virtual machines with libvirt and Open Vswitch, you will note a caveat there around VLAN configuration. I&#8217;m happy to say this latest version of libvirt addresses this issue. You can now effectively setup VLAN configuration for virtual ports connecting to an OVS bridge in multiple places in libvirt. This makes deploying libvirt with Open vSwitch much more useful.

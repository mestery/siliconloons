---
title: OpFlex Is Not An OpenFlow Killer
author: mestery
date: 2014-04-04
url: /opflex-is-not-an-sdn-killer/
socialsharing: true
tmac_last_id:
  - 544155997401776128
categories:
  - Open Source
  - OpFLEX
tags:
  - Open Source
  - Open vSwitch
  - OpFlex
---
There has been a flurry of press around <a title="OpFlex" href="http://blogs.cisco.com/datacenter/introducing-opflex-a-new-standards-based-protocol-for-application-centric-infrastructure/" target="_blank">Cisco&#8217;s release of OpF<span style="text-decoration: underline;">lex</span></a>. If you want the nitty gritty details, please read the IETF draft available <a title="OpFLEX IETF Draft" href="http://tools.ietf.org/html/draft-smith-opflex-00" target="_blank">here</a>. What exactly is OpFlex? The IETF draft sums it up nicely:

<p style="padding-left: 30px;">
  <em>The OpFlex architecture provides a distributed control system based on a declarative policy information model. The policies are defined at a logically centralized policy repository (PR) and enforced within a set of distributed policy elements (PE). The PR communicates with the subordinate PEs using the OpFlex Control protocol. This protocol allows for bidirectional communication of policy, events, statistics, and faults.</em>
</p>

It&#8217;s clear that Cisco intends to make OpFlex an open standard together with it&#8217;s partners in the vendor, provider and Open Source communities. We&#8217;re working hard to make that a reality. On the Open Source front, I&#8217;m leading a team of people who are working hard on the code around this new OpFlex Policy Agent. We intend to fully Open Source the OpFlex Policy Agent under the <a title="Apache 2.0 License" href="http://www.apache.org/licenses/LICENSE-2.0.html" target="_blank">Apache 2.0 license</a>. We&#8217;re excited to build an Open Community around this work, and in the coming months we&#8217;ll be looking to get more companies and individuals involved as we move this out into the Open. As you can imagine, starting an Open Source project from scratch takes time and planning, and we&#8217;re doing our best on all of these fronts.

## What Exactly Is OpFlex?

<span style="line-height: 1.5em;">So, now that you know what OpFlex is, what exactly is it not? Well, if you&#8217;ve read the article </span><a style="line-height: 1.5em;" title="OpFlex is an SDN killer" href="http://www.networkworld.com/news/2014/040214-cisco-openflow-280282.html" target="_blank">here</a><span style="line-height: 1.5em;">, you may think it&#8217;s a, quote, &#8220;OpenFlow Killer.&#8221; Well a headline such as this may make for good SEO, it&#8217;s not true. OpFlex is meant to be embedded in the device or host via the Policy Agent. This could be a virtual switch such as Open vSwitch, a whitebox switch, a load balancer, a firewall, or any other element which can enforce policy. To show how this all fits together, the following diagram can be used:</span>

<pre>+––––––––––––––+                                
|              |                                
|  Policy      |                                
|  Authority   |                                
|              |                                
|              |                                
|              |                                
+––––––+–––––––+                                
       |                                        
       | Policy                                 
       | Messaging                              
       |                                        
       |                                        
+––––––+–––––––+                   +––––––––––––––+
|              |                   |              |
| OpFlex       |                   |  Host or     |
| Policy       +––––––––––––––––---+  Device      |
| Agent        |  Device           |              |
|              |  Programmability  |              |
|              |  Functions        |              |
+––––––––––––––+                   +––––––––––––––+</pre>

As you can see from the diagram, the key pieces of OpFlex are the Policy Authority and the Policy Agent. Policies defined in the Policy Authority are resolved asynchronously by the Policy Agent. The policies are then rendered in the system specific implementation into the programmability functions provided by the device or system. Examples of programmability functions could be the OpenFlow and OVSDB protocols supported by Open vSwitch, APIs provided by Arista&#8217;s EOS, the onePK APIs supported on Cisco gear, or even a CLI interface to a firewall device. OpFlex doesn&#8217;t replace the programmability mechanisms provided by the system, it works in tandem with them to enforce the policy. This is the key piece which many have missed.

## In Conclusion

We&#8217;re excited about the potential of OpFlex and the Policy Agent. OpFlex is not meant to replace Open vSwitch, nor any other host or system programmability layer. Open vSwitch is a great Open Source project for which Cisco is a contributor. We plan to continue working closely with the Open vSwitch community, as well as projects such as OpenCompute, OpenDaylight, and the ONF. And just as these are all vibrant Open Source projects and communities, we hope to get the OpFlex Policy Agent into a similar state over the coming months and build a community for people who want to enable Open Source policy.

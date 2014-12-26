---
title: Moving a Cisco NSSxxx from Cisco Firmware to Qnap Firmware
author: mestery
date: 2012-01-04
url: /moving-a-cisco-nssxxx-from-cisco-firmware-to-qnap-firmware/
socialsharing: true
tmac_last_id:
  - 544156015395348480
categories:
  - Tech Gear
tags:
  - Cisco
  - NAS
  - Qnap
---
So, Cisco (disclaimer: I work at Cisco, although not in the group working on the NSSxxx products) has recently decided to stop selling their Qnap OEM&#8217;d NAS devices. See the link <a title="Cisco NSSxxx End-of-Sale and End-of-Life" href="http://www.cisco.com/en/US/prod/collateral/ps4159/ps9954/ps10817/end_of_life_notice_c51-685438.html" target="_blank">here</a>. For those of us who have one of these in our labs (I have a NSS326 myself), this means no more firmware updates from Cisco. But, the latest firmware for these devices from Cisco (version 1.5, Release Notes PDF <a title="NSSxxx Firmware 1.5 Release Notes" href="http://www.cisco.com/en/US/docs/storage/nass/csbcdp/smart_storage/open_source/78_20467_01.pdf" target="_blank">here</a>) does allow for users to migrate from Cisco firmware to the stock Qnap firmware. So, how easy of a process is this? I was able to do this myself, I thought I would document the steps for others to follow here.

  1. You may want to backup your data first. I did not do this, but depending on how important your data is, it&#8217;s wise to consider this step.
  2. First, acquire the NSS 1.5 firmware from cisco.com. Once you have that, go ahead and load this onto your NSSxxx device and reboot.
  3. Once the device is running 1.5, go ahead and download the latest Qnap firmware for your device (link <a title="Qnap Cisco NSSxxx firmware" href="http://www.qnap.com/cisco" target="_blank">here</a>).
  4. Load the Qnap firmware onto your device, and reboot.
  5. You should now be running the stock Qnap firmware for your OEM&#8217;d Cisco NSSxxx device.

<div>
  One of the main advantages of this transition is that the Qnap firmware supports Time Machine with OSX Lion, whereas the Cisco firmware does not. If you are running Macs in your lab, business, or home, this is reason enough to migrate to the Qnap firmware. Qnap will also continue to support software updates on the Cisco NSSxxx, so this is another good reason to migrate.
</div>



<div>
  One issue I did hit when migrating was that I had ssh access enabled on my Cisco, but when I moved to Qnap, the default ssh worked, but only allowed a single ssh login at a time. I migrated to OpenSSH by following the instructions <a title="How To Replace SSH DAemon with OpenSSH" href="http://wiki.qnap.com/wiki/How_To_Replace_SSH_Daemon_With_OpenSSH" target="_blank">here</a>. This worked well, and allows me to have multiple ssh sessions going to the Cisco NSSxxx.
</div>

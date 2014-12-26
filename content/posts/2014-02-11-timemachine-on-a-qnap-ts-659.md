---
title: TimeMachine on a QNAP TS-659
author: mestery
date: 2014-02-11
url: /timemachine-on-a-qnap-ts-659/
socialsharing: true
tmac_last_id:
  - 544155999725031424
categories:
  - Mac
tags:
  - Backup
  - Mac
  - TimeMachine
---
For the last few months, TimeMachine has been failing for me between my Macs and a QNAP TS-659 NAS I have. The NAS is running firmware 4.0.3, and I would consistently get the error &#8220;Cannot connect&#8221; when trying to connect. I was able to work around this with the following command run manually:

<pre>sudo tmutil setdestination -ap afp://TimeMachine@192.168.64.38/TMBackup</pre>

Running that in a terminal window allowed me to then use the GUI to select that disk for backups and things started rolling again. In the above, make sure to replace &#8220;192.168.64.38&#8221; with your IP or hostname of the QNAP. It will ask you for your password when you run the command. I found all of this on the forum thread <a title="Forum Thread" href="http://forum.qnap.com/viewtopic.php?f=15&t=85065" target="_blank">here</a> for reference.

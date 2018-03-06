---
author: mestery
Description: "Creating a Custom Launchd Plist File"
socialsharing: true
url: ""
categories:
  - launchd
  - Hacking
  - Apple
tags:
  - launchd
  - Hacking
  - Apple
title: "Creating a Custom Launchd Plist File"
date: 2018-03-06T13:22:09-06:00
---

I recently had the need to have a program run every time my Mac was booted. In
this particular case, I'm using an old Mac Mini to host a variety of things
around the house, among them it runs [homebridge][1] with the
[Broadlink RM plugin][2] to control a [Broadlink RM Pro][3] device. The
Broadlink RM Pro uses WiFi to receive commands from Homekit, and controls my
20+ year old receiver. I'll write more about this setup in the future, but
for now, lets focus on using launchd to automatically run the homebridge
node.js application.

For starters, I wanted to run the homebridge application at each boot. This
is a simple application which can be installed with homebrew, and is run
from the command line as `/usr/local/bin/homebridge`. Easy, right? After
some digging through [man pages][4] and reading some [helpful post][5] I
found online, I came up with the below as my plist file:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>org.mestery.homebridge</string>

    <key>UserName</key>
    <string>mestery</string>

    <key>GroupName</key>
    <string>admin</string>

    <key>Program</key>
    <string>/usr/local/bin/homebridge</string>

    <key>RunAtLoad</key>
    <true/>

    <key>EnvironmentVariables</key>
    <dict>
           <key>PATH</key>
           <string>/usr/local/bin</string>
    </dict>

    <key>KeepAlive</key>
    <true/>

    <key>StandardOutPath</key>
    <string>/tmp/homebridge-mestery.log</string>
    <key>StandardErrorPath</key>
    <string>/tmp/homebridge-mestery.log</string>
</dict>
</plist>
```

I created the above file, made it owned by root and in the wheel group, and
moved it to `/Library/LaunchDaemons/org.mestery.homebridge.plist`. Some
notes on it's contents:

* UserName and GroupName are fairly obvious.
* Program references the name of the program you're going to run.
* RunAtLoad is do you want this run when you load the plist file.
* I needed to set PATH so it included /usr/local/bin and code find
  node.js, which is where the EnvironmentVariables section comes
  into play.
* KeepAlive tells launchd to restart homebridge if it exits for some reason.
* StandardOutPath and StandardErrorPath are used to track output from the
  homebridge program.

This works nicely, and homebridge does now indeed start when I reboot my Mac
Mini. I'll write more about [homebridge][1] in a future post.

[1]: https://github.com/nfarina/homebridge
[2]: https://github.com/lprhodes/homebridge-broadlink-rm
[3]: https://www.amazon.com/BroadLink-Automation-Universal-Compatible-Smartphone/dp/B01GIXZDKO
[4]: https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man5/launchd.plist.5.html#//apple_ref/doc/man/5/launchd.plist
[5]: https://serverfault.com/questions/111391/use-an-environment-variable-in-a-launchd-script

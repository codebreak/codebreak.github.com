---
layout: post
title: "Intel HAXM"
date: 2013-03-29 15:09
comments: false
categories: 
---
One of the biggest pains that I found when I started learning how to build android apps was waiting for the emulator to Launch and startup. Luckily, after having tweeted:

>> "This #android #emulator sure takes it's time to load. Wish there was some sort of progress bar to indicate that it's not stuck or hanging."


android sdk

installing HAXM

To verify that Intel HAXM is running, open a terminal window and execute the following command:
1
kextstat | grep intel
If Intel HAXM is operating correctly, the command will show a status message indicating that the kernel extension named “com.intel.kext.intelhaxm” is loaded.

To stop or start Intel HAXM, use the following commands:

Stop:

1
sudo kextunload –b com.intel.kext.intelhaxm

Start:
view sourceprint?
1
sudo kextload –b com.intel.kext.intelhaxm

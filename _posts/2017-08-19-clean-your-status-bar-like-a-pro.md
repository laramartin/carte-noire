---
layout:     post
title:      Clean your status bar like a pro!
date:       2017-06-28 00:00
author:     Lara Martín
summary:    Improve your screenshots in an automated way
categories: android
tags:
  - Android
  - Android Dev
  - Software Development
  - Android App Dev
---

We developers need to take screenshots of our apps sometimes: either for the Google Play Store or to show off on our open source projects. Like everyone else, the status bar of our devices may be crammed with notifications, low battery indicator and not so healthy hours 😉.

![Messy status bar](https://thepracticaldev.s3.amazonaws.com/i/ih1d6szdxmgmnrifhd6d.png)

Your potential user can be distracted by the icons in the status bar and in the worst case it will give the impression you're not careful about your product and not professional.

Until now, every time I needed to take screenshots I used an app called [Clean Status Bar](https://github.com/emmaguy/clean-status-bar) that draws a fake status bar on top of the real one. That allowed me to hide my notifications to show a neutral time and a fully charged phone. I only had to open the app, choose the icons I wanted to display, give it a background color, and that was it! My status bar looked nice for the screenshots!

But I faced a problem. At work we have a script to generate screenshots in different emulators, but we didn't have a way to make the status bar look good automatically every time we needed.

I found the [Demo Mode for Android](https://android.googlesource.com/platform/frameworks/base/+/master/packages/SystemUI/docs/demo_mode.md), which forces the status bar to look on a given way with the aim of taking screenshots. So here I explain how I use it.


## How to use Demo Mode

You need to run these commands from the terminal, so you need `adb` access to the device.

First you enable the Demo Mode:
```
adb shell settings put global sysui_demo_allowed 1
```

Second you enter the commands to display or hide icons on the status bar. The ones I like to use are:

```
// display time 12:00
adb shell am broadcast -a com.android.systemui.demo -e command clock -e hhmm 1200

// Display full mobile data without type
adb shell am broadcast -a com.android.systemui.demo -e command network -e mobile show -e level 4 -e datatype false

// Hide notifications
adb shell am broadcast -a com.android.systemui.demo -e command notifications -e visible false

// Show full battery but not in charging state
adb shell am broadcast -a com.android.systemui.demo -e command battery -e plugged false -e level 100
```

This is how it looks like after running the commands:

![Clean status bar](https://thepracticaldev.s3.amazonaws.com/i/4wgyo0lf2jqatqd9qz5d.png)

Now you can take the screenshots you need, but do not forget to exit the Demo Mode at the end:
```
adb shell am broadcast -a com.android.systemui.demo -e command exit
```

The list of available commands can be found here:

https://android.googlesource.com/platform/frameworks/base/+/master/packages/SystemUI/docs/demo_mode.md

You now have no excuse to not have nicer screenshots! I continue using Emma’s app for my personal projects, but if you need to automate your screenshots, this is a must do.

[Read it in my medium blog.](https://android.jlelse.eu/clean-your-status-bar-like-a-pro-76c89a1e2c2f)

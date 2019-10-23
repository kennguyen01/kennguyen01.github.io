---
title: Frustrating Blue Screens
date: 2019-10-21
categories: rants
---

<p align="center">
  <img alt="Windows 10 logo" src="https://i.imgur.com/QHpoN9w.jpg">
</p>

It's a regular Tuesday night. I came back from work, had dinner, and watched some YouTube videos to pass the time. Then all of a sudden, the screen went black and this message popped up:

> :( Your PC ran into a problem and needs to restart. We're just collecting some error info, and then we'll restart for you.

> If you'd like to know more, you can search online later for this error: DRIVER_IRQL_NOT_LESS_OR_EQUAL

<!--more-->

I watched helplessly as the progress percentage slowly counts up to 100. The computer restarted and I was back to the login screen. Not really sure what happened, I searched online for what the error message means. Some possible causes are corrupted system files, hardware issues, and corrupted device drivers. I needed to know exactly what causes it.

## A Driver Problem

So I downloaded [BlueScreenView](https://www.nirsoft.net/utils/blue_screen_view.html) to read the dump file. Sure enough, the program highlighted **atikmdag.sys** in red. A quick search revealed that it's a driver associated with ATI Radeon Family. The two AMD products I have in my computer are the CPU and the graphics card. The only program from AMD that I use and update regularly is the Radeon Graphics software. I looked around in different forums and turned out this is a common issue with people who have an AMD graphics card and use the software.

Since it's a driver issue relating to my graphics card, I used [DDU](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html) to uninstall all the drivers from my system. Then I downloaded a fresh version of the software directly from AMD website. My system seemed to be working normally after the clean install so I went to sleep.

## A Consistent Issue

The next day I turned on my computer and go about my business. Then a few hours after I got another BSOD. This was getting really annoying so I decided to just bite the bullet and transfer all my important files into an external hard drive and reinstalled Windows. During the installation process, I was really thankful of whoever invented SSD.

Back when HDD was the only thing I had, reinstalling Windows means waiting a very long time for the installation and then download any programs I need afterward. The whole thing would take at least a few hours. With SSD, installing Windows took about 20 minutes and downloading programs probably another 30 minutes. I was back up and running in less than an hour.

With this, I prayed my trouble is past.

Not even two hours later, the ominous blue screen came back. Three blue screens in just a span of days and they happened even more frequently now. Some people online suggested that it might just be a RAM problem. I didn't think it was likely but I had to try. I downloaded [MemTest86](https://www.memtest86.com/) and booted my computer from the flash drive. I let the test ran the whole night and there was no issue. At least now I know my RAM is functioning perfectly.

## Ubuntu to the Rescue

<p align="center">
  <img alt="Ubuntu logo" src="https://i.imgur.com/NgiNGqE.png">
</p>

At this point, I just wanted an OS that works. The main reason why I stuck with Windows on my desktop is because of games. No other system can compare to Windows in term of game choices. Any well known game publisher will always release a Windows version for their games. However, if I can't even use my computer, there's no point for me to even think about gaming.

With Linux the only viable alternative, I chose Ubuntu. It's the first Linux distro that I used and the one I'm most comfortable with. The process was painless. Most of the programs I had on Windows were open source so there was no issue getting them on Ubuntu. It was actually even easier since using command lines to install packages are much more efficient than downloading an .exe file and go through the install wizard.

That was more than a couple months ago since I got Ubuntu and everything is running great so far. Sometimes I missed playing games but having a stable system is much more valuable for me.

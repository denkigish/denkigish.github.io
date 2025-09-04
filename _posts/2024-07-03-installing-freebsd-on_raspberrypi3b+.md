---
layout: post
title:  "Installing FreeBSD on Raspberry Pi 3B+"
date:   2024-07-04 18:16:56 -0500
categories: FreeBSD Adventures
---
The following assumes some familiarity with the command line or terminal, in linux, or macOS. If you have none, you can refer to [Ubuntu’s tutorial](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview) or to [Apple’s](https://support.apple.com/guide/terminal/get-started-pht23b129fed/2.14/mac/14.0).

So, for this I am using a Mac running Mac OS 14.5 Sonoma. The instructions are pretty similar for any Mac. You can accomplish similar on Linux or Windows. Start by going to the [FreeBSD website](https://www.freebsd.org/). While there you can download the image file for an SD Card. Click on the “Download FreeBSD” link, and browse the page looking for the FreeBSD release you want to try. I chose FreeBSD 14.1, and I looked for the SD Image. FreeBSD for RPI at this time is only available as an image file for an SD card. For the Raspberry PI 3B+ you want to. choose the aarch64 build, and select the RPI (3/4) link. In the following file download page, you want to select ” FreeBSD-14.0-RELEASE-arm64-aarch64-RPI.img.xz”. This file will not need to be uncompressed. Verify you chose the right image file, as you want to install it to the right board.

Once you have the file downloaded you can use any disk imager for the Raspberry Pi. Since I already had Balena Etcher installed, I went ahead and used this to image my SD card. You can download Balena from their [page](https://etcher.balena.io/). Balena guides you through the steps once it is installed. You select the drive/ SD card you wish to use for the install media, you then choose the image file you wish to install. Then you flash the image to the SD card. This installs FreeBSD to your SD card, in its entirety. You will be prompted for your admin user name, to erase the SD card contents and replace its contents with the FreeBSD image.

From here it is straight-forward to just take the imaged SD card and plug it in to the SD card slot on your Raspberry Pi. Boot your Raspberry Pi, and if connected to a keyboard, mouse and terminal, you will have a fully functional FreeBSD installation on Raspberry Pi. This is the recommended method for installing FreeBSD on the RPI. However, if you don’t have an extra keyboard, monitor and mouse. You can SSH into your RPI right away. You will need the ip address of your RPI, and that can be found using your router, or another client computer on your network using [Fing](https://www.fing.com/), or other network inspection software. The RPI has 2 accounts natively setup, the “root” account, and the “freebsd” account. The root account does not have the ssh server active, for security reasons, but it is an admin account that you can use to install software packages. The freebsd account does have an ssh server enabled, but is not an administrative account. The native account have a default password of “root” and “freebsd” corresponding to their account name. To login to the RPI you simply type the following command into the terminal:

```
ssh freebsd@<ip_address> 
e.g.
ssh freebsd@192.168.1.200 
```
This calls the “ssh” command, and tells it the user is freebsd and the computer you want to log into can be found at ip address 192.168.1.200. The terminal will prompt you to enter your password, which on a new machine is “freebsd”. I will leave this as the password until this raspberry pi is completely setup.

After booting up, or logging in your terminal will look something like this.

```
Last login: Thu Jul  4 12:30:59 2024 from studio.attlocal.net
FreeBSD 14.0-RELEASE (GENERIC) #0 releng/14.0-n265380-f9716eee8ab4: Fri Nov 10 08:59:18 UTC 2023
Welcome to FreeBSD!
Release Notes, Errata: https://www.FreeBSD.org/releases/
Security Advisories:   https://www.FreeBSD.org/security/
FreeBSD Handbook:      https://www.FreeBSD.org/handbook/
FreeBSD FAQ:           https://www.FreeBSD.org/faq/
Questions List:        https://www.FreeBSD.org/lists/questions/
FreeBSD Forums:        https://forums.FreeBSD.org/
Documents installed with the system are in the /usr/local/share/doc/freebsd/
directory, or can be installed later with:  pkg install en-freebsd-doc
For other languages, replace "en" with a language code like de or fr.
Show the version of FreeBSD installed:  freebsd-version ; uname -a
Please include that output and any error messages when posting questions.
Introduction to manual pages:  man man
FreeBSD directory layout:      man hier
To change this login announcement, see motd(5).
%
```
You are logged as user “freebsd” if you need to login to root to install applications or need admin rights, you can do so by typing “su” after the command prompt “%”.

```
% su
```
The “su” stands for super user, and will log you into a session of the root user. You can exit from the new session by typing the exit command following the new command prompt “#”. The command prompts are different because the root and freebsd accounts use different shells. However that is more detail than you need right now. Just recognize the different prompts. Notice you are back to the “%” command prompt. I point these out because these prompts aren not consistent with Linus or other BSD’s. Therefore you might not understand what is going on.

```
% su
Password:
# exit
%
```
At this point you have successfully installed the FreeBSD OS on your Raspberry Pi. However, while it has the bare necessities, you may want to install some software packages to get more use out of it.

## Time Zone setup and Sync – Updated 12/28/24

At this point, you want to make sure that you run bsdconfig to setup your timezone. If you don’t do this, your install will not install any software because its clock is not correct.
```
# bsdconfig
```
You need to run bsdconfig and select the timezones menu, and follow the prompt to select your timezone, then you need to sync your clock with the internet time servers.
```
ntpd -qg  # Sync time with NTP
```
Upon completion of syncing your time you can confirm your time is correct by using the date command.
```
# date
Sat Dec 28 15:21:01 CST 2024
```
Your date should be synced up. You can now continue
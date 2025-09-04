---
layout: post
title:  "Installing FreeBSD Software Packages."
date:   2024-07-07 18:16:56 -0500
categories: FreeBSD Adventures
---
Once you have installed FreeBSD I would suggest installing the software you will need to use it. This varies by person, and part of the appeal of FreeBSD especially for the Raspberry Pi, is that you don’t have someone else’s idea of what you need installed. For example, the OS does include vim as a text editor, but it doesn’t also include other text editors. So I need to install “nano” if I want to use it. For my purposes, I want some basic things installed to make my life a little easier. I will not cover how to install each package. If the package requies additional configuration, it will be discussed in separate articles. Eventually, I will install the following, but will start with nano and sudo first:

* Nano – text editor
* sudo – command to grant temporary admin rights.
* XFCE – desktop environment
* LightDM – graphical Login Manager
* tiger-vnc-server – VNC server for remote access.
* Zsh – Z shell
* pyenv – python package manager

Freebsd has ports and packages. My understanding of ports is code that is ready to download and compile. Packages are binary packages / compiled programs ready to be installed. I prefer packages, because ports honestly intimidate me. Some day I will venture into ports, but that day is not today.

## Install Nano – text editor

To install a package such as “nano”. You need 2 things administrative access, and you need to call the package command and say install “nano”. First you must access the root account which has administrative access, to install a package. To do so, after the command prompt ‘%” type su and hit <Enter> key. The su command stands for super user. After clicking enter you will be prompted for a password. Enter your root password and hit the <Enter> key, as a default on the Raspberry Pi install, the password is “root”. Note: the password, will not be displayed when you type it in. Upon successfully entering the password your prompt changes to the ‘#”. An example of how to do this follows:

```
% su
Password:
#
```
Once in the root account, you use the pkg command, with the install argument and package name argument. It will search the packages available, and if found will display the package and ask if you wish to proceed installing it. Type “y” for “yes” and when you return to the command prompt the process is complete. This looks like:

```
# pkg install nano
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
The following 1 package(s) will be affected (of 0 checked):
New packages to be INSTALLED:
	nano: 7.2_1
Number of packages to be installed: 1
The process will require 3 MiB more space.
649 KiB to be downloaded.
Proceed with this action? [y/N]: y
[1/1] Fetching nano-7.2_1.pkg: 100%  649 KiB 664.6kB/s    00:01
Checking integrity... done (0 conflicting)
[1/1] Installing nano-7.2_1...
[1/1] Extracting nano-7.2_1: 100%
#
```

The installation of nano was done to make the next step easier. I don’t know the vim commands and don’t really feel the need to learn it for casual computing. However, to make administering this computer easier, I want to install the sudo command. The sudo command is used to grant the user, temporary admin rights, without logging into an administrative account. If you want to find out about sudo, you can of course read about it on its webpage.

## Install sudo

To install the sudo package on FreeBSD you simply do the following at the command root command prompt. You should still be logged into the root account from earlier, if not you can repeat the earlier step of logging into the super user account.

```
# pkg install sudo
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
The following 1 package(s) will be affected (of 0 checked):
New packages to be INSTALLED:
	sudo: 1.9.15p5_4
Number of packages to be installed: 1
The process will require 8 MiB more space.
2 MiB to be downloaded.
Proceed with this action? [y/N]: y
[1/1] Fetching sudo-1.9.15p5_4.pkg: 100%    2 MiB   1.8MB/s    00:01
Checking integrity... done (0 conflicting)
[1/1] Installing sudo-1.9.15p5_4...
[1/1] Extracting sudo-1.9.15p5_4: 100%
#
```
Unfortunately sudo needs a little setup before it can be used. A freshly installed sudo will only allow the root user to use sudo, everyone else will receive a warning. In order to address this we must edit the sudoers file. This is a configuration file that tells sudo who is allowed to use the sudo command. You can edit the file by using nano, and providing the path to the sudoers file to nano. It is possible that the sudoers file to be edited is located at /etc/sudoers instead.

```
#nano /usr/local/etc/sudoers.d/adminuser
```

The nano editor will update the command line. In the header row, it will show that you are running nano and what version, followed by the path and name of the file you are editing. On the footer rows, it will show the commands. The “^” character stands for the CTRL key, and the capital letter stands for the letter to type to execute the command identified to the right. Therefore ^G Help will get the help screen. Below is the blank sudoers file.

```
GNU nano 7.2 /usr/local/etc/sudoers.d/adminuser Modified 
^G Help      ^O Write Out ^W Where Is  ^K Cut       ^T Execute
^X Exit      ^R Read File ^\ Replace   ^U Paste     ^J Justify
```

I can add a group of users, or I can add an individual user to the file. You must remember that the files are executed from top to bottom, so the last modification will apply. In this case, I will not do anything fancy, and will give the freebsd all sudoer rights. If there are entries, you would add this at the bottom, on a blank row.

```
<username or group> ALL=(ALL) ALL 
```
In our case we want to add freebsd and also the wheel group of users. So the following is entered into the file.

```
GNU nano 7.2 /usr/local/etc/sudoers.d/adminuser Modified %wheel ALL=(ALL) ALL
freebsd ALL=(ALL) ALL

 
^G Help      ^O Write Out ^W Where Is  ^K Cut       ^T Execute
^X Exit      ^R Read File ^\ Replace   ^U Paste     ^J Justify
```
```
GNU nano 7.2 /usr/local/etc/sudoers.d/adminuser Modified %wheel ALL=(ALL) ALL
freebsd ALL=(ALL) ALL

 
Save modified buffer?
 Y Yes
 N No           ^C Cancel
 ```
 
The next step is to save the file, this is done by the ^X Exit command. When you type in CTRL+X the display updates asking if you want to save the modified buffer. This is nano’s way of asking if you want to save the file. Type y for yes, and you are returned to the command line. Now you can use sudo on the freebsd account. To return to the freebsd account and its command prompt , when you are in the su session , just type in exit and enter. This will return you to the freebsd account.

```
# exit
%
```
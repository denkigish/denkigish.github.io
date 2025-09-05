---
layout: post
title:  "Raspberry Pi 3B+ and FreeBSD!"
date:   2024-07-02 18:16:56 -0500
categories: FreeBSD Adventures
---
Why am I doing this.

When I was going to community college, I remember asking a professor what I should do to get into this thing called open source software, and he suggested getting into Linux. I was fascinated by computers, but knew practically nothing at all. The teacher referred me to the gnu/linux webpage, and I took a look, and decided I was way out of my depth. Fast forward a few years and I was using Solaris in college, with very limited training, still no linux. However after graduating I decided to make the jump to Mac OSX. From 2003 onward I have been using OSX for my personal computing, and of course I learned more about the terminal commands over time.

So During the pandemic, I started my data analytics journey. DeVry made me take an introductor course on the Internet of Things (IoT). I didn’t complain too much since it was required, and it was essentially a lab course using an Arduino. This made me start looking at the Raspberry Pi (RPI)that I had heard a lot about. Finally I took a jump and got the biggest RPI I could, which at that time was a 3B+ with 4GB of ram. I used it to learn the Linux terminal, in my class, but haven’t really used it too much. Since Linux is a “UNIX” clone, I wanted to get as close to true “UNIX” as I could. I also had some experience with the different ways of doing things for each Linux Distribution, and didn’t want many ways but really just a single way to do things. So I took the plunge of using FreeBSD, because as full OS, as long as it was FreeBSD the instructions should be consistent. There may be more than one way to peel a mango in FreeBSD, but they are all FreeBSD’s way of peeling a mango.

I also have a bunch of software packages that I want to learn, but I don’t necessarily want to clutter up my daily driver with all those experiments. Some might say, install Docker, or use VM’s and I have considered it, and briefly tried it. It is still a piece of software I don’t want on my personal machine. So that is why I now have 2 Raspberry Pi’s. On one I just have a clean Raspberry Pi OS installation, which I share with my son’s so they can learn to program python. On the other, I have chosen to install FreeBSD. My plans are to learn jails on FreeBSD to install mongo, sql, and a git server to start with.

Before we dive into installing and setting up FreeBSD on the RPI. I do have to say the following. It is not necessarily easy finding instructions on how to setup FreeBSD software packages. However, it is not impossible. Part of the reason for this, is that instructions for Linux will populate your web search, and while similar they are not the same . What has impressed me the most, is just how responsive FreeBSD is on the RPI, even compared to the RPI’s native OS distribution, Raspbarry Pi OS. It starts fast, and even with a desktop environment it is responsive. Will I use an RPI 3B+ as a daily driver? No, I have a daily driver for that, but I don’t think I will complain using it to learn software packages on.

I began my FreeBSD learning journey on [RobNuggie’s YouTube Channel](https://www.youtube.com/@RoboNuggie). I have also referenced The FreeBSD Handbook, as well as reading the book [Absolute FreeBSD by Michael Lucas](https://nostarch.com/absfreebsd3#updates).

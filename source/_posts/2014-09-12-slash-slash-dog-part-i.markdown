---
layout: post
title: "//DOG Part I"
date: 2014-09-12 22:44:49 -0400
comments: true
categories: [media server, unRAID, how-to, guide, dog, part I]
---

So I’ve always been meaning to write up a guide/how-to/personal journal of how I built and setup my very own personal home media server. The following is meant to be both a memoir as an easy to follow guide that should spell out the process itself and hopefully help others avoid some of the pitfalls that I struggled through (and eventually triumphed over). There is SO much to cover, so I’ll be breaking this out into a multi-part series  – and off we go!
 
A Growing Problem
=================
 
I found myself stuck in a recurring cycle. I would buy a new external hard drive and fill it up over time but inevitably, I’d start running out of space and need to buy another one with a larger capacity. And every time I’d have to go through the painful process of scrubbing and copying all of my data from the old drive to the new drive. It is never fun having to decide “do I really need all 139 episodes of MacGyver?” (of course, the answer to that question is always “Yes”). But if I wanted to completely backup the new, and largest capacity, drive, I had to spread the backup across multiple lower capacity drives. This process was not only prohibitively expensive; it only provided me with a single back-up as of a particular point in time. 
 
Of course, living in a small apartment means that my coffee table also does double-duty as my desk which meant there was no easy way for me to access any of the drives on a regular basis since I’d have to get the hard drive out and set it up with my laptop every time I wanted to get to any of the data.
 
Clearly I needed a better solution so I started researching the various options out there for backing up, accessing, and streaming my data.
 
Requirements
============
 
I quickly learned that choosing the right backup solution totally depends on your individual needs. My key requirements for this project can be summarized as follows:
 
* Must be expandable. Adding additional capacity down the road should be relatively painless.
* Must be remotely accessible. I want to be able to stream data to PCs on my local wireless network, an existing small form factor HTPC, and a rasberri pi.  Mobile streaming is a bonus but wasn’t an absolute must-have.
* Must automatically provide data redundancy (i.e. backup!).
* Must be able to incorporate all, or at least some, of my existing HDDs
* Low-Cost: I wasn’t looking to break the bank
 
To RAID? Or not to RAID (unRAID)?
---------------------------------
 
You may have heard of RAID (Redundant Array of Inexpensive or Independent Disks) which, put simply, is a technology used to combine multiple drives into a logical unit for storing data. Depending on the type of RAID implementation there are different benefits and drawbacks, be it speed, space, redundancy, etc. which for the purposes of this post I won’t delve too deep into. But for my needs, I found that a “spinoff” of RAID, appropriately named unRAID, seemed to be the best of all worlds.
 
What is unRAID exactly and why should I care? Well, [this website](http://lime-technology.com/technology/) does a pretty good job of explaining it but the most important benefits over traditional RAID is that it was specifically designed for storing digital media. It would allow me to easily store and share data across a network while protecting it at the same time. unRAID also would allow me to reuse the hard drives I already own (mixing and matching), add capacity as I need it, and automatically has redundancy, or as unRAID refers to it, “Parity” built right in. It really seemed like I found…  **The PERFECT SOLUTION!**
 
So, having chosen my RAID implementation of choice, my next move was to pick out the hardware…
 
The little server that could
============================
 
One of the best things about building an unRAID server is the optionality one has in terms of hardware choices. Being that unRAID is linux based, the hardware combinations that would work are truly endless – which might be kind of overwhelming. I wasn’t looking to buy and build a PC component by component so I started researching semi-complete server boxes that would run unRAID. Luckily, HP just happens to sell these pretty sweet little compact server boxes that can hold multiple drives. There were several posts on unRAID forums from users who had great success using them as media servers, and when I found one of them on sale through Newegg, I pounced. The specific model I chose was the N40L HP Microserver, with a 5-drive capacity (more than 5 drives can be squeezed in there too).
 
What I liked:

* Low power draw and very quiet
* Compact form factor
* CHEAP!
* Easy Access / Easy Drive Swapping
 
What I didn’t like:

* Relatively Low-Power CPU/GPU – Limits transcoding capability for Plex Purposes
* Requires some modification in order to fit 6 or more drives (although this is really the fun part J)
* Comes with a 250GB drive that I didn’t need
 
With this server, I knew I’d be able to have anywhere from 16TB all the way up to 20+ TB of available capacity (assuming 4TB drives). This would give me plenty of headroom for years to come – and as I mentioned earlier, unRAID makes increasing capacity very easy, so I could always upgrade to larger drives down the road.
 
As I said, you can certainly choose components piece by piece, but as far I was concerned, the microserver suited my needs just fine.  There were a few other items I needed to purchase before I could get started:
USB Key to store and run the actual unRAID software (Required)
5.25” Drive Bay for adding the 5th Drive (Optional)
eSATA to SATA cable for adding a 6th drive (Optional)
Small SSD to act as an App drive (Optional) – I’ll get into this later
 
With all of my purchases made, I was ready to roll. In part II of this guide, we'll get into the build and software configuration process.
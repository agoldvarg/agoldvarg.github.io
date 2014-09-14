---
layout: post
title: "// DOG Part I"
date: 2014-09-12 22:44:49 -0400
comments: true
categories: [media server, unRAID, how-to, guide, dog, part I]
---

So I’ve always been meaning to write up a guide about how I built and setup my very own personal home media server. The following is meant to be both a memoir and an easy to follow guide that should spell out the process itself and hopefully help others avoid some of the pitfalls that I struggled through but eventually triumphed over. There is SO much to cover, so I’ll be breaking this out into a multi-part series – and off we go!
 
A Growing Problem
-----------------
 
I found myself stuck in a recurring cycle. I would buy a new external hard drive and after a period of time, I’d inevitably start running out of space. My only option was to buy another one with a larger capacity. And every time I’d have to go through the painful process of scrubbing and copying all of my data from the old drive to the new drive. It's never fun having to decide “do I really need all 139 episodes of MacGyver?” (of course, the answer to that question is “Yes”). In order to backup the new, and largest capacity, drive I had to spread my files across multiple lower capacity drives. This process was not only prohibitively expensive; it left me with a point in time backup, as opposed to a live-backup.
 
Clearly I needed a better solution so I started researching the various options out there for backing up, accessing, and streaming my data.
 
Requirements
------------
 
I learned that choosing the right backup solution totally depends on one's individual needs. My requirements were as follows:
 
   * Must be expandable. Adding additional capacity down the road should be relatively painless.
   * Must be remotely accessible. I want to be able to stream data to PCs on my local wireless network, an existing small form factor HTPC, and a rasberri pi.  Mobile streaming is a bonus but wasn’t an absolute must-have.
   * Must automatically provide data redundancy (i.e. backup!).
   * Must be able to incorporate all, or at least some, of my existing HDDs
   * Low-Cost: I wasn't looking to break the bank
 
To RAID? Or not to RAID? *Or unRAID?*
-------------------------------------
 
You may already have heard of RAID (Redundant Array of Inexpensive or Independent Disks) which to put it simply is a technology for combining multiple drives into a logical unit for data storage. Depending on the type of RAID implementation there are different benefits and drawbacks: be it speed, space, security, etc. which for the purposes of this post I won't delve into. I found that a spin off of RAID, appropriately named unRAID, seemed to offer the best combination of features for my needs.
 
What is unRAID exactly and why should I care? Well, [this website](http://lime-technology.com/technology/) does a pretty good job of explaining it but unRAID was specifically designed for storing and serving digital media across a network while protecting it at the same time. unRAID also would allow me to reuse the hard drives I already own, add capacity as needed, automatically back up my data - unRAID calls this “Parity.” It really seemed like I found…  **THE ALMOST PERFECT SOLUTION!**
 
So having chosen my RAID implementation of choice my next move was to pick out the hardware…
 
The little server that could
----------------------------
 
One of the best things about building an unRAID server is the optionality one has in terms of hardware choices. Being that unRAID is Linux based, the hardware combinations one can use are nearly endless – which may seem kind of overwhelming at  first. In my case, I wasn’t looking to buy and build a PC component by component so I started researching semi-complete server boxes that would run unRAID. 

Luckily, HP just happens to sell these sweet little compact servers with multiple drive capacity. There were several posts on unRAID forums from users who had great success using them as media servers and when I found one of them on sale through Newegg, I pounced. The specific model was the N40L HP Microserver, with a 5-drive capacity (although more than 5 drives can be squeezed in there with a little creativity).
 
What I loved:

   * Low power draw and very quiet
   * Compact form factor
   * Easy Access / Easy Drive Swapping
   * CHEAP!
 
What I didn't love:

   * Low-Power CPU/GPU – Limits transcoding capability for Plex Purposes
 
The total storage capacity could go up to 20TB using 4TB individual drives. This would give me plenty of headroom for years to come – and as I mentioned earlier unRAID makes increasing capacity very easy so I could always upgrade to larger drives down the road.
 
Don't get me wrong, you can certainly choose components piece by piece but as far I was concerned the microserver suited my needs just fine.  There were a few other items I needed to purchase before I could get started:

   * USB Key to store and run the actual unRAID software (Required)
   * 5.25” Drive Bay for adding the 5th Drive (Optional)
   * eSATA to SATA cable for adding a 6th drive (Optional)
   * Small SSD to act as an App drive (Optional) – I’ll get into this later
 
With all of my purchases made, I was ready to roll. In part II of this guide, we'll get into the build and software configuration process.

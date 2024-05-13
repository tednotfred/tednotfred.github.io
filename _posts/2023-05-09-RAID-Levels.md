---
title: RAID Levels
layout: post
tags: [server]
---
## Common RAID Levels

![Raid Levels](/assets/RAID-10.png)


___
## ZERO


RAID 0, also known as a striped set or a striped volume, requires a minimum of two disks. The disks are merged into a single large volume where data is stored evenly across the number of disks in the array.


It is important to note that if this type of RAID consists of disks of different sizes, each will be limited to the smallest disk size in the setup. This means that an array composed of two disks, where one is 500 GB, and the other is 225 GB, actually has the capacity of 2 x 225 GB (or 450 GB in total).


RAID zero doesn’t offer redundancy. If a disk fails then the array will fail and data will likely be lost but, there can be significant speed benefits when retrieving data from this type of array.



___
## ONE


RAID 1, is an array consisting of at least two disks where the same data is stored on each to ensure redundancy. The most common use of RAID 1 is setting up a mirrored pair consisting of two disks in which the contents of the first disk is mirrored in the second. This is why such a configuration is also called mirroring.


This type of array offers at least some fault tolerance but none of the performance gains that RAID 0 can offer. It is however a very simple and reliable type RAID which can work in many server situations.


___
## FIVE


RAID 5, is considered the most secure and is probably the most common RAID implementation. It combines striping and parity to provide a fast and reliable setup. Such a configuration gives the user storage usability as with *RAID 1* and the performance efficiency of *RAID 0* .


This type of RAID requires at least three hard drives (and at most, 16). Data is divided into data strips and distributed across different disks in the array.


It is usually the most desirable type of RAID if you have the disks available.


___
## TEN
RAID 10, is part of a group called nested or hybrid RAID, which means it is a combination of two different RAID levels. In the case of RAID 10, the array combines level 1 mirroring and level 0 striping. This RAID array is also known as RAID 1+0.


RAID 10 uses logical mirroring to write the same data on two or more drives to provide redundancy. If one disk fails, there is a mirrored image of the data stored on another disk. Additionally, the array uses block-level striping to distribute chunks of data across different drives. This improves performance and read and write speed as the data is simultaneously accessed from multiple disks. It is essentially two RAID 0 arrays (for performance) which are mirrored like RAID1 (for redundancy).


To implement such a configuration, the array requires at least four drives, as well as a disk controller.


RAID 10 arrays can also be difficult to scale up later if needed.


___


:zap:  *RAID won’t replace backups.* You can easilly get into a situation where corrupted data has been perfectly replicated across the array.


*Ask me how I know this?*

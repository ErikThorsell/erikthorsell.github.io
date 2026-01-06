---
title: State of the Homelab 2026 (Servers edition)
---

_This post is long overdue, but I'm planning some upgrades for 2026 so I figured I'd document the setup that has been
serving me very well for the past 5 years._

> As my posts tend to be, this is another quite lengthy one. If you only care about my current setup, have a look at the
> [Current Setup](#current-setup) section.

# Background

Back in 2011 I bought my first NAS, a [Synology
DS213j](https://global.download.synology.com/download/Document/Hardware/DataSheet/DiskStation/13-year/DS213j/enu/Synology_DS213j_Data_Sheet_enu.pdf).
(This scrawny little machine is _still_ serving!) A couple of years later I built my first "home server" which mostly
just acted as a router. I did however host a ZNC Bouncer and an OpenVPN Server. (I had Gbit Internet and the little 2
core, Intel J CPU, actually managed to provide almost 500Mbit both ways over VPN!)

## One server to rule them all

The fall of 2014 I built my first _real_ server. The purpose was to supersede the Synology NAS and build something
reasonably "production grade". (Albeit, as a second year university student, I was not familiar with the concept of
_production grade_.) I did a lot of reading and listened to a lot of podcasts on the subject. At the time, I was a huge
fan of the various [Jupiter Broadcasting](https://www.jupiterbroadcasting.com/) shows. In particular, I found the [BSD
Now](https://www.bsdnow.tv/) podcast (then hosted by: [Allan Jude](http://www.allanjude.com)) very fascinating.
Persuaded by the BSD folks, I decided to go with FreeNAS (which would be renamed to [TrueNAS
Core](https://en.wikipedia.org/wiki/TrueNAS) in 2021) as my server OS.

## A change of philosophy

Back in 2014, I went all in on FreeNAS and BSD. I hosted a handful of applications in jails and struggled _a lot_ with
running Linux VM:s under FreeNAS to get Docker support. It worked, but it was not particularly pleasant. In 2016 the
woman who would become my wife moved to Sweden, and in with me, meaning I now had an additional issue: Another user, who
had uptime and availability expectations on the few services she enjoyed using (mostly Plex)... Safe to say, I was
becoming more and more frustrated with FreeNAS as an "application hosting OS".

About the same time as FreeNAS morphed into TrueNAS Core, I was really getting sick and tired of the poor Docker support
in FreeNAS. I was also pushing my little server to its limit compute-wise. So I pulled the peripherals out of my gaming
computer (running Ubuntu) and put it in the bookshelf next to the server. Since I had done a pretty good job creating
unique datasets for my various applications, exposing them as NFS shares and mounting them on the gaming computer was
not unbearably difficult.

Back then, I did this out of frustration and necessity. Today, I encourage everyone who wants to self-host to separate
_storage_ and _compute_. Doing so allows you to separate your concerns in a very nice way. You can use more purpose
built tools to solve your respective problems and you can dimension your hardware more appropriately. 

For instance, back in 2014 I ran FreeNAS on a USB drive (as was customary) but apart from doing two RMA:s on the PSU
(Silverstone sure had some issues with their early SFX units) and migrating to a boot SSD a couple of years later, I am
still using the same hardware today. When I hosted jails and VM:s under FreeNAS, my CPU and RAM utilisation would
frequently be at capacity. Now, more than 10 years later, only serving NFS shares, my storage server is barely breaking
a sweat.

> Maybe the most important thing is that you can -- if things really go south -- unplug and nuke your compute machine
without worrying about losing data!

# Current setup

With the background out of the way, you probably (hopefully) understand _why_ I have my homelab setup the way I do.
Let's have a look at what's actually running in there.

## Storage server

As mentioned earlier, my storage server has remained virtually unchanged for over 10 years. (I'm still running TrueNAS
Core though. I should really take the time to upgrade to Scale.) I am _extremely_ pleased with the Supermicro
motherboard. IPMI is excellent and the four core C3558 CPU is perfect for my workload. I also really like the
Silverstone case.

Parts:
* Case: [Silverstone DS380](https://www.silverstonetek.com/en/product/info/server-nas/DS380/)
* Motherboard w/ integrated CPU: [Supermicro A2SDi-4C-HLN4F](https://www.supermicro.com/en/products/motherboard/a2sdi-4c-hln4f)
* RAM: 2x 8GB Samsung DDR4 ECC REG @2400MHz
* Boot: 120GB SSD
* PSU: Silverstone SST-ST45SF-G 450W

Initially, for storage, I used 4x 3TB but back in 2020 I upgraded to 4x 8TB. I run four disks in Raid-Z2, which might be
a little bit unconventional, but with [ZFS vdev
expansion](https://www.truenas.com/docs/scale/scaletutorials/storage/managepoolsscale/#expanding-a-pool) being a
reasonably new thing, I'm looking forward to adding two more 8TB disks to my server in the near future.

### A note on data integrity

I frequently talk to people who ask for advice building their first server or NAS. One common question is that of ECC
memory: _Is it worth it?_

If you're building a computer box for storing data that is important to you, I believe you should do whatever you can to
protect that data.

* Setup your storage solution with parity to handle disk failures. They WILL happen![^disks]
* Use a file system that mitigates data corruption (such as ZFS).
* Use ECC memory to protect yourself from corruption when data is written from RAM to disk.
* Backup your data to a second physical location!

## Compute server

The Ubuntu gaming computer has been the work horse of my homelab for several years. After re-purposing it from gaming to
running Docker services, I sometimes contemplate replacing it with something more "server grade", but since all data I
care about lives on the TrueNAS machine I'm not too concerned.

Parts:
* Case: Fractal Design Era
* Motherboard: Gigabyte B450
* CPU: AMD Ryzen 5 3600 @3.6GHz
* GPU: Asus Radeon RX5500 XT 8GB
* RAM: 2x 16GB Corsair DDR4 @2666MHz
* PSU: EVGA SuperNOVA GM 450W

## How I run my services

I run all of my services as Docker containers, managed using Docker Compose.[^k8s] On the TrueNAS machine, I have one
ZFS Pool which is divided into several datasets. (I don't quite have a 1:1 mapping between dataset and service, but some
day I might take the time to fix that.) The various datasets are then exposed as NFS Shares and mounted on the Ubuntu
machine.

Some shares are mounted directly by Docker, such as my Nextcloud instance:

```yaml
volumes:
  files:
    driver_opts:
      type: "nfs"
      o: "addr=truenas.home.arpa,rw"
      device: ":/mnt/volume1/nextcloud"
```

whereas some less critical services use a common bind mount:

```yaml
services:
  frigate:
    volumes:
      - /mnt/container_volumes/frigate-runtime/:/media/frigate
```


> **Networking?**
>
> I have a quite elaborate network setup too. If you're interested in another post , shoot me an email!

<!-- --------------------------------------------------------------------------------------------------------------- -->
[^k8s]: Every now and then I contemplate migrating to Kubernetes. Maybe k3s? Maybe a single-node-cluster based on Talos?
    Maybe I should just go all in and buy three mini PC:s? But my current setup works and it works quite well, so I'm in
    no hurry.

[^disks]: I believe I have had four disk failures over the past 10 years. One WD Red (the old version, before there
         was a Pro variant) and three Toshiba N300s. The two 2TB WD Red disks I put in my DS213j are still going strong.
         I feel reckless even writing this though. I really need to replace that machine...


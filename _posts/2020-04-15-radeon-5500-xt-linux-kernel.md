---
title: Running Linux with RX Radeon 5500 XT
---

**TL;DR**

I have done the following, it is unclear to me exactly what is required. Maybe
one day I'll do a fresh install and try one thing at the time...

1) Use the latest Linux 5.5 Kernel. **DO NOT USE** 5.6.\*

2) Install the latest mesa drivers (added the kisak-mesa PPA and upgraded, I got
mesa 20.0.3)

3) Add all navi_14 binaries from
[linux-firmware](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/amdgpu)
to `/usr/lib/firmware/amdgpu/`.

4) Downloaded and installed Radeon Software for Linux 19.50 from
[AMD](https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux).

---

# Preamble

Last week I put together my first gaming PC in a decade. Hearing that AMD is the
new black, I decided to go for a red-team-build. My previous build was running a
Intel 2600k and a Nvidia GTX 580 (actually two, in SLI, but that never worked in
Linux), but my new build has a AMD Ryzen 5 3600 and a AMD Radeon RX 5500 XT.

Even though this is a gaming machine, running Linux was natural. I have been
using nothing but Linux and FreeBSD for the past 7 or 8 years, and I used to
game on the aforementioned desktop machine running Arch Linux. The plan for this
new machine, however, was that it should be wife-friendly and stable. So I opted
for Pop!_OS, because I heard it was good.

# The First Problem

 > Upon first boot, Pop!_OS only gave me one resolution option for my QHD
 > display: `1024x768`.

Ugh. Well, I looked around and soon realized that the Kernel that comes with
Pop!_OS (and Ubuntu 19.10, which Pop!_OS is built upon) was (probably) too old.
Nothing weird with that, the 5500 XT is a very new graphics card. Soooo, I off
to Kernel land it was. I downloaded the latest stable Linux Kernel (at the time
of writing this is 5.6.4) from the [Ubuntu
PPA](https://kernel.ubuntu.com/~kernel-ppa/mainline/) and installed it.

*For more info about how to install an additional Kernel, see my post on this
[HERE]({{site.url}}/_posts/2020-04-15-upgrade-linux-kernel.md).*

I rebooted the computer and voilà, glorious 2560x1440 pixels!

# The Second Problem

 > When launching a game (DotA 2) it became apparent that something was
 > still wrong. I literally had only 1Hz options in my graphics settings, and
 > the game updated ~1 FPS.

I checked `dmesg`, and surely -- an error message:

```
Failed to load gpu_info firmware "amdgpu/navi14_gpu_info.bin"
```

I had gotten a Kernel that supported Navi 14 (I assumed) but I was still running
VESA drivers, not the AMD Drivers.

A quick look at `inxi -SG` confirmed this, as I had no active driver for my
graphics card.

At this point, I tried a bunch of things, in various orders, so I am not really
sure what eventually solved my problem... However, I will give you the verbatim
solution, and maybe at one point I'll have time to reproduce my problem, do a
fresh install, and come back and revise these instructions.

## Update the drivers

I installed the latest mesa drivers (20.0.3) by adding the kisak-mesa PPA. `apt
upgrade` then did the rest.

This did not help.

## Add the firmware binaries

I then found that I had no Navi 14 firmware in `/lib/firmware/amdgpu/` so I
downloaded all `navi14_*.bin` files from the [linux-firmware
repository](https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux)
and added them to the aforementioned path.

This did not help either. I got an error message asking for `navi14_ta.bin`, but
the repository did not contain such a file (but there was one named
`navi10_ta.bin`).

## Install amdgpu from AMD

I opted to download the drivers straight from the horse's mouth instead. I went
to
[AMD](https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux)
and downloaded Radeon Software for Linux 19.50. It is easily installed by
extracting the archive and running `./amdgpu-install`.

Unfortunately this did not work.

## Downgrade the kernel

At this point I started to get frustrated. I recalled that one article I read
online had explicitly said that one must not run Linux 5.4.\*, but should use
5.5.\*. I had presumed that 5.6 would be even better, but everything was already
a mess, so why not try?

I installed the latest 5.5-kernel (5.5.17), upgraded, rebooted, and Bob is sure
your uncle. It worked!!

Now, `xrandr` showed the different output options of my GPU (previously it had
only showed *default output*) and I could play DotA!

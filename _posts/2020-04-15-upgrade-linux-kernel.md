---
title: Manually Upgrade Linux Kernel, Pop!\_OS
---

Upgrading the Linux Kernel manually is simple!

# Download Kernel

Find the Kernel you want at the
[kernel-ppa](https://kernel.ubuntu.com/~kernel-ppa/mainline/) and download the
`.deb`-files of interest (4 in total).

If you are reading this article, you want to download:

`linux-headers-*_all.deb`
`linux-headers-*generic*_amd64.deb`
`linux-image-unsigned-*_amd64.deb`
`linux-modules-*_amd64.deb`

For instance, if you want to download the Linux 5.6 Kernel, the files are:

```
linux-headers-5.6.0-050600_5.6.0-050600.202003292333_all.deb
linux-headers-5.6.0-050600-generic_5.6.0-050600.202003292333_amd64.deb
linux-image-unsigned-5.6.0-050600-generic_5.6.0-050600.202003292333_amd64.deb
linux-modules-5.6.0-050600-generic_5.6.0-050600.202003292333_amd64.deb
```

Put them all somewhere nice, like in: `~/Downloads/5.6.0/`

# Install Kernel

It's as simple as running `sudo dpkg -i *.deb` in whichever directory you chose
to put your `.deb`-files.

# Make the Kernel bootable

If you are using `grub`, I think all is fine here, but I'm running
`systemd-boot` so according to
[Frank](https://frank.kumro.io/installing-a-mainline-kernel-on-popos/) there
are some extra steps. Head over to his site and read from *Copying the installed
kernel to make it bootable* and down.


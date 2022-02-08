---
title: Dell U4021QW (Update)
---

In [an earlier post]({% post_url 2022-02-02-dell-u4021qw %}), I wrote about my struggles to find a monitor setup that
satisfies my quite modest requirements, as well as my initial encounter with the
[Dell U4021QW](https://www.dell.com/en-uk/shop/dell-ultrasharp-40-curved-wuhd-monitor-u4021qw/apd/210-ayjf/monitors-monitor-accessories).
Towards the end of the post I shared that I had some issues with the monitor but that I was in contact with Dell
support and was hoping to be able to resolve the issues.

My initial email to Dell was sent on the 27th of January (2022-01-27) and today, almost two weeks later, we have
reached the end of our troubleshooting.

## Let's quickly revisit the issue at hand

The monitor has a USB-hub and is meant to have KVM-switch functionality.
This is great, because I have three computers that I rotate between:

1. An HP Elite Book with Windows 10
2. A MacBook Pro M1 Pro
3. A desktop computer running Ubuntu

So, following [Dell's manual](https://dl.dell.com/content/manual32851179-dell-u4021qw-monitor-user-s-guide.pdf?language=en-us),
my intention is to have the "Super Speed USB 3.2 Gen1 A to B upstream cable" and a DisplayPort cable permanently
plugged into my desktop machine and then use the Thunderbolt 4 cable for whichever laptop I want to use[^usb-c-doc].
All my peripherals (keyboard, webcam, mouse dongle and microphone dongle) are then plugged into the monitor and *should* work with all computers.

*Should...*

When I wrote my previous post, the USB-hub functionality did not work, with any of the computers listed above.
Devices connected to the hub would stutter or stop functioning altogether after anywhere from seconds to minutes.
 
## BTW, I'm on my third monitor

Firstly, Dell sent me a replacement monitor with no fuzz!
They even over-nighted it to my apartment.
Great service!

Unfortunately, it arrived in quite bad shape...

<p align="center">
  <img width="350" src="{{ site.url }}/assets/images/broken-dell-box.jpg">
  <img width="350" src="{{ site.url }}/assets/images/broken-dell-u4021qw.jpg">
</p>

It went back to Dell the day after... but they did send me a *third* monitor that arrived a couple of days later.

## Conclusion 1: The monitor works with Windows

After a lot of additional troubleshooting, I got a driver sent to me over email -- which I *think* was the `A00-00 USB-C
Monitor Driver` that you can find on
[Dell's Support Page](https://www.dell.com/support/home/en-uk/product-support/product/dell-u4021qw-monitor/drivers),
but Dell did not confirm this -- and after installing said driver the monitor works (pretty much) flawlessly with my HP
Windows 10 laptop.
I do experience the occasional stutter, but it might as well just be the mouse acting up.

## Conclusion 2: The monitor does not work with Ubuntu

There is no equivalent driver (kernel patch?) for Ubuntu, even though Dell say they officially support Ubuntu both in
their documentation (take a look at the drop down menu over on
[Dell's Support Page](https://www.dell.com/support/home/en-uk/product-support/product/dell-u4021qw-monitor/drivers)
again) and in their emails to me.

After asking me to test a number of combinations of cables and configurations they eventually told me:

> It sounds like it's related to drivers, or maybe it's something in BIOS that is acting up...

As I have already pointed out, Dell does not list any "drivers" for Ubuntu on their support page, so I highly doubt
the non-existent driver is at fault.
I did check my BIOS settings and there are USB related settings in there, but they are all set to values that seem
reasonable (more permissive than not).

Dead end.

## Conclusion 3: The monitor does not work with MacBook Pro (M1 Pro)

This is probably the most frustrating issue, because I found
[this reddit post](https://www.reddit.com/r/ultrawidemasterrace/comments/p5sigt/dell_u4021qw_m1_macbook_pro/)
and OP claims to have *two* U4021QW working fine.
Additionally, since Dell has the [USB-C with a Mac article](https://www.dell.com/support/kbdoc/en-uk/000131273/using-a-dell-ultrasharp-usb-c-monitor-with-a-mac)
mentioned in the footnote earlier, it makes me so annoyed that I cannot get the monitor to work for me.

I got even more annoyed when I received the following from Dell's support:

> I consulted with higher tier support that confirmed that both Linux and MacOS based systems must use
> Video + Upstream cable for full functionality.

I want to call BS, because this is mentioned **absolutely nowhere** in Dell's official documentation...
Neither does it make any sense, since Dell claims other Dell monitors work with Thunderbolt and I see no reason why
they would limit this particular monitor.

## This is the end

Nevertheless, the U4021QW does not work for me and I have contacted the retailer I bought the monitor from.
They have offered to take the monitor back and help me look for a monitor setup that suits my needs.
I hope to write a more cheerful post in a week or so. That LG monitor I mentioned in my earlier post seems quite nice...

<!-- REFS and FOOTNOTES -->

[^usb-c-doc]: There is also an article called: [Using a Dell UltraSharp USB-C Monitor with a Mac](https://www.dell.com/support/kbdoc/en-uk/000131273/using-a-dell-ultrasharp-usb-c-monitor-with-a-mac), and even though it has not been updated since the U4021QW was released it still contains some information I think is worthwhile reading. The information in it indicates that it should be possible to use the Thunderbolt connection for Ultrasharp monitors with Mac computers.
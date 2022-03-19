---
title: Lenovo ThinkVision P40w-20 (the Dell is gone)
---

Yet again, another monitor post.

If you have not followed along in this saga, you can read about my initial struggles with the Dell U4021QW
[here]({% post_url 2022-02-02-dell-u4021qw %}) and my updated post where I described my two week long troubleshooting
session with Dell Support [here]({% post_url 2022-02-08-dell-u4021qw-update %}).

The TL;DR of those two posts is:
1. The monitor works with Windows (but poorly)
2. The monitor does not work with Ubuntu
3. The monitor does not work with MacBook Pro (M1)

## The hunt to find another monitor

In the previous posts I also explained that I was sad about the Dell not living up to my expectations, primarily because it
had been so difficult to find a monitor setup that satisfied my requirements to begin with.
Ideally, I want two daisy chained monitors (one 30" and one 24"), with Thunderbolt 4 connectivity to my laptops and
Display port + some USB-upstream solution for my desktop.
This has proven virtually impossible to come by, so I have loosened my requirements to _a monitor setup_ with:

* At least as many pixels as one would get from one 4k monitor (`3840 x 2160`) and one 1440p monitor (`2560 x 1440`)[^res].
* USB-hub functionality, so I can switch between my three computers (Windows, macOS, Ubuntu) without moving my peripherals.
* No external switch, unless absolutely necessary.

Together with Oskar, over at [Inet](https://inet.se), I have scavenged the market for a solution.
Simply put, since I really want to avoid an external KVM switch, we both concluded that we would have to settle for an
ultrawide monitor.
A handful of monitors were considered, such as:

* [Samsung S95UA](https://www.samsung.com/se/monitors/business/s95ua-49-inch-dqhd-curved-ls49a950uiuxen/), which has a KVM switch, but has too low resolution.
* [Eizo FlexScan EV3895](https://www.eizoglobal.com/products/flexscan/ev3895/index.html#tab03), which also has a KVM, but the same (low) resolution as the Samsung.
* [LG 40WP95C](https://www.inet.se/produkt/2220632/lg-40-ultrawide-40wp95c-21-9-wqhd-nano-ips-thunderbolt), which I mentioned in my earlier post.
  It has high enough resolution but lacks the USB hub.

Finally, Oskar mentioned that they would have a new monitor coming in soon; the [Lenovo ThinkVision P40w-20](https://www.lenovo.com/us/en/p/accessories-and-software/monitors/professional/62c1gar6us).
On paper, the monitor is very similar to the Dell U4021QW.
It has the same resolution, is the same size and has KVM functionality.
Additionally, it's a 75Hz panel (the Dell is 60Hz) and Thunderbolt 4 (the Dell has Thunderbolt 3) but the Lenovo **does not** have built-in speakers.

The Lenovo is also 2 000 SEK (~200 USD) cheaper.

## Switching the Dell for the Lenovo

Said and done, I placed an order for the Lenovo and Inet was kind enough to offer _both_ a refund for the Dell monitor
(even though that is usually a bit trickier for company purchases) and as if that wasn't enough, they also offered to
hold my old Dell monitor in their store while I tested the Lenovo.

While waiting for the Lenovo monitor, the Dell monitor started miss behaving even more.
The last week, I had to plug both my mouse and my microphone adapter into the laptop in order to use them.
Even on Windows, which I previously said was working fine.
It was like the monitor knew I was getting rid of it and wanted to make my life extra miserable...

Last Saturday (2022-03-12) I drove to the store and exchanged my Dell for the new Lenovo monitor and I have now been
using the Lenovo monitor daily, for a week.

### Reviewing the Lenovo

It's been a week with a lot of work (meaning Windows laptop) and workouts (meaning no computer at all), so I have
accumulated, maybe:

* 50h Windows + Thunderbolt
* 5h macOS + Thunderbolt
* 2h Ubuntu + Display Port + USB-upstream
* 3h iPad + Thunderbolt (_I use this for Zwift, but it's just a bonus that it works._)

I have three negative things that I have noticed with the Lenovo monitor.

1. When waking my Windows laptop from sleep, the monitor will sometimes not show anything.
   The peripherals works, but no image.
   The solution is to turn off/on the monitor, but I think it's a weird issue.
   I have not noticed the same issue with my MacBook, so it might by a Windows-issue, rather than the monitor itself.
2. The KVM switch does not automatically switch to the current active device[^kvm].
   This has caused me to wake my sleeping laptop _a lot_, which also means that there are two video inputs to the
   monitor, and usually Thunderbolt (which is often the wrong one, in these cases) takes precedence.
   The KVM switching functionality itself is not very intuitive either, so this really causes frustration...
3. I have noticed very minor -- but still noticeable -- mouse lag when using my MacBook.
   I have not noticed any issues today (browsing around a bit and now writing this post) but it is non-negligible and
   I _really_ hope it does not get worse.

Additionally, as I already mentioned, I _do_ miss the built-in speakers.
When using one of my laptops it's not a big deal (especially when using the MacBook which has better speakers than
the Dell monitor had) but I now need to use headphones when using my desktop.
That's a bummer.

## It's a keeper

Regardless.
It's been a week with the Lenovo monitor and it's here to stay, at least for the foreseeable future.
I'm content with it and even though it does not tick all my boxes, it does fulfill my requirements.

> Don't let perfect get in the way of good enough.

Right?

<!-- -->
[^res]: That is 11980800 pixels, for any one counting.
[^kvm]: The most common use case here is that I have used a Thunderbolt connected laptop during the day, but it is now sleeping, and I turn on my desktop machine.
        I want the monitor to detect that the only active computer is the desktop and switch the USB-hub to that computer.
        Instead, I need to manually switch over between Thunderbolt and USB-upstream.
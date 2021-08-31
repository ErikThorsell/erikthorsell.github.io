---
title: Issues with Apple devices after upgrading UniFi AP
---

As I mentioned in [my previous post about migrating my UniFi Controller]({% post_url 2021-08-29-migrate-unifi-controller %})
I successfully re-adopted an AP that I had not touched for several years, using
the [Home Assistant UniFi Controller Plugin][ha-unifi].
No one in the house reported any issues so I moved on and concluded the upgrade
a big success!

# Troubleshooting a badly behaving MacBook from 2012

Unfortunately, after ~24h the Apple devices in the house started behaving badly.
My wife (who is a Mac and iPhone user) noted that the WiFi on her laptop stopped
working.
It was not *just* the connection to the WiFi that occasionally failed; the WiFi
interface resolutely declared: **Status: Off** in the *Network Settings*.
I tried all things I could think of (reboot the laptop, remove/add the interface,
power cycle the wifi card) but nothing worked.

I actually blamed the 9 year old laptop and thought it finally decided to die.
The AP upgrade was unrelated and simply a fluke.

# Troubleshooting a badly behaving iPhone 12, 11 and an iPad Air 4th Gen

When we went to bed the same evening, my wife told me that her iPhone 12 was also
behaving poorly.
It connected/disconnected to/from the WiFi approximately once per minute.
She had not seen this before and thought it started recently.

I expected that this could not possibly be unrelated to the AP upgrade and the
issue with her MacBook, so I brought up the UniFi Controller on my phone
(Android 11, with no issues shown so far).
The log shown below glared back at me...

<p align="center">
  <img width="150" src="{{ site.url }}/assets/images/ap-issues.jpg">
</p>

I could also see that my work phone (iPhone 11) and our iPad Air showed similar
(but not as frequent) behavior.

# Going down the Apple/UniFi rabbit hole

I started searching around the Internet for some ideas.
Finally I found [this post][apple-sauce], and after changing my settings
accordingly things seem to work!
It is not clear to me what in the firmware upgrade caused the issues.
Maybe something 5G-related that was introduced recently?

I concluded that the AP logs did not show the connect/disconnect issues
and thereafter I tried to fix the WiFi interface on my wife's laptop.

* Remove the WiFi interface altogether
* Apply
* Add the WiFi interface again
* Apply
* **Profit!!**

*Previously, the above process resulted in the WiFi connecting for a split
second and thereafter go back to **Status: Off**.*

Now -- finally -- it seems like we have a successful UniFi Upgrade!


[ha-unifi]: https://github.com/hassio-addons/addon-unifi
[apple-sauce]: https://community.ui.com/questions/iPhone-Constantly-Disconnects-and-Reconnects/0240acbd-6db7-4f52-86b9-e75ac7373948#answer/73c33161-be05-42d4-8bd3-ddcf2d1bf2b8
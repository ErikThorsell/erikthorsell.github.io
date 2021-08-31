---
title: Migrate from old Unifi Controller to Unifi Controller in Home Assistant
---


I have been using my [pfsense][pfsense] router (bought from [teklager.se][teklager])
together with a [UniFi AP AC Lite][ap-ac-lite] for over three years.
The combo has worked flawlessly, but something has always bothered me; the
need for a [UniFi Controller][unifi-controller] or a [UniFi Cloud Key][unifi-cloud-key]
to configure the AP.
There's nothing inherently wrong with the controller software as such,
but I don't want to buy a Cloud Key and at the same time I *do* want a dedicated
device.
Therefore, I decided to migrate from an old (no longer existing) Docker based
controller, to the [Home Assistant UniFi Addon][ha-unifi].

If you don't care for the background, jump to the [step-by-step
instructions](#step-by-step-instructions).

# How we got here

Three years ago, I setup my AP AC Lite using Docker, on my laptop.
IIRC I used [this image](https://hub.docker.com/r/jacobalberty/unifi) by Jacob
Alberty.
It worked well, but you know what?
The Arch installation on that laptop is long gone and despite me taking a backup
of the data, I was unable to mount the volumes in a new container and get the
old Controller up and running again.

The beauty of the UniFi system -- however -- is that once you've set your AP up,
you don't really *need* your Controller again
*(Unless you want to upgrade your AP or make changes to it ... but ye.)*
so I have just let it be.
Today that changed.

# Home Assistant

About two years ago, I started using [Home Assistant][home-assistant] to handle
small automation tasks in our apartment.
Mostly light switches/bulbs talking [Zigbee][zigbee] with a [Conbee II][conbee]
stick.
It has been working great (and most importantly, my wife loves it).
A while ago I noticed that there's a [UniFi Addon][ha-unifi] for Home Assistant.
This piqued my interest, as I consider my Home Assistant installation much more
stable (and dedicated to one task) than my laptop.

# The Migration

Firstly, I understood that migrating from an old (now non-existing) controller
would most definitely result in downtime on our WiFi.
Hence, I had to ensure I performed the migration during at an appropriate time.
Luckily, in our household, that means: *on weekends, before my wife wakes up*.

## Step-by-step Instructions

1. Bring up the documentation for the [HA UniFi Addon][ha-unifi-docs].

2. Follow the installation instruction for the addon.
   
   *I have issues with the `Open Web UI`-button and need to connect using
   `<IP>:8443`.
   This is likely because I have setup my HA installation with
   reverse proxy, but the proxy does not forward 8443.*
   
3. Once you gain access to your newly installed controller, switch to the old
   user interface.
   (Or you won't be able to follow the Addon Documentation properly.)

4. Configure as much as possible in the UniFi Controller *before* you
   re-initialize your AP. This minimizes downtime.
   In my case, this entailed configuring the: `Site`, `Wireless Networks`
   (regular and guest) in addition to the `Controller` settings already 
   mentioned in the Addon Documentation.

   **LPT:** Use the same SSIDs and passwords as before.
   This worked like a charm for me, and all devices connected as if
   nothing had ever happened.

5. Now, to the only thing that threw me a curve ball.
   Since your AP is associated with another Controller you need to make your AP
   forget its old comrade before you attempt to adopt it in the new controller.

   **Note:**
   *I did not know this, so I followed the [Manually Adopting a Device instructions][ha-unifi-manual]
   in the HA Addon Documentation. It is possible that me issuing the `set-inform`
   command before restoring the AP affected the overall installation process,
   but I doubt it.*
   
   Regarding connecting to your AP using SSH, it is as easy as:
   ```
   ssh <username>@<ip-of-AP>
   ```
   *The default credentials for a non-adopted AP are `ubnt:ubnt`,
   but after an AP has been adopted and provisioned, the UniFi Controller changes the
   SSH login credentials.
   If you do not remember the login credentials to your AP you need to reset the AP
   some other way, maybe there's a hardware switch one can use, idk.
   That is out of scope for this post... Good luck though!*

6. Once you have a shell, it should look something like:
   ```
   LivingroomAP-BZ.3.9.42#
   ```
   From here, I reset the AP using:
   ```
   LivingroomAP-BZ.3.9.42# set-default
   ```

7. Your shell will drop and now you need to SSH into your AP again.
   This time, you must use `ubnt:ubnt`.

   ```
   LivingroomAP-BZ.3.9.42# mca-cli
   ```
   ```
   UniFi# set-inform http://<ip of the HA host>:8080/inform
   ```

8. By now, you should be able to see the AP under *Devices* in the Controller UI.
   Adopt it and the Controller will do the rest!
   Remember that the SSH Credentials will now change per the comment above.


[pfsense]: https://www.pfsense.org/ "pfsense - the world's most trusted open source firewall"
[teklager]: https://teklager.se/en/ "teklager website"
[ap-ac-lite]: https://www.ui.com/unifi/unifi-ap-ac-lite/ "UniFi AP AC Lite product page"
[unifi-controller]: https://www.ui.com/download/unifi/default/default/unifi-controller-v5-user-guide
[unifi-cloud-key]: https://store.ui.com/collections/unifi-accessories/products/unifi-cloudkey
[home-assistant]: https://www.home-assistant.io/
[zigbee]: https://zigbeealliance.org/solution/zigbee/
[conbee]: https://phoscon.de/en/conbee2
[ha-unifi]: https://github.com/hassio-addons/addon-unifi
[ha-unifi-docs]: https://github.com/hassio-addons/addon-unifi/blob/main/unifi/DOCS.md
[ha-unifi-manual]: https://github.com/hassio-addons/addon-unifi/blob/main/unifi/DOCS.md#manually-adopting-a-device

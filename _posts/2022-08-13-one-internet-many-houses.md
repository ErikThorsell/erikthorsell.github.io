---
title: Sharing your Internet connection between several apartments or houses
---

Recently, I have had several reasons to look into different ways to *share one Internet connection between several
apartments or houses* on a property.
I figured I'd create this post to have a reference to link to in the future.

# One Internet connection, many local networks 

At the core of it, we want to create a network setup where *one incoming Internet connection* can be split into
*several local networks*, which are not able to interfere with or talk to one another.

### Why?

Maybe you have a large house and rent out part of it as an apartment, or you have a property with two (or more) houses
and you rent out the other one(s).
Your property most likely only have one connection to the Internet (be it via fiber, DSL, or Dial-Up) and you now find
yourself wondering about how everyone who lives there can reach the Internet; but you might also wonder how
to make sure people living in different houses/apartments **cannot** reach each others' devices on your local network.

# Scope of this post

In this post, we will look at a scenario where a *Main House* has an incoming Internet connection via
fiber[^no-fiber] (terminated in a `Fiber Box`), but we want to have Internet connectivity in both the main house
and an extra rent out house.
We also would like to ensure that neither house can see the other house's Internet activities[^req-4].


# Some quick terminology

Software Development in general contains a lot of acronyms and abbreviations; networking is no different.
The three acronyms below are important to understand before we proceed.

### WAN

When we talk about [WAN][wiki-wan], we mean the *Wide Area Network* that constitutes the Internet.
(We will use *WAN* and *Internet* interchangeably in this post.)
The *WAN Port* on a router is the port by which you connect your router to your fiber box.

To the outside facing world, your WAN Port will have an IP.
This IP is referred to as *your public IP*.
When reading on, don't confuse your public facing (WAN) IP with any of the IP addresses on your *local* network.

### LAN

[LAN][wiki-lan] stands for *Local Area Network* and is the network we're mostly concerned with in this post.
The most common home network setup is a router with WiFi capabilities, where all devices (connected either via cable or
WiFi) belong to the same LAN.
Routers like these have a WAN port and often several ports labeled LAN 1, LAN 2, etc.
These LAN ports are not really ports for *different* LANs but belong to a built-in switch, giving you *X* number of
ports to your *one* LAN.
Unless you have configured your routing or firewall rules otherwise, all devices on your LAN can talk to one another.

In order to save addresses (and probably other good reasons you can read about on the link) LANs use
[dedicated IP address ranges][wiki-reserved-ip]; the two most commonly used are `192.168.0.0` to `192.168.255.255`
and `10.0.0.0` to `10.255.255.255`[^cidr].


### VLAN

*Virtual Local Area Network* [(VLAN)][wiki-vlan] is a technique for having multiple *virtual* LANs contained in the same
hardware.
Instead of having multiple, physical, LANs, the router uses VLAN tags to indicate which VLAN each network package
belongs to.

More on this below.

# Multiple IPs from your ISP

The simplest way to achieve separation of concerns for the two houses is to call your ISP and ask them if they can
provide you with multiple public IP-addresses.
In a usual home setup, each home will have one router, with one WAN port, and one public IP; but if you can
get your ISP to provide you with two public IPs you can connect your fiber box to a regular network switch and then
connect two routers to the switch.
It might even be the case that you can omit the switch altogether and just plug into several ports in the fiber box.

![Sharing your Internet connection with between multiple houses with multiple public IPs]({{ site.url }}/assets/images/share-lan-multiple-ip.png)

With this setup, each house can manage their own router (and additional network equipment) and they will not be more
connected than than yours and your neighbors' houses.

# Single IP from your ISP

More often than not, ISPs are reluctant to hand out several IPs.
Hence, we need a solution that works for such a use case.
But first, some disclaimers:

### Disclaimer about ports

Although I have not run into trouble myself, I have come across arguments online stating that a setup where you share
a single public IP -- as in the examples below -- might cause problems if you run applications that require certain
ports to be used.
Allegedly, certain games bind to certain public ports and if a user in *Main House* is playing said game and connects
to their server using `public-ip:some-predefined-port`, it might be the case that a user in *Rent Out* is unable to
establish a connection to the server.

I would hope this is not the case.
It seems silly to implement your application to only work with predefined ports (especially since ports are usually
arbitrarily assigned and any application could potentially occupy any port), but now you have been at least been
made aware.

Also, note that any port forwarding requirements will need to be carried out by the *Main House* owner, as that user
is the only one that *should* have access to the router/firewall interface.

### Disclaimer about hardware

Regardless of which solution you go for you will likely not be able to use a regular consumer router from
Asus, Netgear, etc.
You could either roll your own router or buy a prosumer router from (for instance) Ubiquiti.
It could also be the case that my knowledge is outdated and the consumer brands have evolved to include more advanced
functionality.

In the setups below there's only one router and it will (likely) live in *Main House*.
This makes you the IT Tech for both houses, for good and bad.
This also means you have full insight into the funnel through which all traffic flows.

### Disclaimer about WiFi

In the examples below, I have omitted any access points for WiFi connectivity.
Without knowing more about the actual needs for each house, it is difficult to be specific about the required hardware,
what brand of accesspoints to use, etc. 
Different vendors have different ways of setting up and managing their APs and going through all the common actors in
this post would be infeasible.

However, I have only used [UniFi Access Points](https://store.ui.com/collections/unifi-network-wireless) and setting
them up is relatively straight forward, but it does require additional hardware or the use of their phone app.
My UniFi APs are managed using the [Home Assistant UniFi Network Integration](https://www.home-assistant.io/integrations/unifi/).

## Router with several LAN interfaces

It is possible to buy a router with several LAN interfaces.
As an example, I use an [ADU3D4 from PC Engines](https://www.pcengines.ch/apu3d4.htm) -- with three gigabit NICs
(Network Interface Cards) -- as my router and firewall.
One port is configured as WAN and the other two are used as LAN ports.
Devices connected to `LAN 1` cannot talk to devices on `LAN 2`, and vice versa.

![Sharing your Internet connection with between multiple houses with multiple NICs]({{ site.url }}/assets/images/share-lan-single-ip-multiple-nic.png)

How to configure such a setup depends on the software you have installed on your router.
I have been using [pfSense](https://www.pfsense.org/) for the past couple of years and been very pleased with its
performance and ease of use.
Before pfSense I used a DYI router running Debian and way back I used a Netgear router flashed with DD-WRT.
It is difficult to get into the *details* about how to configure your network unless you can specify exactly what
software your using.
The aim of this post is to give the wider picture.

## Router with one LAN interface (use VLANs)

If you cannot get multiple IPs from your ISP and you do not have a router with at least three NICs, maybe your router
supports VLANs. A prerequisite is (1) that your router have NICs that support hardware VLAN tagging, and if you
have a need for ethernet connectivity (i.e. it's not enough to use the single NIC to connect a WiFi Access Point)
(2) you must have network switches which supports [IEEE 802.1Q][wiki-ieee], the official standard for VLAN.

![Sharing your Internet connection with between multiple houses with VLANs]({{ site.url }}/assets/images/share-lan-singel-ip-vlan.png)

With such a setup, you could vary the complexity.
Either you have one VLAN Switch and split the traffic straight away, or you forward the VLAN tags further along
the network chain.
Personally, I'd probably create one VLAN for the rent out and then have multiple VLANs for my personal needs, to
segment my own network further.

# Conclusion

There are multiple ways to achieve our goal.
The different ways have their pros and cons but in general I'd start from the top of the post and only move on to
trying out the next option if the previous one does not work.
It *is* -- I think -- easier to manage hardware than software; especially if your biggest concern is separation of
concerns.



<!-- --------------------------------------------------------------------------------------------------------------- -->

<!-- FEET NOTES -->
[^no-fiber]: If you do not have a fiber connection you could most likely just replace `Fiber box` with `Modem` or
             whatever is applicable for your situation and it should work all the same.
             We are concerned with the LAN, not so much with the WAN.

[^req-4]: And if (2) is not achievable we shall ensure that: (3) the renter cannot see the Internet connectivity in the
          *Main House*.

[^cidr]: IP address ranges can be written using CIDR notation, denoting blocks. The ranges listed could be abbreviated
         as `192.168.0.0/16` and `10.0.0.0/8`.

<!-- REFERENCES -->
[wiki-wan]: https://en.wikipedia.org/wiki/Wide_area_network
[wiki-lan]: https://en.wikipedia.org/wiki/Local_area_network
[wiki-reserved-ip]: https://en.wikipedia.org/wiki/Reserved_IP_addresses
[wiki-vlan]: https://en.wikipedia.org/wiki/VLAN
[wiki-ieee]: https://en.wikipedia.org/wiki/IEEE_802.1Q
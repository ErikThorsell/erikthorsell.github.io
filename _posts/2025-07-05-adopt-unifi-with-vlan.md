---
title: Adopt UniFi Devices with VLANs
---

_This is mostly a quick note to myself, for future reference._

If you plug in a new UniFi device on your network and it does not show up for adoption in your UniFi Network Application
UI, try switching the VLAN of the port in the upstream switch to be the same as the VLAN where you have your controller.

I am fairly sure I have been able to adopt devices using `Default (1)` as the setting on the switch, but I recently
bought a couple of
[USW-Flex-2.5G-5](https://eu.store.ui.com/eu/en/category/switching-utility/products/usw-flex-2-5g-5) switches as well
as two [U7-Pro-Max](https://eu.store.ui.com/eu/en/category/all-wifi/products/u7-pro-max) to extend my lab for work and
the first switch refused to show up under _UniFi Devices_. When I switched the upstream switch's port to the same VLAN
as where I run my Home Assistance instance (which in turn hosts my [UniFi Network
Application](https://github.com/hassio-addons/addon-unifi)) it showed up straight away.

Once the device has been adopted (and potentially updated) you can switch it to whichever VLAN you want.

<!-- --------------------------------------------------------------------------------------------------------------- -->

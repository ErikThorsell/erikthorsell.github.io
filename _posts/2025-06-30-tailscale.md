---
title: I replaced both OpenVPN and Wireguard with Tailscale on pfSense
---

Ever since I got my own place I have been hosting my own VPN. The purpose has been both to (1) ensure I can reach _my
stuff_ when I'm out and about, and (2) have a way to tunnel traffic when connecting to networks I'm not in
control of[^firstvpn]. I started my VPN-journey with my good 'ol [Asus
RT-N66U](https://openwrt.org/toh/asus/rt-n66u) which had a rudimentary PPTP VPN built in, but I quickly replaced the
default firmware with [Tomato](https://advancedtomato.com/) and IIRC I ran an OpenVPN Server for a while. I say _"for a
while"_, because I soon upgraded(?) my setup significantly, by building my own Debian-based router where I -- again --
ran OpenVPN.

## pfSense + OpenVPN & Wireguard

Since a couple of years back, I'm running [pfSense](https://github.com/pfsense)[^netgate] and when I setup my
first pfSense box I naturally deployed an [OpenVPN
Server](https://docs.netgate.com/pfsense/en/latest/vpn/openvpn/index.html) to go with it. Certificate based
auth was just a couple of clicks away and the service has been serving my household very well for several years. I did
dabble a little bit with [Wireguard](https://docs.netgate.com/pfsense/en/latest/vpn/wireguard/index.html) too, but truth
be told I never really got it to work the way I wanted it to.

## Tailscale as a mesh network

A couple of years ago, I first heard about [Tailscale](https://tailscale.com/). I figured it seemed like a nice product,
but I didn't really have a need for such a solution at the time. This all changed when I wanted to place a NAS at my
mother's place to act as an off-site backup. Her crappy, IPS provided, little router/firewall/switch combo-box did not
have the possibility to run a VPN Server. I also doubt her IPS would provide a public IP for her. Lastly, even if both
of these assumptions proved to be incorrect, I would not want to setup port forwarding in her firewall.

Well....

I started to look into to Tailscale a little bit more and found that it was perfectly suited for this use case. I sat
down to install Tailscale on the NAS and on my laptop, deployed a simple `Allow all` ACL configuration, and they could
talk within minutes. I joined my phone and all three devices were now able to talk to each other as if they were on the
same LAN.

_Sweet._

## Tailscale as a regular VPN

The tailnet solved the problem:

> How should I be able to communicate with a device which is not really accessible from the Internet?

but I still ran my OpenVPN Server in parallel for a long time (years), simply because I wasn't sure whether Tailscale
would be able to satisfy my other VPN-needs.

_Until this past weekend._

I did some more reading and learned about two critical features for me:

1. [Subnet routers](https://tailscale.com/kb/1019/subnets)
2. [Exit nodes](https://tailscale.com/kb/1103/exit-nodes)

The former let you extend your Tailscale network (known as a tailnet) to include devices that don't or can't run the
Tailscale client, and the latter can be used to tell your device to route _all traffic_ through your tailnet -- not only
the traffic that is going between Tailscale-adopted devices.

### My Tailscale configuration

In pfSense, I have installed the [Tailscale package](https://tailscale.com/kb/1146/pfsense) and configured it s.t. it
offers to be an exit node _and_ advertises routes. More specifically, I have advertised the subnet corresponding to the
VLAN where I have _the things I want to be able to connect to_ as well as `/32`-CIDR which points at the IP of my
reverse proxy. I have also enabled both _Accept DNS_ and _Accept Subnet Routes_.

On the Tailscale side I have the following ACL:

```hujson
{
  "groups": {
    "group:admins": [<list of users>],
    "group:family": [<list of users>]
  },
  "tagOwners": {
    "tag:admin-devices": [<list of users>],
    "tag:pfsense": [<list of users>],
    "tag:exit-node": [<list of users>],
    "tag:synology-mom": [<list of users>],
    "tag:family-devices": [<list of users>]
  },

 "grants": [
    // Allow admin-devices to reach everything
    {
      "src": ["tag:admin-devices"],
      "dst": ["*"],
      "ip": ["*"]
    },

    // Allow family-devices to reach HA Proxy VIP
    {
      "src": ["tag:family-devices"],
      "dst": ["10.10.11.1/32"],
      "ip": ["*:80", "*:443"]
    },

    // Allow admins and family members to use Tailscale as an exit node
    {
      "src": ["tag:admin-devices", "tag:family-devices"],
      "dst": ["autogroup:internet"],
      "ip": ["*"]
    },

    // Grant access to Synology NAS @ mom's
    {
      "src": ["tag:admin-devices", "tag:pfsense"],
      "dst": ["tag:synology-mom"],
      "ip": ["*"]
    }
  ]
}
```

> **NOTE:** The last grant, paired with a NAT rule in pfSense, allows _devices on specific IP:s_ to communicate directly
> with the off-site NAS even though they do not have Tailscale installed on them. Very convenient.

All in all, my configuration has proven itself over the past week and I have disabled my OpenVPN Server. My only complaint
thusfar is that the Tailscale iOS client is quite the battery drainer, so the _VPN On Demand_ feature isn't really useful.


<!-- --------------------------------------------------------------------------------------------------------------- -->


<!-- FEET NOTES -->
[^firstvpn]: More recent use cases also includes (3) being able to stream content only available from Sweden, when
    going abroad.

[^netgate]: This is not a post about Netgate politics and controversies, maybe another post...

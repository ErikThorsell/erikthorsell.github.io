---
title: Overlapping Docker network (subnet) gotcha
---

I have been running the good'ol `docker-compose` for too long and have been
meaning to upgrade to `docker compose` for quite a while.
Yesterday, it was time, but I got thrown a real curve ball by the Docker
network daemon (if that's what you call it).

## Overlapping subnets

I'll spare you 4h of troubleshooting, trying to figure out why _pretty much_
all of my Docker-stuff was working just fine, but my surveillance system did
not.
I found the issue when I tried pinging one of my cameras in `192.168.30.0/24`.
Pinging from my workstation worked fine, but pinging from the server[^desktop]
did not work.
This is weird, because both are in the `192.168.10.0/24` subnet.

When pinging from the server, I noticed that `ping` used a gateway it shouldn't:

<p align="center">
  <img width="450" src="{{ site.url }}/assets/images/docker-gotcha-2.jpg">
</p>

What I finally concluded was that Docker had created a bridge network for my
Graylog deployment with the subnet mask: `192.168.16.1/20`.
This CIDR spans: `192.168.16.0 - 192.168.31.255` which is a problem, because
I have VLANs for `192.168.[10,20,30,40].0/24`.

<p align="center">
  <img width="600" src="{{ site.url }}/assets/images/docker-gotcha-1.jpg">
</p>

Since the interface only existed on the server[^desktop], all my RTSP debugging
on my workstation was pointless...

## Removing the overlapping subnet

Luckily for me the "solution" was to do `docker compose down` on the Graylog
deployment and then `docker compose up` again.
This created a new non-overlapping bridge network. 

After investigating further I have found that it is possible to:

1. Specify the subnet for a bridge network upon creation \[[LINK](https://docs.docker.com/compose/compose-file/05-services/#ipv4_address-ipv6_address)\].
2. Set the default subnet from the Docker daemon \[[LINK](https://docs.docker.com/network/drivers/bridge/#use-the-default-bridge-network)\].

I am not sure whether the second option hinders the daemon from creating
_new_ networks outside the default range or the configuration just applies to
"the first network" which is created.

<!-- --------------------------------------------------------------------------------------------------------------- -->

<!-- FEET NOTES -->
[^desktop]: Yes, I know the hostname says `ubuntu-desktop`.
    The "server" is actually my gaming computer, which is repurposed and has been
    acting as a server for the past couple of years.

---
title: Openwrt NTP override
date: 2024-05-06 17:00 +500
categories: [openwrt, ntp]
tags: [openwrt,ntp]
---

# Force all devices to sync time with openwrt's NTP server

First see why you need to do that. 

* Some devices have ntp ip or dns hardcoded 
* some devices need to sync time for showing the right data according to set timezone
* some countries have change in time due to summer and winter

> So lets see how to do that:

## Proper/Easy way: 

Find where NTP is set up in settings (Web UI) and point it to your router.

## Hacky way:

If the device uses DNS names of NTP servers, override that locally to resolve these names to your IP (LuCI/DHCP and DNS / Hostnames)

## Even more Hackyway:

Catch all port 123/UDP traffic and redirect locally.

#### Reference 

<https://forum.openwrt.org/t/ntp-problem-with-a-tp-link-camera/145401/2>


# DNS override/hijacking

<https://openwrt.org/docs/guide-user/firewall/fw3_configurations/intercept_dns>
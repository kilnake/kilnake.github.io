---
title: Finding hidden DNS upstream
date: 2024-05-11 20:44 +500
categories: [homelab]
tags: [pihole, unbound, openwrt, proxmox]
image: /assets/thumbnails/pihole.png
---

## Configure Pi-hole Upstream DNS Servers

Each DNS server address is configured within two files `/etc/pihole/setupVars.conf` and `/etc/dnsmasq.d/01-pihole.conf`. By default, Pi-hole will use Google’s DNS servers.

1. Edit Pi-hole Setup Variables.

   ```bash
   nano /etc/pihole/setupVars.conf
   ```

2. Edit Dnsmasq configuration file.

   ```bash
   nano /etc/dnsmasq.d/01-pihole.conf
   ```

3. Restart Pi-hole DNS service for changes to take affect.
   ```bash
   pihole restartdns
   ```

## Configure Openwrt Upstream DNS for LAN interface

![openwrt](/assets/openwrtdns.png)

#### Good to know if your ISP is overriding your DNS, If yes use DNSCrypt

![test-tool](/assets/test-upstream-dns.png)

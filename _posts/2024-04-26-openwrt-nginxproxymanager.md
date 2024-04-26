---
title: Local DNS with Openwrt and Nginx Proxy Manager
date: 2024-04-26 19:48 +500
categories: [openwrt, nginxproxymanager, pihole, unbound]
tags: [openwrt,nginxproxymanager,pihole,unbound]
---

## Openwrt would be assigning local IP addresses and hostnames can be changed either via in openwrt, proxmox hostnames of specific container or vm.

Firstly set up static ip address and put hostnames.

`Network > DHCP and DNS > Static Leases`

![Openwrt page](/assets/ip.png)

#### Edit the local domain and ip address in the same format as yellow highlighted

![General addresses change](/assets/addresses.png)

#### Now add hosts in Nginx Proxy Manager 

Add services according to your needs

![nginxproxymanager-hosts](/assets/npm.png)


#### These are without https right now, But I would be adding HTTPS certificates using lets encrypt.

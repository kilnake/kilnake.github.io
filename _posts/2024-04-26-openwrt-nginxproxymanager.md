---
title: Local DNS with Openwrt and Nginx Proxy Manager
date: 2024-04-26 19:48 +500
categories: [openwrt, nginxproxymanager, pihole, unbound]
tags: [openwrt,nginxproxymanager,pihole,unbound]
---

#### Openwrt would be assigning local IP addresses and hostnames can be changed either via in openwrt, proxmox hostnames of specific container or vm.

`Network > DHCP and DNS > Static Leases`

![Openwrt page](/assets/ip.png)

#### Check yellow highlight

![General addresses change](/assets/addresses.png)

#### Now add hosts in Nginx Proxy Manager 

![nginxproxymanager-hosts](/assets/npm.png)


#### These are without https right now, But I would be adding HTTPS certificates using lets encrypt.

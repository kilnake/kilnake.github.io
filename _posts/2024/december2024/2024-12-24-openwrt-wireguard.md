---
title: Openwrt Wireguard
date: 2024-12-24 19:00 +500
categories: [openwrt, wireguard]
tags: [openwrt, wireguard]
image: (https://openwrt.org/_media/logo.png)
---

# Finally a quick GUI guide to setup and configure wireguard on openwrt using luci only.

1. Step - Packages to install

![add packages](/assets/wireguard-openwrt/package1.png)
![dont forget qr generator](/assets/wireguard-openwrt/package2.png)

## Save and Apply

2. Step - Configure Firewall

   ![port forward](/assets/wireguard-openwrt/pf1.png)
   ![port forward](/assets/wireguard-openwrt/pf2.png)

   ## Save and Apply

3. Step - Add and Configure Interface

![create new interface and pick wireguard protocol](/assets/wireguard-openwrt/int1.png)
![generate new keys by pressing button](/assets/wireguard-openwrt/int2.png)

## Save and Apply

4. Step - Add IPv6 in Advance tab

![delegate ipv6](/assets/wireguard-openwrt/int3.png)

## Save and Apply

5. Step - Add firewall to LAN

![assign firewall zone](/assets/wireguard-openwrt/int4.png)

## Save and Apply

6. Step - Add peers

![add peer](/assets/wireguard-openwrt/int5.png)
![generate peer keys](/assets/wireguard-openwrt/peer.png)

7. Step - Generate QR and choose right ddns/domain/IP

![generate qr and select right ddns and endpoints](/assets/wireguard-openwrt/qr.png)

## Save and Apply and Reboot

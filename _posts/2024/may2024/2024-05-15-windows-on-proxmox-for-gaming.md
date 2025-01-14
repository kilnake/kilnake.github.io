---
title: Gaming on Windows on Proxmox
date: 2024-05-15 11:44 +500
categories: [windows, proxmox]
tags: [proxmox, windows]
image: /assets/thumbnails/driver.png
---

# Have you ever dealt with this problem?

> "Cannot run under Virtual Machine" in windows vm (proxmox)

This is due to famous Easy Anti Cheat.

## Lets see how to fix it.

- Fill in the BIOS information (VM -> Options -> SMIBIOS Setting)
- Don't use virtio driver. Detached the SCSI drive, edit and change it to SATA drive
- Change the boot order and enable the SATA drive
- Network card MAC address change to INTEL type

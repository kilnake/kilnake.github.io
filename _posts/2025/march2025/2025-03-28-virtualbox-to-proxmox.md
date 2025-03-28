---
title: Virtualbox to Proxmox
date: 2025-03-28 15:44 +500
categories: [virtualbox, proxmox]
tags: [virtualbox, proxmox]
---

1. Convert .VDI to .IMG using VBoxManage

2. Move Image to Proxmox-accessible location.

3. Convert .IMG to .QCow2 using qemu-image (Step 2 & 3 are interchangeable)

4. Create blank proxmox VM without disks.

5. import disk

6. set boot order, attach disk.

7. done.

Also, hindsite- you could just copy the .VDI directly to proxmox, and use qemu-img to go straight from .VDI to .qcow2

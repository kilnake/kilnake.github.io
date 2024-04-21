---
title: Remove Proxmox Nag
date: 2024-04-21 11:01 +500
categories: [proxmox, initialconfig]
tags: [proxmoxnag,proxmox]
---

1. Login with root account. 

```bash
nano /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
```

2. Press Ctrl+w to search the text saying **No valid subscription** and press **enter**

3. Add **void ({    //** just before **Ext.Msg.show({**
   
   ![like this](/assets/proxmoxnag.png))

4. Press Ctrl+x and yes to save and exit.
5. The restart the service or reboot to take effect

```bash
systemctl restart pveproxy.service
```

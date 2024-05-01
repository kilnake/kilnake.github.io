---
title: Powershell GUI
date: 2024-05-01 13:44 +500
categories: [windows, powershell]
tags: [powershell]
---

# Generate powershell GUI directly 

This is fantastic for those who are coming from bash environment like me to get familiar with powershell.

```powershell
Show-Command Get-Process
```
![PowershellGUI](/assets/powershellgui.webp)

> Show-Command <any cmdlet> (e.g. Show-Command Get-Process) will create an UI for any PowerShell command.
{: .prompt-tip }

## This module shows user a toast message that their windows is on for long time and requries a hard-restart

<https://github.com/Windos/BurntToast>
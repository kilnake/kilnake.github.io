---
title: Windows Sysadmin stuff
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

## Reset Windows Graphics Driver

This key combo causes the Desktop Window Manager to recreate its graphics context and surface

>  From a discussion with an AMD Radeon driver engineer, it does NOT restart the graphics driver. It does appear to discard the desktop surface buffer and re-create the allocation from DWM (on a healthy system the desktop goes black for a second)

> Ctrl+Shift+Windows+B
{: .prompt-tip }

Any time I’m having issues with my monitors not being detected, screens flashing, etc. this shortcut comes in handy. Can be useful in a myriad of situations. Enjoy! 

## Windows A C Tiva-tion

<https://github.com/massgravel/Microsoft-Activation-Scripts>

## HVEC driver windows

There is an old package by MS for this extension "HEVC Video Extensions from Device Manufacturer".

Paste this in your browser and it will open the MS Store promt to install it:

<ms-windows-store://pdp/?ProductId=9n4wgh0z6vhq>

## EasyJob

Keep and execute your PowerShell and BAT scripts from one interface

<https://github.com/akshinmustafayev/EasyJob>

## Prank -Fake-update

<https://fakeupdate.net/>



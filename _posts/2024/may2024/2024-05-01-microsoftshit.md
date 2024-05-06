---
title: Windows Sysadmin stuff
date: 2024-05-01 13:44 +500
categories: [windows, powershell]
tags: [powershell]
pin: true
---

# Generate powershell GUI directly 

This is fantastic for those who are coming from bash environment like me to get familiar with powershell.

```powershell
Show-Command Get-Process
```
![PowershellGUI](/assets/powershellgui.webp)

> Show-Command <any cmdlet> (e.g. Show-Command Get-Process) will create an UI for any PowerShell command.
{: .prompt-tip }


## Fix all annoying windows issues at once.

```cmd
DISM /Online /Cleanup-Image /RestoreHealth
SFC /scannow
```

## This module shows user a toast message that their windows is on for long time and requries a hard-restart

<https://github.com/Windos/BurntToast>


## You can increase the FPS limit on RDP from 30hz to 60hz with a simple registry edit on the host machine

To do configure the registry entry, follow these steps:

    Start Registry Editor.
    Go to the following registry subkey:
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations
    On the Edit menu, select New, and then select DWORD(32-bit) Value.
    Type DWMFRAMEINTERVAL, and then press Enter.
    Right-click DWMFRAMEINTERVAL, and select Modify.
    Select Decimal, type 15 in the Value data box, and then select OK. This sets the maximum frame rate to 60 FPS.
    Exit Registry Editor, and then restart the computer.

Frame rate mapping

    15 decimal = 60 frames
    10 decimal = 40 frames
    5 decimal = 20 frames
    1 decimal = 4 frames
#### Reference

<https://learn.microsoft.com/en-us/troubleshoot/windows-server/remote/frame-rate-limited-to-30-fps>

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


## Corrupt a file- anyfile

<https://corrupt-a-file.net/>


## Better way to wipe harddrive with reports

This is based on old magnificient DBAN.

<https://github.com/martijnvanbrummelen/nwipe>


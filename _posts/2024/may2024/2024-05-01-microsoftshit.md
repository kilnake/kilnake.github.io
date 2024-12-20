---
title: Windows Sysadmin stuff
date: 2024-05-01 13:44 +500
categories: [windows, powershell]
tags: [powershell]
pin: true
---

# Microsoft Admin consoles direct portal login

<https://msportals.io/>

# Generate powershell GUI directly

This is fantastic for those who are coming from bash environment like me to get familiar with powershell.

```powershell
Show-Command Get-Process
```

![PowershellGUI](/assets/powershellgui.webp)

> Show-Command <any cmdlet> (e.g. Show-Command Get-Process) will create an UI for any PowerShell command.
> {: .prompt-tip }

## Fix all annoying windows issues at once.

```
DISM /Online /Cleanup-Image /RestoreHealth
SFC /scannow
```

## Proper Restart

```
shutdown /r /f /t 0
```

## This (from the command shell) will disable Hibernation and turn off Fast Startup all in one.

```
powercfg -h off
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

> From a discussion with an AMD Radeon driver engineer, it does NOT restart the graphics driver. It does appear to discard the desktop surface buffer and re-create the allocation from DWM (on a healthy system the desktop goes black for a second)

> Ctrl+Shift+Windows+B
> {: .prompt-tip }

Any time I’m having issues with my monitors not being detected, screens flashing, etc. this shortcut comes in handy. Can be useful in a myriad of situations. Enjoy!

## Windows A C Tiva-tion

<https://github.com/massgravel/Microsoft-Activation-Scripts>

- Right-click on the Windows start menu and select PowerShell or Terminal (Not CMD).
- Copy and paste the code below and press enter  
  `irm https://get.activated.win | iex`
- You will see the activation options. Follow the on-screen instructions.
- That's all.

## Free Imaging solution for windows depolyment

<https://aka.ms/mdtdownload>
<https://www.osdcloud.com/>
<https://fogproject.org/> Open Source

## Corporate DNS 101.

Nothing in your network should talk to external DNS except your DNS servers. The firewall should be blocking it since it's a known way for malware/spyware to exfil data (The malware sends data chucks over the DNS port to avoid detection).

## HVEC driver windows

There is an old package by MS for this extension "HEVC Video Extensions from Device Manufacturer".

Paste this in your browser and it will open the MS Store promt to install it:

<ms-windows-store://pdp/?ProductId=9n4wgh0z6vhq>

## BGinfo for easy locating the computers in the domain.

<https://learn.microsoft.com/en-us/sysinternals/downloads/bginfo>

#### Deploying BGInfo with Intune

- Get BGInfo from Sysinternals
- Run BGInfo, create your template, and save it as bginfo.bgi
- Get IntuneWinAppUtil.exe from this GitHub repo
- Package the scripts, template, and BGInfo
- Add the package to Intune, and deploy it

#### Creating the .intunewin package

You’ll need an install/uninstall script, which are shown here. Dump these in a folder as install.ps1 and uninstall.ps1 along with your bginfo.bgi templace and BGInfo64.exe. Since this is for labbing, I won’t bother with signing or any of that stuff.

**_install.ps1_**

```powershell
New-Item –ItemType Directory –Force –Path "C:\Program Files\BGInfo" | Out-Null
Copy-Item –Path "$PSScriptRoot\Bginfo64.exe" –Destination "C:\Program Files\BGInfo\BGInfo64.exe"
Copy-Item –Path "$PSScriptRoot\bginfo.bgi" –Destination "C:\Program Files\BGInfo\bginfo.bgi"
$Shell = New-Object –ComObject ("WScript.Shell")
$ShortCut = $Shell.CreateShortcut("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\BGInfo.lnk")
$ShortCut.TargetPath="`"C:\Program Files\BGInfo\BGInfo64.exe`""
$ShortCut.Arguments="`"C:\Program Files\BGInfo\bginfo.bgi`" /timer:0 /silent /nolicprompt"
$ShortCut.IconLocation = "BGInfo64.exe, 0";
$ShortCut.Save()
```

**_uninstall.ps1_**

```powershell
Remove-Item -Path "C:\Program Files\BGInfo" -Recurse -Force -Confirm:$false
Remove-Item -Path "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\BGInfo.lnk" -Force -Confirm:$false
Return 0
```

The next step is to run **intunewinutil.exe -c SOURCE -s bginfo64.exe -o DESTINATION -q**.

Once this is done, you’ll have a **.intunewin** file you can upload as a Win32 application.

#### Creating the app in Intune

In this deployment I just used the all-devices deployment group, but you can target it at any group you want. I’ve done this on my setup for the virtio-win driver MSI so that it only installs on machines with a quick device.deviceManufacturer -eq "QEMU" rule.

<https://www.youtube.com/watch?v=BFyX8EyTPho>

> Install command: **powershell -ex bypass -file install.ps1**

> Uninstall command: **powershell -ex bypass -file uninstall.ps1**

> Detection folder: **C:\Program Files\BGInfo**

> Detection file: **bginfo.bgi**

## Commands for powershell for repetative tasks

<https://cmd.ms/>

## Rock solid print management 3rd party tool

`http://www.laptechnologies.com/Printers.exe` from <https://www.donationcoder.com/forum/index.php?topic=20903.0> `This is very old tool but works flawless`

## Email things that should be checked while setting up domain

<https://dmarcian.com> and <https://www.learndmarc.com> as great tools.
<mxtoolbox.com> and <https://dnsdumpster.com> for dns

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

<https://github.com/PartialVolume/shredos.x86_64>

## Uniget UI

<https://github.com/marticliment/UnigetUI>

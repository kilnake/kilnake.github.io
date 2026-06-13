---
title: Windows Hygiene
date: 2026-03-24 13:44 +500
categories: [windows]
tags: [windows]
---

# The Only True Secure Computer Is One That's Turned Off — So Let's Do the Next Best Thing

> *"The only truly secure computer is one that's turned off, inside a safe, at the bottom of the ocean. But since you probably want to use your computer, let's build the next best thing."*

Security isn't glamorous. It's a checklist of things that feel tedious until the day they save you. This guide walks through the full stack of PC hardening — from firmware to browser to physical access — so you can stop being low-hanging fruit.

---

## 1. Security Starts in the UEFI, Not Windows

Most people think security begins with antivirus software. It doesn't. It begins before your OS even loads.

**The golden rule: if your BIOS is open, your PC is just a toy.**

### Set a BIOS Password

A cold boot attack is real. If someone has physical access to your machine for 60 seconds, they can boot a specialized Linux distro from a USB drive, dump your RAM, and bypass your local login entirely. A BIOS password locks the boot order and kills this attack before it starts.

### Enable Secure Boot

If you're running Windows, Secure Boot is your first line of defense against boot kits — malware that loads before your OS does. Linux power users have valid reasons to disable it, but for most people, it should be on.

### Enable Kernel DMA Protection

DMA (Direct Memory Access) lets hardware like Thunderbolt and USB-C devices talk directly to your RAM, bypassing the CPU. That's a performance win, but also a potential security nightmare. A malicious hardware implant can use DMA to read your encryption keys straight out of memory.

Enabling Kernel DMA Protection ensures your OS manages these requests, creating a logical barrier between your ports and your secrets. If your motherboard is from 2020 or later and this is off, you're leaving a physical backdoor open for a $20 hardware exploit.

---

## 2. Harden Windows From the Inside

Windows hides its most aggressive security features behind PowerShell commands and obscure menus. Here's how to actually use them.

### Exploit Protection — Control Flow Guard

Navigate to **Windows Security → App & Browser Control → Exploit Protection**. Don't just look at it — tweak it. Make sure **Control Flow Guard** is enabled.

In plain English: it stops a hacker from redirecting your program's execution flow into their own malicious code. It's the difference between a door that's shut and a door that's bolted.

### Attack Surface Reduction (ASR) Rules

Microsoft keeps these hidden because they're afraid of support tickets. You don't have to be.

Go to GitHub and download **ConfigureDefender** and set it to **HIGH**. This enables ASR rules, which block specific behaviors that are almost exclusively used by malware. Key ones to enable:

- **Block Office applications from creating child processes** — there is zero reason for Microsoft Word to launch a PowerShell script. This alone kills ~90% of macro-based ransomware.
- **Block obfuscated scripts**
- **Block executable content from email clients**

Think of it as telling your OS: *"If it looks like a threat and acts like a threat, kill it before it speaks."*

### Disable Unnecessary Services

If a service doesn't need to run, it shouldn't exist. Use tools like **O&O ShutUp10** to disable telemetry and unnecessary background services like Remote Registry and Print Spooler. Every running service is an attack surface.

---

## 3. Virtualization-Based Security (VBS)

This is the pro tier. Windows 10 and 11 can use your CPU's hardware virtualization — the same technology that runs virtual machines — to create a secure region of memory that's completely isolated from the OS itself.

Go to **Windows Security → Device Security → Core Isolation** and enable **Memory Integrity**. This ensures every driver trying to run in your kernel is verified and sandboxed first.

Yes, it has a minor performance cost. It's worth it.

### Enable the Microsoft Vulnerable Driver Blocklist

Hackers love **Bring Your Own Vulnerable Driver (BYOVD)** attacks. They take a legitimate but outdated, buggy driver from a reputable company and install it into your system to escalate privileges. The Microsoft Vulnerable Driver Blocklist is a database of these known-bad-good drivers. Keep it updated.

---

## 4. Lock Down Your Network

Your PC is hardened. Your network is still a public park.

Every time you visit a website, your PC sends a **plain-text DNS request** to your ISP's servers. Your ISP knows every site you visit. These requests can also be intercepted or spoofed by anyone on your local network — this is how DNS hijacking works.

### Switch to Quad9 DNS

[Quad9](https://www.quad9.net) is a nonprofit DNS provider focused on threat security. Every domain lookup is checked against a global database of malware command-and-control servers. If a domain is malicious, Quad9 simply tells your computer it doesn't exist.

### Enable DNS over HTTPS (DoH)

Go to **Windows Settings → Network & Internet → Ethernet/Wi-Fi → DNS Settings**. Set it to manual and toggle **DNS over HTTPS** on.

Your DNS requests are now wrapped in TLS encryption. Your ISP can no longer see what you're looking up, and anyone on your Wi-Fi can't poison your DNS cache.

### Use SimpleWall for Outbound Firewall Control

Windows Firewall is decent at blocking incoming connections, but it lets almost everything phone home freely. **SimpleWall** is an open-source frontend for the Windows Filtering Platform. With it, nothing connects to the internet until you explicitly say yes.

---

## 5. Physical Security

All the software hardening in the world means nothing if someone can plug something into your machine.

### Lock USB Ports When Unattended

A device like a Rubber Ducky (a USB attack tool) can type PowerShell commands at 1,000 words per minute, download a Remote Access Trojan, execute it, and hide — in under 60 seconds.

The fix: open **gpedit.msc** and navigate to:

```
Computer Configuration → Administrative Templates → System → Device Installation → Device Installation Restrictions
```

Enable **"Prevent installation of devices not described by other policy settings"**. This freezes your I/O — if a new device is plugged in, Windows will refuse to install the driver. Only disable it when you're intentionally adding hardware.

### Never Use Public USB Charging Ports

Juice jacking is real. If you absolutely must use a public USB port, buy a **USB data blocker** (yes, they're real, yes they're called USB condoms, and yes they work). They allow charging while physically blocking data transfer pins.

---

## 6. Browser Hygiene

90% of threats are delivered via the browser. Using stock Chrome with default settings is like walking through a biohazard lab without protective gear.

**Recommended browsers:** Brave or a hardened Firefox.

### Disable JavaScript for High-Risk Browsing

JavaScript is the root of almost every browser-based exploit. For high-risk browsing, use **NoScript**. It blocks all scripts by default — yes, this will break most modern websites, but that's the point. You whitelist scripts site by site, on domains you actually trust. It makes you immune to drive-by downloads and cross-site scripting attacks.

### Clear Cookies on Exit

Stale session cookies are a goldmine for attackers. If someone steals your session token, they can bypass your password *and* your 2FA. Set your browser to clear cookies on exit.

---

## 7. Identity and Access Management

### Use a Password Manager

If your password is your dog's name followed by a number, this section is for you. Use **Bitwarden** — it's open source, free, and generates 30-character random strings per site.

### Stop Using an Administrator Account

This is perhaps the single most impactful thing on this list.

If you're running as admin, malware runs as admin. If you're running as a standard user, malware hits a UAC prompt and dies. Create a standard user account for daily use and keep admin access separate. This is the **principle of least privilege**, and it's the difference between a minor infection and a full system wipe.

### Use Proper 2FA — Ditch SMS

SMS-based 2FA is weak. SIM swapping is trivially easy. Use a **TOTP app** like Aegis or Ente Auth. Better yet: buy a **YubiKey**. Hardware keys are phishing-resistant in a way that software never can be.

---

## 8. Persistence Detection — Know If You've Already Been Compromised

A hacker's real goal isn't just getting in — it's *staying* in. Malware hides in your registry, scheduled tasks, and startup folders so it survives reboots.

### Use Autoruns

**Autoruns** (from Microsoft Sysinternals) is the most comprehensive tool for auditing what starts with your computer. Run it as administrator and look for anything highlighted in **pink or yellow** — these are unsigned files or missing files.

Check the **Logon** and **Scheduled Tasks** tabs. Be suspicious of anything:
- Named generically (e.g., "updater", "helper")
- Running from `%TEMP%`, `AppData\Local`, or `AppData\Roaming`

**Real software lives in Program Files. Malware lives in user folders.**

Right-click anything suspicious and check it on **VirusTotal**, which scans against 70+ antivirus engines.

---

## 9. Offline Backups — The Only True Immunity to Data Loss

No security setup is complete without a backup strategy. Follow the **3-2-1 rule**:

- **3** copies of your data
- **2** different media types (e.g., internal SSD + cloud)
- **1** copy stored offsite

"Offsite" doesn't mean iCloud. It means an **external drive that is physically unplugged from your computer**. If the drive isn't connected, a ransomware attack cannot encrypt it.

And yes — emphasis on *electricity*. If you want to go deeper, look up **side-channel attacks**. It gets wild.

---

## Summary Checklist

| Layer | Action |
|---|---|
| Firmware | BIOS password, Secure Boot, Kernel DMA Protection |
| OS | Control Flow Guard, ASR rules, disable unused services |
| Virtualization | VBS / Memory Integrity, Vulnerable Driver Blocklist |
| Network | Quad9 DNS, DNS over HTTPS, SimpleWall |
| Physical | USB port lockdown, no public charging ports |
| Browser | Brave/Firefox, NoScript, clear cookies on exit |
| Identity | Bitwarden, standard user account, TOTP/hardware 2FA |
| Persistence | Autoruns, VirusTotal |
| Backup | 3-2-1 rule, offline external drive |

---

Security isn't a product you buy. It's a posture you maintain. Start with this list, keep researching, and stay paranoid — the good kind.
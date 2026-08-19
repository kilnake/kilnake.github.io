---
title: Linux game streaming
date: 2026-10-19 19:27 +500
categories: [linux]
tags: [linux,couch,stream,sunshine,lgtv,moonshine]
---

# Streaming PC Games/Desktop from Linux Mint to an LG webOS TV (Sunshine + Moonlight)

A beginner-friendly guide to streaming your Linux Mint desktop to an LG webOS TV using **Sunshine** (the host, running on your PC) and **Moonlight** (the client, running on your TV).s

> **Time estimate:** 45–75 minutes for first-time setup.
> **You'll need:** A Linux Mint PC, an LG webOS TV, both on the same Wi-Fi/network, and a spare 15 minutes where you don't mind your TV rebooting a couple of times.

---

## How this works

- **Sunshine** runs on your Linux Mint PC and shares your desktop/games over the network.
- **Moonlight** runs on your LG TV and displays the stream.
- Because LG doesn't officially allow apps like Moonlight in its store, you'll need to briefly put the TV into **Developer Mode** to sideload it. This is safe and reversible — it doesn't wipe your TV or void anything permanently.

---

## Part 1: Install Sunshine on Linux Mint

1. **Install Sunshine.** The easiest method is Flatpak:
   ```
   flatpak install flathub dev.lizardbyte.sunshine
   ```
   (A `.deb` package and AppImage are also available from the [Sunshine GitHub releases page](https://github.com/LizardByte/Sunshine/releases) if you prefer.)

2. **Launch Sunshine once** so its background service starts running.

3. **Open the Sunshine web dashboard** in a browser:
   ```
   https://localhost:47990
   ```
   Your browser will warn you about a self-signed certificate — this is expected, click through it. Set an admin username and password when prompted.

4. **Check your GPU encoder.** In the web dashboard, confirm Sunshine detected your graphics card (AMD, Intel, and Nvidia are all supported for hardware encoding; software encoding works as a fallback if needed).

5. **Open the firewall ports.** This is the step people most often miss — Sunshine needs both TCP *and* UDP ports open:
   ```
   sudo ufw allow 47984:48010/tcp
   sudo ufw allow 47998:48010/udp
   ```
   Double-check both rules are active:
   ```
   sudo ufw status verbose
   ```
   > 💡 **Why this matters:** If you only open the TCP range, initial connections and pairing may work, but streaming itself will fail with errors like `control stream establishment failed, error code 11` — because the actual video/control stream traffic runs over UDP.

6. **Restart Sunshine** after any firewall changes so it rebinds properly:
   ```
   sudo systemctl restart sunshine
   ```
   (Or just quit/relaunch it if you're using the Flatpak version.)

7. Leave the default **"Desktop"** entry in Sunshine as-is for now — that's what you'll stream first to confirm everything works.

---

## Part 2: Get Moonlight installed on the LG webOS TV

Because Moonlight isn't in the official LG Content Store, you need a developer account and a sideloading tool.

1. **Create a free LG developer account** at [webostv.developer.lge.com](https://webostv.developer.lge.com/).

2. **On the TV**, open the LG Content Store and install the **Developer Mode** app.

3. Open the Developer Mode app, log in with your new developer account, and turn on:
   - Developer Mode
   - The Key Server toggle

   > ⚠️ Developer Mode is **not permanent** — it can reset after a TV reboot or after a timeout. If Moonlight later disappears or won't launch, this is the first thing to re-check.

4. **On your PC**, download and install **Dev Manager Desktop** from [webosbrew.org](https://www.webosbrew.org/) (this is the tool that lets your computer talk to the TV).

5. In Dev Manager Desktop, connect to your TV using the **IP address and passphrase** shown in the TV's Developer Mode app.

6. Once connected, use Dev Manager Desktop to install **Moonlight** (the community webOS build, distributed via the webOS Homebrew Channel). It installs like any other webOS app.

---

## Part 3: Pair the TV with your PC

1. Confirm the TV and PC are on the **same local network** (same Wi-Fi/router, not a separate guest or IoT network — those often block device-to-device traffic).

2. Open **Moonlight** on the TV. Your Sunshine PC should appear automatically. If it doesn't, tap **Add**, and enter the PC's local IP address manually.

   > 💡 If the IP keeps timing out, first confirm Sunshine is actually reachable by opening `https://localhost:47990` directly on the Mint PC. If that works but the TV still can't connect, it's a network/firewall issue between the two devices — see the troubleshooting section below.

3. Moonlight will display a **4-digit PIN** on the TV screen.

4. On the PC, open the Sunshine web dashboard → **PIN** tab, and enter that same PIN to complete pairing.

5. Back on the TV, select your PC, then select **Desktop** — you should now be streaming!

---

## Part 4: Tune your stream quality

In the Sunshine web dashboard → **Settings**:

- **Resolution/frame rate:** 1440p60 is a good starting point for most modern TVs; adjust up or down depending on your TV's native resolution and your Wi-Fi/network strength.
- If the stream looks choppy or laggy, **lower the resolution or bitrate first** before assuming it's a hardware problem — most stutter issues are network bandwidth, not GPU power.
- Wired Ethernet (on either the PC or a Powerline/adapter for the TV) will always be more reliable than Wi-Fi if you have persistent quality issues.

---

## Part 5: Basic remote control navigation

Since you're using the TV's original (non-Magic) remote rather than a game controller, here's what works:

- **Navigate menus:** Directional buttons + OK/Select should move around the Moonlight interface normally.
- **Bring up the in-stream overlay** (to disconnect, check stats, or quit cleanly): **long-press the Back button** (or the Exit button, depending on your remote model). This is not always obvious — a *quick tap* on Back may just close the whole app instead of opening the overlay.
- **If Back/Exit doesn't respond at all:** try connecting a mouse (USB or Bluetooth) to the TV temporarily — some older Moonlight-tv versions have had bugs where the remote doesn't register on first launch until a mouse click "wakes up" input handling. This is usually a one-time hiccup per session.
- **Emergency exit:** If nothing else works, press the TV's **Home** button — this force-exits to the TV's main launcher. You can then reopen Moonlight and manually end the session from there if it's still shown as active in Sunshine.

> 💡 Since you're on the original remote (not the Magic Remote), stick to Back/Exit for the overlay — pointer-based gestures don't apply to you.

---

## Troubleshooting quick reference

| Symptom | Likely cause | Fix |
|---|---|---|
| `curl error: timeout has reached` when adding PC by IP | Firewall blocking Sunshine's ports, or wrong/stale IP | Check `sudo ufw status`, confirm PC's current IP, ensure TV isn't on an isolated guest network |
| `control stream establishment failed, error code 11` | UDP ports not open in firewall | Run `sudo ufw allow 47998:48010/udp`, restart Sunshine |
| TV can't find PC automatically | Different subnets / guest network isolation | Manually enter PC's IP; move TV off any guest/IoT Wi-Fi |
| Moonlight app installed but disappears later | Developer Mode expired/reset | Reopen Developer Mode app on TV, re-enable, reinstall if needed |
| Remote doesn't respond in Moonlight menus | Known input bug on first launch | Connect a USB/Bluetooth mouse briefly to "wake" input handling |

---

## Quick recap checklist

- [ ] Sunshine installed and running on Linux Mint
- [ ] ufw rules added for **both** TCP and UDP port ranges
- [ ] LG developer account created
- [ ] Developer Mode enabled on TV
- [ ] Dev Manager Desktop installed on PC and connected to TV
- [ ] Moonlight installed on TV via Dev Manager Desktop
- [ ] PC and TV paired via PIN
- [ ] Stream quality tuned to taste
- [ ] Comfortable exiting the stream with Back/Exit long-press

Enjoy your couch gaming setup! 🎮
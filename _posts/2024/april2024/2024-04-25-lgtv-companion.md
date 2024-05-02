---
title: Lgtv Rooting for Jellyfin and Kodi
date: 2024-04-25 13:28 +500
categories: [lgtv, webos, jellyfin, kodi]
tags: [lgtv,webos,jellyfin,kodi]
---

My LGTV having WebOS spyware is giving  headache so rooting is only option to get rid of ads all together as they have hardcoded DNS.

## Firstly browse to rootmy.tv
```
https://rootmy.tv/
```
#### Check github for more info

<https://github.com/RootMyTV/RootMyTV.github.io>
<https://github.com/webosbrew/webos-homebrew-channel>

* This entire github is savior as my WebOS version is v04.80.15 and I haven't updated. (I AM GLAD)
* WebOS TV Version 4.8.0-52106 (goldilocks2-gyeongju)
* LAN connected.
* LG TV 43UM7100PLB (2019)

#### Steps to follow

* (Pre-webOS 4.0) Make sure "Settings → Network → LG Connect Apps" feature is enabled.
* Developer Mode app must be uninstalled before rooting. Having this application installed will interfere with RootMyTV v2 exploit, and its full functionality is replaced by Homebrew Channel built-in SSH server.
* Open the TV's web browser app and navigate to https://rootmy.tv
* "Slide to root" using a Magic Remote or press button "5" on your remote.
* Accept the security prompt.
* The exploit will proceed automatically. The TV will reboot itself once during this process, and optionally a second time to finalize the installation of the Homebrew Channel. On-screen notifications will indicate the exploit's progress. On webOS 6.x Home Screen needs to be opened for notifications/prompts to show up.

Your TV should now have Homebrew Channel app installed.

By default system updates and remote root access are disabled on install. If you want to change these settings go to Homebrew Channel → Settings. Options there are applied after a reboot.

## Turn on computer and Device/DevMode Manager for webOS TV 

<https://github.com/webosbrew/dev-manager-desktop>

Make is executable and you can install remotely via telnet or ssh (whatever you have selected)

Here the the app list 

<https://repo.webosbrew.org/>

I will install :-

* Youtubeadfree <https://github.com/webosbrew/youtube-webos>
* Jellyfin
* Kodi
* Homebrew channel
* Homebrew channel updater
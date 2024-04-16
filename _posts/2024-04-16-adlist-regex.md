---
title: Adlist and Regex for network wide adblockers
date: 2024-04-16 19:48 +500
categories: [pihole, adlists]
tags: [pihole,regex,adlists]
---

> Simple copy and paste the adlists into your pihole or adguardhome or adblock or blocky instance.
{: .prompt-info }


![vue](img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=60&section=header")


```
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts	
https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt	
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt	
https://v.firebog.net/hosts/Easyprivacy.txt	
https://raw.githubusercontent.com/erkexzcx/disconnectme-pihole/master/services_Cryptomining.txt	
https://raw.githubusercontent.com/erkexzcx/disconnectme-pihole/master/services_Advertising.txt	
https://raw.githubusercontent.com/erkexzcx/disconnectme-pihole/master/services_Analytics.txt	
https://raw.githubusercontent.com/StevenBlack/hosts/master/alternates/fakenews-gambling/hosts	
https://raw.githubusercontent.com/superover/TikTok-Blocklist/master/tiktok.txt	
https://raw.githubusercontent.com/d43m0nhLInt3r/socialblocklists/master/TikTok/tiktokblocklist.txt	
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV.txt	
https://big.oisd.nl	
https://raw.githubusercontent.com/PolishFiltersTeam/KADhosts/master/KADhosts.txt	
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Spam/hosts	
https://v.firebog.net/hosts/static/w3kbl.txt	
https://adaway.org/hosts.txt	
https://v.firebog.net/hosts/AdguardDNS.txt	
https://v.firebog.net/hosts/Admiral.txt	
https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt	
https://v.firebog.net/hosts/Easylist.txt	
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext	
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/UncheckyAds/hosts	
https://raw.githubusercontent.com/bigdargon/hostsVN/master/hosts	
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt	
https://osint.digitalside.it/Threat-Intel/lists/latestdomains.txt	
https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt	
https://v.firebog.net/hosts/Prigent-Crypto.txt	
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Risk/hosts	
https://bitbucket.org/ethanr/dns-blacklists/raw/8575c9f96e5b4a1308f2f12394abd86d0927a4a0/bad_lists/Mandiant_APT1_Report_Appendix_D.txt	
https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt	
https://v.firebog.net/hosts/RPiList-Malware.txt	
https://v.firebog.net/hosts/RPiList-Phishing.txt	
https://raw.githubusercontent.com/Spam404/lists/master/main-blacklist.txt	
https://raw.githubusercontent.com/AssoEchap/stalkerware-indicators/master/generated/hosts	
https://urlhaus.abuse.ch/downloads/hostfile/	
https://zerodot1.gitlab.io/CoinBlockerLists/hosts_browser
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt
```

> Regex blobs for your pihole or adguardhome or adblock or blocky instance.
{: .prompt-info }


```
^(.+[-_.])??adse?rv(er?|ice)?s?[0-9]*[-.]
^(.+[-_.])??m?ad[sxv]?[0-9]*[-_.]
^(.+[-_.])??xn--
^adtrack(er|ing)?[0-9]*[-.]
^advert(s|is(ing|ements?))?[0-9]*[-_.]
^analytics?[-.]
^banners?[-.]
^beacons?[0-9]*[-.]
^count(ers?)?[0-9]*[-.]
^pixels?[-.]
^stat(s|istics)?[0-9]*[-.]
^telemetry[-.]
^track(ers?|ing)?[0-9]*[-.]
^traff(ic)?[-.]
(\.|^)bytecdn\.cn$
(\.|^)bytedance\.com$
(\.|^)bytedance\.net$
(\.|^)bytedns\.net$
(\.|^)byteicdn\.com$
(\.|^)byteimg\.com$
(\.|^)byteoversea\.com$
(\.|^)byteoversea\.net$
(\.|^)bytetcdn\.com$
(\.|^)hypstarcdn\.com$
(\.|^)ibytedtos\.com$
(\.|^)ibyteimg\.com$
(\.|^)ipstatp\.com$
(\.|^)isnssdk\.com$
(\.|^)muscdn\.com$
(\.|^)musemuse\.cn$
(\.|^)musical\.ly$
(\.|^)pstatp\.com$
(\.|^)sgpstatp\.com$
(\.|^)sgsnssdk\.com$
(\.|^)snssdk\.com$
(\.|^)tiktok\.com$
(\.|^)tiktokcdn\.com$
(\.|^)tiktokv\.com$
(\.|^)toutiao\.com$
(\.|^)worldfcdn\.com$
(\.|^)wsdvs\.com$
clarity.ms
```


> This is curated for my home setup while being super practical and no un-necessary blocking.
{: .prompt-tip }
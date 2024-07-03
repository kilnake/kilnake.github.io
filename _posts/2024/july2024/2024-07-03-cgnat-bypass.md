---
title: Bypass CGNAT using oracle VPS
date: 2024-07-03 10:44 +500
categories: [networking,oracle,cloud]
tags: [oracle]
---

Bypass CG-NAT, get yourself a free Public IP! (Reverse SSH Tunnel)
==================================================================

[![Dhruv Gera](https://miro.medium.com/v2/resize:fill:88:88/1*ecuLirIkinYH-hlKO4xQ2g.jpeg)](https://medium.com/?source=post_page-----c717d1000422--------------------------------)

[Dhruv Gera](https://medium.com/?source=post_page-----c717d1000422--------------------------------)

All credits to Dhruv gera, very proud of you brother.


Most of us today are plagued by CG-NAT, ruining our dreams of self hosting anything which can be accessed over the internet. And since sadly most of us are still on IPv4 and not IPv6, there’s not much you can do except paying your ISP, or can you?

![captionless image](https://miro.medium.com/v2/resize:fit:948/format:webp/1*YlfLHvh_LteMcwiduBA80A.jpeg)

How did I land here?
====================

On my journey of reverse proxying, self-hosting media server, LLM etc., I had a need to be able to access my home server from anywhere, and I needed a way to break through CG-NAT in order to do that. CG-NAT in basic terms is you sharing a common public IPv4 address with your neighbors because those are rare to come by.

Now, since Cloudflare Tunnels are limiting you to only HTML based content by their ToS, you can’t really do anything. And if you use ngrok and such, you need to pay to get static URLs, which defats the entire purpose: Enter Oracle Free Tier and Reverse SSH tunnels!

Reverse SSH tunnel is exactly what it sounds: Instead of you ssh-ing into the machine to send commands, you can instead have the data be tunneled back to you over the security of the SSH protocol!

The Procedure
=============

Now the clever amongst you would already know where this is going, but for those who don’t, here’s a basic overview:

1.  Grabbing yourself a free VPS
2.  Setting up SSH access and keys
3.  Running remote reverse tunnel
4.  Setting up an Apache reverse proxy on the server end (Optional)
5.  Enjoying!

This might seem daunting, but follow along and its super easy:

First, grab yourself a free tier Oracle VPS, they provide you with up to 4Gbit internet and 10TB of data bandwidth a month, way more than what a generic home server needs.

Spin up an always free tier VM, I would recommend going for the Ampere ARM instances, those are newer and way faster. It should look like this:

![You can select up to 4 cores and 24GB of RAM, but we honestly don’t need more](https://miro.medium.com/v2/resize:fit:862/format:webp/1*gOp_ZfST0uYKH2q4BlhbSg.png)

Make sure to open ports on the VM’s sub-net from the Oracle Dashboard, it looks like this:

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*9SzDDwaZnh9LvunnwAnLdg.png)

After this, login to the VM instance and setup all the stuff that you want, mostly an Apache server and reverse proxying if you want to connect domain name to a particular port ( I will be writing a guide on how you can reverse proxy anything in under 5mins! )

Now comes the fun part, from the local machine that hosts most of your stuff, just run this command:

```
ssh -N -g -R YOURPORT:LOCALIP:SERVERPORT
```

This sets up a reverse tunnel that will forward YOURPORT to the SERVERPORT on the VM we just set up. And now you can access the website/app from the server’s public IP and port combo! If you took the time to setup an Apache reverse Proxy, now you can add records in Cloudflare or any other provider and have a live website hosted at home!

The Automations
===============

Since I am a lazy person who wants everything to auto-resume, here’s a quick PowerShell script I wrote that continuously picks up the ssh tunnel connection if it ever drops, you can set it to run on startup and voila, you have no hassles!

Also, quick tip, you can forward multiple ports by adding -R in the end of the command and adding the same port IP combos, and ssh takes care of the rest!

```
while($true) {
    echo "Starting Proxy"
    ssh -N -g -R YOURPORT:LOCALIP:SERVERPORT
    echo "Connection Error"
    echo "Sleeping 10s"
    ssh username@SERVERIP "sudo fuser -k PORT/tcp" 
    # The PORT here should be a port you are using, this tackles an edge case
    # where the server keeps the tunnel open despite no connection
    Start-Sleep -Seconds 10
}
```

That’s it!
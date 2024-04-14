---
title: Selfhost secuirty checklist
date: 2024-04-14 13:48 +500
categories: [selfhost, security]
tags: [selfhost,security,cybersecurity]
---

# Crash course on security for Self hosting

* Here are the basic things you can do that will reduce a significant amount of the vulnerabilities you will see. I've got a number of other suggestions but these are some of the most critical.

* SSH is not safe to expose by default. Enforce lockout through Fail2Ban/CrowdSec and require key authentication.

* Any webserver facing the internet should be put behind a proxy using HTTP Basic Auth. While it isn't a particularly secure step, it does make it harder to enumerate for scanners and can be *just* enough of an extra step to defeat trivial attacks.

* Ensure that anything facing the internet are on a separate network and VLAN with only the absolutely necessary services are open to anything else

* Enable automatic updates on anything exposed to the internet (honestly in general but internet facing in particular). This will be one of the biggest things you can do to easily remove a great deal of attack surface.

* Any user accounts on these systems should have no permissions on any other system. Different passwords, no SSH keys shared, that sort of thing.

* Ensure that you have a good AV on each thing facing the internet, Defender for Endpoints (under the name MDATP still for Linux) is pretty competent and free. I say this as someone who has a raging hatred for MSFT products

* I don't entirely recommend dockerizing everything since I trust my ability to secure an application far more than some random gentleman on Docker Hub. However, if you don't have the skillset or time to harden them, by all means, sandbox things to hell. 

* If your firewall supports it, install and enable Suricata in block mode on that interface, it will take some tuning to not block legitimate traffic but can help cut down on a significant number of threats.

* Use HTTPS on everything that support it, Let's Encrypt works pretty well in my experience.

* Keep an eye on news for the services you run, particularly for any vulnerabilities and have a solid understanding on what is really running on your network. Excellent example of this is the recent Log4J mess.

> Bonus Round:
{: .prompt-tip }

If you want to go nuts and really harden your systems, go through CIS Level 1 benchmarks for the relevant services (if applicable) and operating systems. Deploying a real EDR (Endpoint Detection and Response) system with logging and alerting through a SIEM (Security Information Event Management) system.

I will note, we're moving far, far from "Securing a home server" and firmly into "Enterprise security lab" but a well tuned EDR, IDS and SIEM will give you a lot of defensive capability. However, this introduces a massive jump in complexity and requisite skillset.

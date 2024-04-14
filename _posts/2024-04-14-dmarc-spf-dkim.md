---
title: Bought domain name now what?
date: 2024-04-14 10:48 +500
categories: [domain, spf, dmarc, dkim]
tags: [domain,spf,dmarc,dkim]
---

# Bought domain name now what?

If you just bought a new domain name do not forget to fix it's emails! 

Make sure that domains that do not send email cannot be used for spoofing.

Make these changes to your domain name system (DNS) records.

## To protect your domain you need to create:

* an SPF record that says you do not have any sending servers
* a DMARC record to reject any email from your domain
* an empty DKIM key record
* a null MX record

## First - Create an SPF record

```
type: TXT

host or name: @ (if required)

value: v=spf1 -all

If you check your record using nslookup or dig you should get a result like this:

yourdomain.example.com. TXT “v=spf1 -all”
@ TXT “v=spf1 -all”
yoursubdomain.yourdomain.example.com. TXT “v=spf1 -all”
```

## Second - Create a DMARC record

```
type: TXT

host or name: _dmarc

value: v=DMARC1;p=reject;sp=reject;adkim=s;aspf=s;fo=1;rua=mailto:dmarc-rua@dmarc.service.example.com,mailto:dmarc@yourdomain.example.com
```

Replace dmarc@yourdomain.example.com with the email address that you want reports to be sent to.

If you check your record using nslookup or dig you should get a result like this:

```
_dmarc TXT “v=DMARC1;p=reject;sp=reject;adkim=s;aspf=s;fo=1;rua=mailto:dmarc-rua@dmarc.service.example.com,mailto:dmarc@yourdomain.example.com”
```


## Third - Create an empty DKIM record

```
type: TXT

host or name: *._domainkey

value: v=DKIM1; p=
```

As this is a wildcard record you cannot check it other than to look in your DNS host admin panel.

Revoke all existing DKIM selectors in both TXT and CNAME records.

This record will make email servers more likely to reject email from your domain.


## Finally - Create a null MX record

```
type: MX

host or name: leave this field empty

priority: 0

value: .
```


> Note that some DNS providers do not support a null MX record, so do not worry if you cannot create this record.
{: .prompt-info }

Once you have made these changes you can check your domain is configured correctly in the <**https://mxtoolbox.com**>

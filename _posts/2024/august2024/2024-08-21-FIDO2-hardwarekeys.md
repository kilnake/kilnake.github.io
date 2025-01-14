---
title: FIDO2 Hardware Keys Implementation Strategy
date: 2024-08-21 11:44 +500
categories: [windows, hardwarekeys]
tags: [windows, hardwarekeys, fido2]
image: assets/thumbnails/authentication.png
---

# Rolling out FIDO2 Hardware keys in M365

## Strategy and thought process how it works.

#### 1. You buy them

- Recommend distributing at least 3 Yubikeys (preferably 4) per person. $25 Yubikey FIDO2 Passwordless only highly recommended. If you're doing FIDO2 then purchase and deploy the Security Key Series, NOT the Yubikey 5 series. In the instructions ensure users enroll all of their yubikeys.
- Yubikey Security Series for $25 per key supports FIDO2 and NFC. They do not support the Yubikey app, TOTP, or other forms of MFA which is what you want if going strictly phish-resistant passwordless MFA.

#### 2. You distribute them

- x1 at home x1 on their keychain x1 for the office x1 as a spare.

#### 3.

Block Windows Hello For Business so they don't enroll Windows Hello For Business thinking they enrolled their Yubikey.

#### 4.

Send out instructions to users on how to enroll their Yubikeys, give users a few days/weeks to enroll them

#### 5.

Configure a conditional access policy to enforce Phish Resistant MFA and block all other forms of MFA.

<!-- prettier-ignore -->
> Also Android phones Yubikey NFC FIDO2 still doesn't work with M365. So hope you have iPhones(August 2024).
{: .prompt-tip }

<!-- prettier-ignore -->
> Do not fall back to Push MFA, TOTP or other methods that are not Phish Resistant. Remember the goal is Phish Resistent, no exceptions. Do it right and enforce them and do not give the option to fall back or use any other MFA methods. (Windows Hello For Business if configured properly or CBA is also acceptable)
{: .prompt-warning }

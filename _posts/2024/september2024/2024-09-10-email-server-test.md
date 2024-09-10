---
title: Email server Security test
date: 2024-09-10 11:44 +500
categories: [email, security]
tags: [email, dmarc, dkim, spf, dnssec]
---

# Essential Security Tests for Your Email Server

If you host your own email server, ensuring its security is critical. Regularly validating your server's configuration against security standards can help protect against various threats. Below is a list of publicly available security tests that I have found invaluable for validating and hardening my email server's security.

### Recommended Email Server Security Tests

    MECSA - JRC: <https://mecsa.jrc.ec.europa.eu>
    Great for testing StartTLS, X509 certificates, SPF, DKIM, DMARC, DANE, DNSSEC, and MTA-STS.

    Hardenize: <https://www.hardenize.com>
    Excellent for checking rDNS, PTR records, and cipher suites.

    Internet.nl: <https://internet.nl>
    Useful for testing IPv6 support and DNSSEC configuration.

    NCSC Email Security Check: <https://checkcybersecurity.service.ncsc.gov.uk/email-security-check/form>
    Focuses on testing DKIM, rDNS, and PTR records.

    CheckTLS: <https://www.checktls.com/TestReceiver?ASSURETLS>
    Validates mandatory TLS enforcement for email delivery.

    Mail-Tester: <https://www.mail-tester.com >
    Analyzes HELO compliance and rDNS configuration.

    DANE Test: <https://dane.sys4.de>
    Verifies the correct implementation of DANE.

### Conclusion

Regularly using these tools can help you maintain a secure and reliable email server, providing peace of mind and a solid defense against potential threats.

<!-- prettier-ignore -->
> Feel free to explore these resources to validate your server's security posture!
{: .prompt-tip }

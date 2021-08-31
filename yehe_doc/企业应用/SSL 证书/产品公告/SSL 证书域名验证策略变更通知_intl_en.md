
In order to comply with the requirements of CA/Browser Forum, the following changes will be introduced to domain validation policies, which will take effect from **December 1, 2021**.

**From December 1, 2021, file validation supports only issuing the SSL certificate for the current validated domain, but not wildcard SSL certificates as well as its sub-domains.**

Currently, Tencent Cloud’s SSL Certificate Service only requires validating the primary domain (e.g., `dnspod.cn`), and will also issue SSL certificates for wildcard certificates (e.g., `*.dnspod.cn` or `*.sub.dnspod.cn`) and its sub-domains (e.g., `sub.dnspod.cn` or `sub2.sub1.dnspod.cn`).

But from December 1, 2021, if a domain is validated using file validation, the certificate can only be issued for the domain validated. For example, if the domain `dnspod.cn` is validated using file validation, an SSL certificate can only be issued for the `dnspod.cn` domain, but not `*.dnspod.cn` or `sub.dnspod.cn`.

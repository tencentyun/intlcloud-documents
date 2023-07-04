### What domain names are supported by wildcard certificates?

Tencent Cloud SSL certificates can be wildcard certificates. A wildcard certificate can secure a single server domain name and all the sub-domain names of the same level.
- A wildcard certificate covers all sub-domain names of the same level. For example, both `*.tencent.com` and `*.cloud.tencent.com` are wildcard domain names.
- Currently, wildcard certificates support only wildcard domain names, and do not support ordinary domain names (non-wildcard domain names). If you require a certificate that covers multiple wildcard domain names, we recommend purchasing a multi-domain wildcard SSL certificate.

### What are the rules for matching a wildcard certificate with a domain name?
A wildcard certificate can match only sub-domain names of the same level, and cannot match sub-domain names of different levels. For example, a third-level wildcard domain name such as `*.tencent.com` does not support a fourth-level domain name such as `www.ssl.tencent.com`.

### Why can't I use file verification when applying for wildcard certificates?
From December 1, 2021, file verification supports only issuing the SSL certificate for the current validated domain, but not wildcard SSL certificates as well as its sub-domains. For more information, see [Domain Validation Policy Update](https://intl.cloud.tencent.com/document/product/1007/40857).

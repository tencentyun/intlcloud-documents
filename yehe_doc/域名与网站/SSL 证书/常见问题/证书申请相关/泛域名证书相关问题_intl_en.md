### What domain names are supported by wildcard certificates?

Tencent Cloud SSL certificates can be wildcard certificates. A wildcard certificate can secure a single server domain name and all the sub-domain names of the same level. Both OV certificates and DV certificates can be wildcard certificates.
If you have a server with multiple sub-domain names of the same level, you can use a wildcard certificate instead of purchasing and installing a certificate for each sub-domain name.
- Wildcard SSL certificates support second-level domain names.
- A wildcard certificate supports only 1 wildcard domain name, and does not support multiple domain names.
- Currently, wildcard certificates support only wildcard domain names, and do not support ordinary domain names (non-wildcard domain names). If you require a certificate that covers multiple wildcard domain names and 1 or more ordinary domain names, we recommend purchasing a multi-domain wildcard SSL certificate.

### What are the rules for matching a wildcard certificate with a domain name?
A wildcard certificate can match only sub-domain names of the same level, and cannot match sub-domain names of different levels. For example, a third-level wildcard domain name such as `*.tencent.com` does not support a fourth-level domain name such as `www.ssl.tencent.com`.

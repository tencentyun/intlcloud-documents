This document describes how to configure DNS hijacking test parameters for network quality, page performance, file download, and audio/video experience tasks in CAT.


## Hijacking categories
Hijacking falls into two categories:
- **DNS hijacking:** For example, if `www.cloud.tencent.com` is resolved to another server, user access will fail, or a non-Tencent Cloud IP will be returned.
- **Page tampering:** JS, HTML, and HTTP headers of intermediate pages are used for redirects, window opening, or frameset embedding and then rendering of the hijacked page on the user side. Common forms are pop-up ads, floating ads, redirects, etc.

**DNS hijacking monitoring parameter format:**
- Input: `www.cloud.tencent.com:202.0.3.55|203.3.44.67`
- Rule:
 - The part before the colon is the target domain.
 - The part after the colon is the match rule.
 - You can set multiple match rules and separate them by vertical bar.
 - The exact IP, IP wildcard, subnet mask, and CNAME can be set in a match rule.

**Use case:**

DNS hijacking allowlist:

| Input                                       | Description                                                        |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `www.cloud.tencent.com:202.0.3.55|203.3.44.67` | Indicates that IPs except 202.0.3.55 and 203.3.44.67 under the `www.cloud.tencent.com` domain are not hijacked. |
| `www.cloud.tencent.com:202.0.3.*`              | Indicates that IPs starting with `202.0.3.` under the `www.cloud.tencent.com` domain are not hijacked. |
| `www.cloud.tencent.com:202.0.3.1/27`           | Indicates that IPs starting with the same first 27 digits as 202.0.3.1 under the `www.cloud.tencent.com` domain are not hijacked. |
| `www.cloud.tencent.com:*`                      | Indicates that all IPs under the `www.cloud.tencent.com` domain are not hijacked.   |

DNS hijacking blocklist:

| Input                                       | Description                                                        |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `www.cloud.tencent.com:202.0.3.55|203.3.44.67` | Indicates that IPs except 202.0.3.55 and 203.3.44.67 under the `www.cloud.tencent.com` domain are hijacked. |
| `www.cloud.tencent.com:202.0.3.*`              | Indicates that IPs starting with `202.0.3.` under the `www.cloud.tencent.com` domain are hijacked. |
| `www.cloud.tencent.com:202.0.3.1/27`           | Indicates that IPs starting with the same first 27 digits as 202.0.3.1 under the `www.cloud.tencent.com` domain are hijacked. |
| `www.cloud.tencent.com:*`                      | Indicates that all IPs under the `www.cloud.tencent.com` domain are hijacked.   |


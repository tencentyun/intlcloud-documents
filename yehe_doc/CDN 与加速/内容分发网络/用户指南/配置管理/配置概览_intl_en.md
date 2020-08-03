<style> table th:first-of-type { width: 200px; } </style>

CDN supports various custom configurations that allow you to optimize your CDN acceleration service based on your business needs.

## Basic Configuration
| Configuration Name | Feature Description |
| ---------------------------------------- | ------------------- |
| [Basic Information](https://intl.cloud.tencent.com/document/product/228/7864) | You can change the domain name project, service region, and business type. |
| [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289) | You can configure the basic information of the origin server, the origin-pull request protocol, the origin domain, and the hot backup origin server to ensure smooth origin-pull. You can configure the settings in/outside mainland China differently. |


## Access Control
| Configuration Name | Feature Description |
| ---------------------------------------- | ------------------------- |
| [Ignore Query String Configuration](https://intl.cloud.tencent.com/document/product/228/35316) | You can specify whether a node will ignore the parameters after ""?"" in a user request URL. |
| [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292) | You can configure the HTTP referer blocklist/allowlist. You can configure the settings in/outside mainland China differently. |
| [IP Blocklist/Allowlist Configuration](https://intl.cloud.tencent.com/document/product/228/6298) | You can configure the IP blocklist/allowlist for access control. |
| [IP Access Limit Configuration](https://intl.cloud.tencent.com/document/product/228/6420) | You can configure the access limit of an IP to a single node. |
| [Video Dragging Configuration](https://intl.cloud.tencent.com/document/product/228/8111) | You can enable the video dragging configuration. |
| [Authentication Configuration](https://intl.cloud.tencent.com/document/product/228/35237) | You can configure the URL authentication. You can configure the settings in/outside mainland China differently. |


## Cache Expiration Configuration
| Configuration Name | Feature Description |
| ---------------------------------------- | ----------------- |
| [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/35317) | You can configure the cache expiration rules for the specified resources. |
| [Status Code Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35318) | You can configure the 403 and 404 status code cache period. |
| [HTTP Header Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35319) | You can configure the header cache policy. |

## Origin-Pull Configuration
| Configuration Name | Feature Description |
| ---------------------------------------- | -------------------- |
| [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184)  | You can enable/disable Range GETs. |
| [Follow 301/302 Configuration](https://intl.cloud.tencent.com/document/product/228/7183) | You can configure whether requests should be redirected when the origin server returns the 301/302 status code. |
| [Origin-Pull Timeout Configuration](https://intl.cloud.tencent.com/document/product/228/35227) | You can configure the timeout periods for origin-pull TCP connection and data loading to ensure smooth origin-pull. |


## Advanced Configuration

| Configuration Name | Feature Description |
| ---------------------------------------- | -------------------------------- |
| [Bandwidth Cap Configuration](https://intl.cloud.tencent.com/document/product/228/7541) | You can configure the bandwidth cap for domain names. When the cap is reached, the CDN service will be disabled and the access request will be forwarded to the origin server. You can configure the settings in/outside mainland China differently. |
| [HTTPS Configuration](https://intl.cloud.tencent.com/document/product/228/35212) | You can configure HTTPS to implement secure acceleration, which supports forced HTTPS redirection, HTTP2.0 access, and OCSP stapling. |
| [SEO Optimization Configuration](https://intl.cloud.tencent.com/document/product/228/35219) | You can enable SEO optimization configuration to ensure the stability of the search engine weights. |
| [HTTP Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320)  | You can add an HTTP header configuration. |

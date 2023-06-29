<style> 
table th:nth-of-type(1) {width:20%; } 
table th:nth-of-type(2){ width:45%; } 
table th:nth-of-type(3){ width:16%; } 
table th:nth-of-type(4){ width:19%; } 
</style>

## January 2022
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|ECDN origin-pull monitoring|This feature enables you to view monitoring curves in real time.|January 06, 2022|[Origin-Pull Monitoring](https://intl.cloud.tencent.com/document/product/228/32921)|

## December 2021
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|New names of acceleration types|Tencent Cloud CDN has changed the names of acceleration types: "Static content" to "Webpage file download", "Download" to "Large file download", and "Streaming media" to "Audio & video on demand". Note that only the names have changed.|December 10, 2021|[Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734), [Basic Information](https://intl.cloud.tencent.com/document/product/228/7864)|
|Upgrade of real-time logging|Real-time logging allows you to ship logs for regions outside the Chinese mainland and search logs in various ways.|December 06, 2021|[Real-time Logs](https://intl.cloud.tencent.com/document/product/228/35380)|


## October 2021
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|New user rewards|From October 25, 2021, new users who have activated Tencent Cloud CDN service and completed tasks during the required period will be rewarded.|October 25, 2021|New User Rewards|
|Added data metrics|Tencent Cloud CDN has added three metrics for beta data for regions in the Chinese mainland: top client IPs, top UA, and top Referer.|October 21, 2021|[Data Analysis](https://intl.cloud.tencent.com/document/product/228/32923)|
|Purging and prefetching .txt files| Purging and prefetching .txt files is supported.|October 13, 2021 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299), [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000)|
|Fine-grained configuration|Configuration based on file extension, file directory, and full directory is supported.|October 12, 2021 |[Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184)|
|Supported file types|Options `All Files` and `File Content-Type` are added.|October 12, 2021 |[Smart Compression Configuration](https://intl.cloud.tencent.com/document/product/228/35220)|


## September 2021
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Underscores and Punycode-converted Chinese characters|Underscores and Punycode-converted Chinese characters are supported. The Chinese domain name must obtain an ICP filing with the Chinese characters.|September 16, 2021|[Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734)|
|Added traffic limiting|The setting "Usage Limit Configuration", previously "Bandwidth Cap Configuration" supports traffic limiting with alarm percentage.|September 15, 2021|[Usage Limit Configuration](https://intl.cloud.tencent.com/document/product/228/7541)|
|Alarm threshold for bandwidth cap |CDN supports setting an alarm threshold for bandwidth cap. When the ratio of access bandwidth to the bandwidth cap reaches this value, an alarm message will be sent.|September 2, 2021|[Bandwidth Cap Configuration](https://intl.cloud.tencent.com/document/product/228/7541)|


## August 2021
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Quick configuration of CNAME|The capabilities of resolution and configuration have been interconnected between Tencent Cloud CDN and [DNSPod](https://console.dnspod.cn/). For domain names hosted on Tencent Cloud DNSPod, you can configure CNAME with fewer steps in the [CDN console](https://console.cloud.tencent.com/cdn/domains) to enable CDN acceleration.|August 26, 2021|[Configuring CNAME via DNSPod ](https://intl.cloud.tencent.com/document/product/228/42353)|
|Invalid status for URL prefetch| A new cache status "Invalid" is added. For invalid prefetch, the origin server will return an error status code such as 4XX/5XX.|August 18, 2021|[Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000)|
|New log field|A new log field is added, which is a port connecting the client and CDN nodes.|August 6, 2021|[Download Logs](https://intl.cloud.tencent.com/document/product/228/6316)|





## July 2021
| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|CDN-ECDN console | The CDN console integrates the ECDN service. A new user can activate both CDN and ECDN services without paying for the service that is not used. If you only have the CDN service activated, the ECDN service will be automatically activated after you add an ECDN domain name for the first time. | July 26, 2021 | [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734)|
|Origin-pull to a third-party bucket | Supports pulling resources from a third-party bucket such as AWS S3 and Alibaba Cloud OSS. The origin-pull authentication can be enabled. | July 14, 2021 | [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289)|



## June 2021

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Extended refund period for a traffic package | Eligible traffic packages are now refundable within 15 days | June 23, 2021 |Traffic Package Refund|
| Daily URL purge and prefetch quota increase | When you are running out of daily URL purge and prefetch quota, you can quickly increase it. | June 23, 2021 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299), [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000)|
|Query for the origin-pull node IP of acceleration domain names in the console | Supports querying the origin-pull node IP (including IP address and IP range) of acceleration domain names. | June 23, 2021 | Origin-pull Node Query|





## March 2021

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Batch change configuration|Supports changing domain name configurations for multiple acceleration domain names in batches, increasing configuration efficiency.|March 31, 2021 |[Batch Changing Configuration](https://intl.cloud.tencent.com/document/product/228/39911)|
|QUIC beta|Releases CDN QUIC beta. |March 2, 2021 |[QUIC](https://intl.cloud.tencent.com/document/product/228/39746)|
|POST request size configuration|Supports setting the maximum size of POST requests.|March 2, 2021 |[POST Request Size Configuration](https://intl.cloud.tencent.com/document/product/228/39747)|



## December 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Advanced origin-pull configuration | Supports more refined origin-pull configurations, including path-based origin-pull (by specifying the file type, folder, full-path file, or homepage) and client IP region-based origin-pull (which is not generally available), etc.| December 29, 2020 | [Advanced Origin-pull Configuration](https://intl.cloud.tencent.com/document/product/228/39745) |
| IPv6 access fully supported in the Chinese mainland | IPv6 access is available in the Chinese mainland. You can enable it to allow IPv6 addresses accessing CDN nodes. | December 14, 2020 | [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734) |
| Browser cache validity configuration | Supports customizing client browser cache policies to reduce origin-pull rate. | December 7, 2020 | [Browser Cache Validity Configuration](https://intl.cloud.tencent.com/document/product/228/38932) |
| Origin URL rewrite | Supports configuring origin URL rewrite rules. |  December 7, 2020 | [Origin URL Rewrite Configuration](https://intl.cloud.tencent.com/document/product/228/38933) |
| TLS version configuration | Supports enabling and disabling TLS versions as needed. | December 7, 2020 | [TLS Version Configuration](https://intl.cloud.tencent.com/document/product/228/38934) |
| Custom error page | Supports redirecting a request with the specified status code to the specified URL. | December 7, 2020 | [Custom Error Page](https://intl.cloud.tencent.com/document/product/228/38935) |
|Self-diagnosis tool upgrade | The self-diagnosis tool now supports domain names that have been connected to the "Global" and "Outside the Chinese Mainland" acceleration regions. | December 3, 2020 | [Self-Diagnosis Tool](https://intl.cloud.tencent.com/document/product/228/6304)|

## November 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Origin-pull request header configuration upgrade | Supports configuring the referer header. | November 25, 2020 | [Request Header Configuration](https://intl.cloud.tencent.com/document/product/228/37037) |
| Copy configuration | Supports copying the configurations of an existing forwarding domain name to one or multiple new forwarding domain names. | November 3, 2020 | [Copying Configuration](https://intl.cloud.tencent.com/document/product/228/38936) |


## October 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Official launch of the real-time log service | CDN access logs can be collected and published in real time to realize quick retrieval and analysis of log data. | October 29, 2020 | [Real-time Logs](https://intl.cloud.tencent.com/document/product/228/35380) |
|Domain name ownership verification|To prevent domain name appropriation, domain name ownership verification is required for connecting a new domain name to Tencent Cloud CDN.|October 14, 2020|[Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734)|




## August 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| ---------------------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Access URL rewrite               | Supports configuring URL rewrite rules to redirect 302 URLs to the specified URL. | August 13, 2020 | [Access URL Rewrite Configuration](https://intl.cloud.tencent.com/document/product/228/38074) |
| Closing ports for accesses from the Chinese mainland   | Supports closing the access ports 80, 8080, and 443 as needed.                      | August 13, 2020 | [Chinese Mainland Access Port Configuration](https://intl.cloud.tencent.com/document/product/228/39879) |
| Increasing the number of allowed/blocked IPs to 200 | Supports adding up to 200 allowed/blocked IPs.       | August 13, 2020 | [IP Blocklist/Allowlist Configuration](https://intl.cloud.tencent.com/document/product/228/6298) |

## June 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------ | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| UA blocklist/allowlist configuration          | Determines whether to deny or allow requests according to HTTP request header `User-Agent`. | June 30, 2020 | [UA Blocklist/Allowlist Configuration](https://intl.cloud.tencent.com/document/product/228/37256) |
| Downstream speed limit configuration             | Controls the CDN access bandwidth by setting the downstream speed limit on a URL.      | June 30, 2020 | [Downstream Speed Limit Configuration](https://intl.cloud.tencent.com/document/product/228/37257) |
| Configuring case-insensitive for cache keys       | Configures whether to ignore letter cases for cache keys (case-sensitive by default)    | June 30, 2020 | [Cache Key Rule Configuration](https://intl.cloud.tencent.com/document/product/228/35316) |
| Origin-pull request header configuration | Supports adding specified header information to the origin-pull request, such as carrying the real client IP. | June 30, 2020 | [Request Header Configuration](https://intl.cloud.tencent.com/document/product/228/37037) |
| Quick HSTS configuration           | Supports adding the header `strict-transport-security`.                  | June 30, 2020 | [HSTS Configuration](https://intl.cloud.tencent.com/document/product/228/37036) |
| OCSP stapling configuration            | Fully releases the quick OCSP stapling configuration to improve TLS handshake efficiency and speed up user authentication. | June 30, 2020 | [OCSP Stapling Configuration](https://intl.cloud.tencent.com/document/product/228/35216)|

## April 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Image optimization | Supports enabling WebP, Guetzli, and TPG compression for qualified requested images to effectively reduce downstream traffic generated by image transfer and reduce costs. | April 27, 2020 | Image Optimization |
| Enabling global CDN service manually| Opens up global acceleration service to global users.<br>Users can activate global CDN service easily in the console by themselves. | April 15, 2020 | [Configuring CDN from Scratch](https://intl.cloud.tencent.com/document/product/228/32978) |


## March 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Upgraded domain name retrieval feature| Supports resolving and verifying domain name ownership, reclaiming domain names, and connecting wildcard domain names.  | March 3, 2020 | [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734) |
| New origin-pull timeout configuration | Supports adjusting the timeout periods for origin-pull TCP connection and data loading to ensure normal origin-pull. | March 3, 2020 | [Origin-pull Timeout Configuration](https://intl.cloud.tencent.com/document/product/228/35227) |

## February 2020

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Beta of real-time log service | CDN access logs can be collected and published in real time to realize quick retrieval and analysis of log data. | February 24, 2020 | [Real-time Logs](https://intl.cloud.tencent.com/document/product/228/35380) |

## December 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Global CDN <br>The monthly operations report feature is supported | The monthly operations report feature in the Chinese mainland CDN console and overseas CDN console has been merged to improve the business status analysis of any month in the past year. | December 23, 2019 | [Data Analysis](https://intl.cloud.tencent.com/document/product/228/32923) |

## November 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------- | --------------------------------------------- | ---------- | ------------------------------------------------------------ |
| Global CDN <br>Purge cache | Supports the purge cache feature in the console for regions in and outside the Chinese Mainland. | November 14, 2019 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299) |
| Global CDN <br>Prefetch cache | Supports the prefetch cache feature in the console for regions in and outside the Chinese Mainland. | November 14, 2019 | [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| Global CDN <br>Log download | Supports downloading the CDN logs in the console for regions in and outside the Chinese Mainland. | November 14, 2019 | [Download Logs](https://intl.cloud.tencent.com/document/product/228/6316) |

## October 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------- | --------------------------------------------------------- | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>The statistical analysis page is redesigned | Following the upgrade of overseas CDN's data APIs, data analysis will be upgraded to global data analysis. | October 21, 2019 | [Data Analysis](https://intl.cloud.tencent.com/document/product/228/32923) |

## May 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------------------- | -------------------------------------- | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>The self-diagnosis tool is upgraded | Supports region and status diagnosis and list refreshing. | May 29, 2019 | [Self-Diagnosis Tool](https://intl.cloud.tencent.com/document/product/228/6304) |

## April 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------------------- | ------------------------------------ | ---------- | ------------------------------------------------------------ |
| Global CDN<br>Domain name level tagging is supported | Speeds up domain names query and improves the efficiency of domain names management. | April 16, 2019 | [Domain Name Search](https://intl.cloud.tencent.com/document/product/228/32913) |

## March 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------------------- | ---------------------------------------------------- | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>Bandwidth cap can be configured | This feature prevents hotlinking by malicious users which can generate high amounts of bandwidth and dramatically increase costs. | March 18, 2019 | [Bandwidth Limit Configuration](https://intl.cloud.tencent.com/document/product/228/7541) |
| Overseas CDN <br>Range GETs can be configured | Improves the delivery efficiency of large files greatly, speeds up the response, and reduces the pressure on the origin server. | March 18, 2019 | [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184) |

## January 2019

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------------------------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>IPv6 is now supported (in beta) | IPv6 acceleration is now launched in beta and is supported for ISPs in all provinces within Chinese mainland. | January 18, 2019 | [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734) |

## December 2018

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>More timestamp hotlink protection options are supported | More formats of timestamp hotlink protection are supported. | December 20, 2018 | [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292) |
| Chinese mainland CDN <br>The API for data query at a 1-minute granularity is supported| Allows you to query the actual billable data at 1-minute granularity and access the monitoring data in real time. | December 6, 2018 | [DescribeBillingData](https://intl.cloud.tencent.com/document/product/228/37472)<br>[DescribeCdnData](https://intl.cloud.tencent.com/document/product/228/31734) |

## November 2018

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>The data monitoring page is redesigned | Key monitoring metrics can now be easily viewed. | November 30, 2018 | [Panel Configuration](https://intl.cloud.tencent.com/document/product/228/32918) |
| Overseas CDN <br>Billing by region is supported | An overseas CDN billing zone is determined by the region where the CDN cache node is located, and CDN service fees will continue to be charged based on the zone-specific unit price and usage. | November 29, 2018 | [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949) |
| Chinese mainland CDN <br>All headers can be cached | Supports quick caching of all headers for Chinese mainland CDN. | November 29, 2018 | [HTTP Header Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35319) |

## May 2018

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>Multiple purge logics are supported for directory purge | Multiple purge logics are added for Chinese mainland CDN to help purge resources cached in CDN nodes on a regular basis. The nodes will pull the latest resources from the origin server and cache again. | May 31, 2018 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299) |

## January 2018

| Update | Description                                               | Release Date   | Documentation                                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>Timestamp hotlink protection can be configured | By setting an access control policy on the value of the referer field in the HTTP request header, the access source can be restricted to prevent hotlinking by malicious users. | January 30, 2018 | [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292) |
| Chinese mainland CDN <br>404 status code cache validity can be customized | Supports custom configuration of 404 status code cache validity. | January 30, 2018 | [Status Code Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35318) |

## November 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------- | ------------------------- | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>The time periods for overdue payment processing are adjusted | The time periods for overdue payment processing in CDN are adjusted. | November 9, 2017 | [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949) |

## September 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>Forced HTTPS 301 redirect is supported | Enables you to forcibly rewrite all HTTP requests arriving at the CDN node to HTTPS requests. Supports permanent 301 redirect. | September 30, 2017 | [Forced Redirection Configuration](https://intl.cloud.tencent.com/document/product/228/35214) |
| Chinese mainland CDN <br>Homepage cache validity period can be configured | Enables you to configure a set of expiration rules that the CDN cache nodes should follow when caching business contents. | September 30, 2017 | [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317) |

## July 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------- | -------------------------------- | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>The statistical analysis feature is launched | This feature keeps you informed of user distribution and usage. | July 7, 2017 | [Data Analysis](https://intl.cloud.tencent.com/document/product/228/32923) |

## April 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>Node region query is supported | Supports querying whether a specified IP belongs to a Tencent Cloud node and the service status. | April 12, 2017 | DescribeCdnIp |
| Chinese mainland CDN <br>Batch IP ownership query is supported | This feature enables you to batch query whether specified IPs belong to Chinese mainland CDN cache nodes and check their acceleration service regions, provinces, and ISPs. | April 12, 2017 | [Verify Tencent IP](https://intl.cloud.tencent.com/document/product/228/10747) |
| Chinese mainland CDN <br>Quick domain name export is supported | This feature enables you to quickly export the list of CDN domain names. | April 12, 2017 | [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736) |

## March 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>The advanced cache feature is launched | This feature enables you to adjust the node cache validity period dynamically by setting the `Max-Age` value in the HTTP response header `Cache-Control` of the origin server. | March 15, 2017 | [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317) |



## January 2017

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>HTTP header customization is supported | This feature enables you to add a custom header in the returned response message to implement cross-origin access when a business resource is requested. | January 12, 2017 | [HTTP Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320) |

## December 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| ----------------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Chinese mainland CDN <br>Bandwidth cap can be configured for domain names | Prevents hotlinking by malicious users which can dramatically increase bandwidth usage and result in exorbitant costs. | December 14, 2016 | [Bandwidth Cap Configuration](https://intl.cloud.tencent.com/document/product/228/7541) |
| Chinese mainland CDN <br>Forced HTTPS redirect is supported | This feature enables you to specify a redirect method and forcibly rewrite all HTTP requests arriving at the CDN node to HTTPS requests. | December 14, 2016 | [Forced Redirection Configuration](https://intl.cloud.tencent.com/document/product/228/35214) |
| Chinese mainland CDN supports primary/secondary origin server configuration | This feature ensures the high availability of origin-pull. | December 14, 2016 | [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289) |
| Chinese mainland CDN <br>Switching between customer and COS origin servers is supported | This feature enables you to change the type of the primary origin server from customer origin server to COS origin server and vice versa. | December 14, 2016 | [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289) |
| Chinese mainland CDN <br>Range GETs can be configured | This feature can greatly improve the delivery efficiency of large files, speed up responses, and reduce the pressure on the origin server. | December 14, 2016 | [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184) |
| Overseas CDN <br>Cross-border origin-pull optimization is supported | Overseas CDN supports cross-border origin-pull optimization.  | December 14, 2016 | [Data Types](https://intl.cloud.tencent.com/document/product/228/31739) |

## November 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>Purge and prefetch are supported             | Overseas CDN now supports the purge cache and prefetch cache features. | November 25, 2016 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299)<br> [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| Overseas CDN <br>Access log download is supported | The access logging feature is launched in Overseas CDN to help you analyze user access. | November 25, 2016 | [Download Logs](https://intl.cloud.tencent.com/document/product/228/6316) |
| Overseas CDN <br>COS origin server is supported | Static resources in COS can be connected to Overseas CDN for global acceleration and delivery to user clients. | November 1, 2016 | [COS as Origin Server of CDN](https://intl.cloud.tencent.com/document/product/228/32977) |

## October 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Overseas CDN <br>HTTPS acceleration is supported | You can upload certificates for deployment or directly deploy certificates hosted in Tencent Cloud SSL Certificates Service to the CDN platform. In this way, you can enable HTTPS acceleration service to implement encrypted data transfer over the entire network. | October 28, 2016 | [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213) |
| Chinese mainland CDN <br>Real-time monitoring of origin-pull data is supported | This feature enables you to view monitoring curves in the last 6 hours at 1-minute granularity.  | October 26, 2016 | [Origin-Pull Monitoring](https://intl.cloud.tencent.com/document/product/228/32921) |
| Batch certificates configuration is supported   | Certificates can be configured in batches in the console.   | October 26, 2016 | [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229) |

## September 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| IP access limit can be configured | By limiting the number of access requests per second from a client IP to a node, you can defend against high-frequency CC attacks and prevent hotlinking by malicious users. | September 23, 2016 | [IP Access Limit Configuration](https://intl.cloud.tencent.com/document/product/228/6420) |

## August 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| -------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Cache validity rule priority adjustment is supported | The priorities of multiple cache validity rules can be adjusted. | August 22, 2016 | [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317) |
| IP blocklist/allowlist can be configured | By setting an access control policy on IPs of user requests, you can effectively restrict the access source to prevent malicious IP hotlinking and attacks. | August 11, 2016 | [IP Blocklist/Allowlist Configuration](https://intl.cloud.tencent.com/document/product/228/6298) |
| Self-diagnosis tool is supported | This tool enables the detection of DNS resolution of connected domain names, linkage quality, node status, origin server, and data access consistency. | August 11, 2016 | [Self-Diagnosis Tool](https://intl.cloud.tencent.com/document/product/228/6304) |

## July 2016

| Update | Description | Release Date | Documentation |
| --------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| SEO optimization configuration is supported   | This feature solves the problem of incorrect weights of domain name search results due to frequent IP changes by CDN. By identifying whether an access IP belongs to a search engine, you can choose to directly pull the resource from the origin server, ensuring the stability of the search engine weight. | July 19, 2016 | [SEO Optimization Configuration](https://intl.cloud.tencent.com/document/product/228/35219) |
| Custom HTTP Header is supported | This feature enables you to add a custom header in the returned response message to implement cross-origin access when a business resource is requested. | July 19, 2016 | [HTTP Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320) |

## June 2016

| Update | Description                                               | Release Date   | Documentation                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| The resource prefetch feature is launched<br>(In beta test)   | CDN offers a resource prefetch feature that enables you to load specified resources to a cache node by simply submitting the list of resources in the CDN console instead of waiting for user requests to trigger. | June 30, 2016 | [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| Entry for Overseas CDN application is opened <br>(In beta test) | You can apply to enable Overseas CDN acceleration on this page. | June 30, 2016 | [Overseas Acceleration](https://intl.cloud.tencent.com/document/product/228 ) |
| The CDN monthly operational report feature is launched | Your monthly business status is displayed in multiple dimensions to facilitate analysis of your business operations. | June 13, 2016 | [Data Analysis](https://intl.cloud.tencent.com/document/product/228/32923) |

## April 2016

| Update | Description | Release Date | Documentation |
| ------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Free third-party HTTPS certificates are provided | You can go to the [SSL Certificates Service console](https://console.cloud.tencent.com/ssl) to apply for a free third-party certificate provided by TrustAsia. | April 29, 2016 | [FAQs about HTTPS](https://intl.cloud.tencent.com/document/product/228/11206) |

## March 2016

| Update | Description | Release Date | Documentation |
| ------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN supports querying IP ownership | This feature enables you to verify whether a specified IP belongs to a Chinese mainland CDN cache node and check its acceleration service region, province, and ISP. | March 4, 2016 | [Verify Tencent IP](https://intl.cloud.tencent.com/document/product/228/10747) |

## January 2016

| Update | Description | Release Date | Documentation |
| ----------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN supports COS origin server | Static resources in COS can be connected to CDN for global acceleration and delivery to user clients. | January 20, 2016 | [COS as Origin Server of CDN](https://intl.cloud.tencent.com/document/product/228/32977) |

## October 2015

| Update | Description                                               | Release Date   | Documentation                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| The entire network status monitoring feature is launched for CDN | This feature enables you to monitor the latency and availability status of ISPs in all provinces of Chinese mainland and each region outside the Chinese mainland. | October 10, 2015 | [Entire Network Status Monitoring](https://intl.cloud.tencent.com/document/product/228/6311) |

## August 2015

| Update | Description | Release Date | Documentation |
| -------------------------- | --------------------------------------- | ---------- | ------------------------------------------------------------ |
| Multidimensional statistics collection (such as access status code) is supported | Statistics of 2XX/3XX/4XX/5XX status codes can be collected. | August 8, 2015 | [Access Monitoring](https://intl.cloud.tencent.com/document/product/228/32920) |

## June 2015

| Update | Description | Release Date | Documentation |
| -------------------- | -------------------- | ---------- | ------------------------------------------------------------ |
| Directory purge | Resources can be purged by directory. | June 12, 2015 | [Purge Cache](https://intl.cloud.tencent.com/document/product/228/6299) |
| Prefetch feature for large files | Large files can be prefetched. | June 12, 2015 | [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000) |

## May 2015

| Update | Description | Release Date | Documentation |
| ---------------------------------- | ------------------------------------ | ---------- | ------------------------------------------------------------ |
| Cache validity inherits the origin server's `cache-control` | The cache validity inherits the origin server's `cache-control` parameter. | May 18, 2015 | [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317) |

## April 2015

| Update | Description | Release Date | Documentation |
| ---------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Origin domain can be configured | CDN supports modifying origin domains. | April 20, 2015 | [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289) |
| Referer hotlink protection can be configured | By setting an access control policy on the value of the referer field in the HTTP request header, the access source can be restricted to prevent hotlinking by malicious users. | April 20, 2015 | [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292) |
| Advanced features such as cache validity are launched | Cache validity of resources of a particular type or resources in a particular directory or path can be specified. | April 20, 2015 | [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317) |

## March 2015

| Update | Description | Release Date | Documentation |
| ---------------------------------- | ---------------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN supports connecting customer and FTP-hosted origin servers | Customer and FTP-hosted origin servers are supported. | March 15, 2015 | [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734) |
| Bill-by-bandwidth and bill-by-traffic are supported  | CDN offers two billing modes: bill-by-bandwidth and bill-by-traffic. | March 15, 2015 | [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949) |
















## Vast Resource Reserves

### Nodes in mainland China

CDN has over 2,000 cache nodes deployed across all provinces in mainland China, with a total reserved bandwidth of over 110 Tbps. These are all high performance and highly secure Tencent Cloud data centers with quality ISP networks. In addition, Tencent Cloud has strengthened connections with China Mobile, China Unicom, China Telecom, and over 50 small and medium-sized ISPs, and has built four central nodes to significantly improve CDN's acceleration effect.
![img](https://main.qcloudimg.com/raw/c7af2903e117b831a68bbaaf13967181.png)

| Region   | Distribution                                                     |
| :--- | :----------------------------------------------------------- |
| East China | Shanghai, Jiangsu, Zhejiang, Anhui, Jiangxi, Shandong, Fujian       |
| North China | Beijing, Tianjin, Shanxi, Hebei, Central Inner Mongolia             |
| Central China | Henan, Hubei, Hunan                                       |
| Northwest China | Shaanxi, Gansu, Qinghai, Ningxia, Xinjiang, western Inner Mongolia |
| South China | Guangdong, Hainan, Guangxi                               |
| Southwest China | Chongqing, Sichuan, Guizhou, Yunnan, Tibet                   |
| Northeast China | Heilongjiang, Jilin, Liaoning, eastern Inner Mongolia                   |

### Nodes outside mainland China

CDN has been working industriously on global acceleration since 2017. As of December 2022, CDN has over 8,00 cache nodes across more than 70 countries and regions with a total reserved bandwidth of over 50 Tbps, helping your business go global with ease and speed.
![image-20200210165753661](https://main.qcloudimg.com/raw/034a95d5f46fb8bf848c0a53dd265611.png)

| Region   | Distribution                                                     |
| :----- | :----------------------------------------------------------- |
| North America | United States, Mexico, Canada                                         |
| South America | Brazil, Colombia, Peru, Ecuador, Chile, Argentina                 |
| Asia   | Hong Kong (China), Macau (China), Taiwan (China), Japan, South Korea, Mongolia, Vietnam, Laos, Singapore, Thailand, Philippines, Myanmar, Cambodia, Malaysia, Indonesia, India, Bangladesh, Nepal, Pakistan, Kuwait, Kyrgyzstan, Qatar, Israel, Türkiye, Iraq, Saudi Arabia, Oman, United Arab Emirates, Bahrain, Lebanon |
| Africa | Djibouti, Kenya, Madagascar, Mauritius, Egypt, South Africa             |
| Oceania | Australia, New Zealand                                             |
| Europe   | Belarus, Italy, Austria, Poland, Finland, Denmark, Belgium, Sweden, Spain, France, Netherlands, Germany, United Kingdom |

## Global Intelligent Scheduling

When accessing resources, a variety of factors including the ISP network, client region, and the network bandwidth of the IDC origin server might affect the response time and user experience.

Through real-time monitoring of the linkages across the entire network and leveraging Tencent Cloud's self-designed GSLB scheduling system and intelligent routing technology, CDN schedules users' access requests to the optimal edge nodes for acceleration. This ensures quick and stable resource access for users.

## Quick Configuration

You can use CDN to accelerate your services through a simple and quick configuration process, with no additional modification required on your end.

After registering your Tencent Cloud account and completing identity verification, you can activate the CDN service. Prepayment is not required. Add your business domain name on the CDN Console and wait for about 5 minutes for the domain name configuration to be distributed to cache nodes across the entire network. During this process, as the acceleration service has not taken effect yet, your business will not be affected.

When enabling the acceleration service, you need to modify the CNAME resolution configuration through your domain name service provider. Acceleration service will take effect when the DNS takes effect.

## A Variety of Features

CDN comes with an easy-to-use, full-featured console where you can change the configuration items and view monitoring data as needed:

**Domain management**

- You can add, delete, activate, and deactivate domain names.
- You can switch acceleration regions and select "Mainland China", "Outside Mainland China", or "Global" for the acceleration scope.
- You can customize the domain name list page to display, filter, and query configuration items.

**Domain configuration**

- You can configure an external origin server (IP list or domain names) or use COS as an origin server. Round robin, weighted origin-pull, and hot backup of origin server are supported.
- You can configure custom access control policies such as referer blacklist/whitelist, IP blacklist/whitelist, timestamp hotlink protection, and IP access frequency limit.
- You can customize the expiration time of node cache, status code cache, and HTTP header cache.
- CDN supports configuring optimizations for cross-border origin-pull linkage, range GETs, and 301/302 origin-pull follow-redirect.
- CDN supports HTTPS acceleration, HTTP/2 acceleration, and forced request redirection.
- You can configure the bandwidth cap and customize advanced configuration items such as HTTP response header, auto compression, and SEO.

**Purge cache**

- Self-service purging of the entire network’s cache is supported, as well as directory purge and URL purge.

**Real-time monitoring**

- CDN supports real-time monitoring of the bandwidth, traffic, traffic hit rate, number of requests, and all status codes generated by access requests at a granularity of 1 minute. The statistics can be filtered by project, domain name, province, ISP, and protocol to present a comprehensive view of service status.
- CDN supports real-time monitoring of the origin-pull bandwidth, traffic, number of requests, failure rate, and all status codes generated by origin-pull requests at a granularity of 1 minute. The statistics can be filtered by project or domain name to help you conveniently view the origin server status.
- You can view real-time reports of user distribution by region around the globe or by ISP in mainland China.
- CDN provides daily, weekly, and monthly operational reports to keep you updated on business fluctuations.

**Log service**

- All logs generated by access requests are grouped by hour and can be downloaded.
- CDN access logs can be collected and published in real time to quickly search and analyze log data.

**CDN APIs**
CDN provides [APIs](https://intl.cloud.tencent.com/document/product/228/31719) for all the supported features listed above to enable customized service usage. You and your team can conveniently manage, monitor, display, and analyze your business through these APIs.

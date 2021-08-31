Content Delivery Network (CDN) is a new layer of network architecture built on the existing internet. It consists of servers distributed around the globe to accelerate internet content delivery. These high-performance cache nodes store your content based on caching policies. When a user makes a content request, it will be routed to the node closest to the user, reducing access latency and improving availability.

CDN operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------|------|---------------------|
| Adding acceleration domain name           | cdn  | AddCdnDomain        |
| Creating SCDN domain name         | cdn  | CreateScdnDomain    |
| Creating SCDN log event task     | cdn  | CreateScdnLogTask   |
| Deleting acceleration domain name           | cdn  | DeleteCdnDomain     |
| Querying access data           | cdn  | DescribeCdnData     |
| Verifying SSL certificate and extracting its domain name | cdn  | DescribeCertDomains |
| Querying active user           | cdn  | DescribeIpVisit     |
| Querying origin-pull data           | cdn  | DescribeOriginData  |
| Querying SCDN domain name configuration       | cdn  | DescribeScdnConfig  |
| Querying SCDN data         | cdn  | DescribeScdnData    |
| Disabling URL           | cdn  | DisableCaches       |
| Querying the list of SCDN domain names       | cdn  | ListScdnDomains     |
| Querying the list of SCDN log download tasks   | cdn  | ListScdnLogTasks    |
| Querying top data          | cdn  | ListTopData         |
| Getting top SCDN data      | cdn  | ListTopScdnData     |
| Activating CDN          | cdn  | OpenCdnService      |
| Purging directory             | cdn  | PurgePathCache      |
| Purging URL           | cdn  | PurgeUrlsCache      |
| Prefetching URL           | cdn  | PushUrlsCache       |
| Enabling acceleration service           | cdn  | StartCdnDomain      |
| Enabling domain name security protection         | cdn  | StartScdnDomain     |
| Disabling acceleration service           | cdn  | StopCdnDomain       |
| Disabling domain name security protection         | cdn  | StopScdnDomain      |
| Modifying domain name configuration           | cdn  | UpdateDomainConfig  |
| Updating domain names in batches         | cdn  | UpdateDomainsHttps  |
| Modifying the image processing configuration of acceleration domain name     | cdn  | UpdateImageConfig   |
| Modifying billing type           | cdn  | UpdatePayType       |
| Modifying SCDN domain name configuration       | cdn  | UpdateScdnDomain    |

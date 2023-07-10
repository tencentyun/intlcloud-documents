### How do I enable CDN for COS?

For more information, see [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

### Does COS support CDN origin-pull with HTTPS?

Yes. For more information, see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).

### What is the difference between COS and CDN?

COS and CDN are two different products.

 Tencent Cloud [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436/6222) is a distributed storage service designed to store a massive number of files. It allows you to upload, download, and manage files in various formats for storage and management of massive amounts of data.
[Content Delivery Network (CDN)](https://intl.cloud.tencent.com/document/product/228) consists of high-performance cache nodes distributed around the globe to accelerate internet content delivery. These nodes store your content based on caching policies. When a user makes a content request, it will be routed to the node closest to the user, reducing access latency and improving availability.

You do not have to enable CDN when using COS. Using CDN in COS applies to the following scenarios:
- Scenarios that require low latency and high download speed
- Scenarios where gigabytes to terabytes of data need to be transmitted across regions, countries, and continents
- Scenarios where the same content needs to be downloaded frequently and repeatedly

For more information, see [CDN Acceleration Overview](https://intl.cloud.tencent.com/document/product/436/18669).

### Can frontend businesses access the content of COS by means of CDN and temporary key?

No. If you want to use CDN to access COS with private read/write permission on COS, see [CDN origin-pull authentication](https://intl.cloud.tencent.com/document/product/436/18670).

### Can I access private-read buckets via CDN acceleration?

Yes, but you need to be authorized with related configurations first. For more information, see [Private-read buckets](https://intl.cloud.tencent.com/document/product/436/18669#private-read-buckets).


### When a file is updated (re-uploaded or deleted) on COS, its cached content remains unchanged in CDN, resulting in inconsistency with the origin server. Can the cache in CDN be purged automatically when the file on COS is updated?

COS itself does not support automatic purging of CDN cache, a feature you should use with the help of Serverless Cloud Function (SCF). For more information, see [CDN Cache Purging](https://intl.cloud.tencent.com/document/product/436/37273).

### Can I use COS to upload files via a CDN acceleration domain name?

It is recommended that you do not use a CDN acceleration domain name as a custom domain name to upload files, because CDN itself is not used for accelerated upload. You are advised to use the global acceleration feature of COS to accelerate data upload and download. For more information on global acceleration, see [here](https://intl.cloud.tencent.com/document/product/436/33409).

### Does COS come with the CDN feature?

No. You need to configure the CDN feature yourself. For more information, see [Enabling Custom CDN Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).



This document describes how to use Tencent Cloud CDN to accelerate access to COS.


## Content Delivery Network (CDN)
By delivering resources to high numbers of globally deployed cache nodes and leveraging Tencent's independently developed GSLB scheduling system, CDN enables nearby access to required resources for end users. This reduces access delays caused by network congestion, distance, and ISP issues and effectively improves the download speed, responsiveness, and user experience.


## Cloud Object Storage (COS)
You can store all your static resources such as static scripts, audio/video files, images, and attachments in standard storage in COS, which features unlimited capacity and high-frequency reads/writes to provide scalable and reliable storage for static resources and reduce pressure on resource servers.


## Content Delivery Practices
CDN can accelerate global delivery of static resources such as static scripts, audio/video files, images, and attachments stored in COS. With CDN's global cache nodes and scheduling capabilities, frequently requested resources can be delivered to edge servers in advance. When they are accessed or downloaded by end users, the cached resources on a nearby node will be returned. This reduces both pressure on the origin server as well as transfer delay, significantly improving the user experience.
![](https://main.qcloudimg.com/raw/6316f3fde6226ad974d0bc17592c1425.png)

>! [Tencent Cloud Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/product/ecdn) can be used to accelerate the delivery of dynamic/static resources or dynamic resources stored in COS.


## Implementation

CDN acceleration can be implemented for COS in the following two ways. Choose either of them to complete acceleration：

- Point the COS endpoint to the CDN acceleration domain name and bind your domain name to the CDN acceleration domain name (through CNAME). For detailed directions, please see [Implementation via CDN Console](https://intl.cloud.tencent.com/document/product/228/32984).
- Bind your domain name to the COS endpoint and enable CDN acceleration. For detailed directions, please see [Implementation via COS Console](https://intl.cloud.tencent.com/document/product/228/32985).


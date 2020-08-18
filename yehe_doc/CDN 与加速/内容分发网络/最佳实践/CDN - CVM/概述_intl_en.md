This document describes how to use Tencent Cloud CDN to accelerate access to CVM.

## Content Delivery Network (CDN)
By delivering resources to high numbers of globally deployed cache nodes and leveraging Tencent's independently developed GSLB scheduling system, CDN enables nearby access to required resources for end users. This reduces access delays caused by network congestion, distance, and ISP issues and effectively improves the download speed, responsiveness, and user experience.

## Cloud Virtual Machine (CVM)
CVM provides scalable virtual computing resources in the cloud. You can launch CVM instances on different operating systems and load them into your custom application environment. As your business needs change, you can scale your computing resources in real time and adjust your CVM instance specifications accordingly.


## Content Delivery Practices

CDN can accelerate global delivery of static resources such as massive amounts of audio/video files, images, and files stored in CVM. With CDN's global cache nodes and scheduling capabilities, frequently requested resources can be delivered to edge servers in advance. When they are accessed or downloaded by end users, the cached resources on a nearby node will be returned.

CDN acceleration for CVM not only reduces the pressure on the origin server, transfer delay, and bandwidth costs, but also significantly improves the service availability.
![](https://main.qcloudimg.com/raw/66e176f86760440228d930e077f21247.png)

>! [Tencent Cloud Enterprise Content Delivery Network (ECDN)](https://intl.cloud.tencent.com/product/ecdn) can be used to accelerate the delivery of dynamic/static resources or dynamic resources stored in CVM.


## Implementation

CDN acceleration can be implemented for CVM in the following way:

Bind the CDN acceleration domain name to the CVM domain name or IP address and enable the CDN acceleration service. For detailed directions, please see [Implementation via CDN Console](https://intl.cloud.tencent.com/document/product/228/32988).

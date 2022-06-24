This document describes how to check whether the CLB WAF is running.

## Directions

1. By binding domain names to a CLB listener, WAF can protect traffic to the domain names passing through the CLB listener. To check whether the CLB WAF is running, ensure that your local computer can access the domain names added to different CLB instances.
>? To check whether the access to domain names added in CLB is normal for IPv4 domain name requests, see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). For IPv6 domain name requests, see [Getting Started with IPv6 CLB](https://intl.cloud.tencent.com/document/product/214/34560).
2. Open `http://wow.qcloudwaf.com/?test=alert(123)` in a browser.

>! `wow.qcloudwaf.com` is a sample domain name. Please replace it with the actual domain name that has been added.

![](https://qcloudimg.tencent-cloud.cn/raw/e45acf63d1c5bd6497b8b8b59e94bd97.png)




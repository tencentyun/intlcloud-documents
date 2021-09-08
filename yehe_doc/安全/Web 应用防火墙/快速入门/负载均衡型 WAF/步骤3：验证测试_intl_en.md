This document describes how to check whether the CLB WAF is running.
## Directions

1. By binding domain names to a CLB listener, WAF can protect traffic to the domain names passing through the CLB listener. To check whether the CLB WAF is running, ensure that your local computer can access the domain names added to different CLB instances.
>?To check whether an IPv4 domain name added to CLB can be accessed, see **Verifying the CLB Service** in [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975); to check the access of an IPv6 domain name, see **Step 4. Test IPv6 CLB** in [Getting Started with IPv6 CLB](https://intl.cloud.tencent.com/document/product/214/34560).
2. Open `http://wow.qcloudwaf.com/?test=alert(123)` in a browser.
>! `wow.qcloudwaf.com` is a sample domain name. Please replace it with the actual domain name that has been added.

![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)




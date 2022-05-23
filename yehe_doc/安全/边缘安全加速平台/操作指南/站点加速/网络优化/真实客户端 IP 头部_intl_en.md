## Overview

Real client IP header allows you to create a custom origin-pull HTTP request header that carries the real client IP information.

## Directions

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site acceleration** > **Network optimization** on the left sidebar.
>?The EdgeOne console is not yet fully available. To access the console, please [contact us](https://intl.cloud.tencent.com/contact-us) for activation.
> 
3. On the network optimization page, select a site and click ![](https://qcloudimg.tencent-cloud.cn/raw/8d3e9bac718473e40a340843b4cc7fb8.png) to enable the "Real client IP header" feature.
![](https://qcloudimg.tencent-cloud.cn/raw/975479021d5c361b038c2339a1709bba.png)
4. In the pop-up window, enter a header name, such as Tencent-Client-IP, and click **Save**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6a5b5cf7584ca3f8fd76270f8371b19e.png" style="zoom:80%;" />
>?The configuration on this page takes effect for all requests of the selected sites. To create a custom configuration for subdomain names or request paths, you can switch to [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151).


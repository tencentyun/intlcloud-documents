## Overview
This document describes how to obtain the public IP address of a CVM instance. 

## Directions
<dx-tabs>
::: Console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: In the primary IP column, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/> to copy the IP.
![](https://qcloudimg.tencent-cloud.cn/raw/de3e24445d11fca4fc194dd51462c406.png)
  - **Tab view**: On the instance page, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"/> after the public network address in "IP Address" to copy the public IP.
![](https://qcloudimg.tencent-cloud.cn/raw/1a719829bf4f09d9f4785a97f66abfd0.png)

<dx-alert infotype="notice" title="">
The public IP address is mapped to the private IP address through NAT. Therefore if you view the network interface attributes from within the instance (such as by using `ifconfig (Linux)` or `ipconfig (Windows)` commands), the public IP address is not displayed. To obtain the public IP from within the instance, you need to check the [instance metadata](#jump).
</dx-alert>


:::
::: API
See [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258).
:::
::: Instance metadata[](id:jump)
1. Log in to the CVM instance.
For more information, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/zh/document/product/213/5436) and [Logging in to Windows Instance](https://intl.cloud.tencent.com/document/product/213/41018).
2. Use the cURL tool or an HTTP GET request to access the metadata and obtain the public IP address.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
``` Check the public IP in the result:
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
For more information, see [Instance Metadata](https://intl.cloud.tencent.com/document/product/213/4934).
:::
</dx-tabs>

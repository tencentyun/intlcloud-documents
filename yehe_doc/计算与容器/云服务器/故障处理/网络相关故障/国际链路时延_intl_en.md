## Problem Description
The user experiences high latency when logging in to CVMs located in North America.

## Problem Analysis
Due to the limited number of international egress routers within the country, high concurrency may cause linkage congestion and unstable access. Tencent Cloud has reported this issue to ISPs.
If you need to manage within the country a CVM located in North America, you can purchase a CVM located in Hong Kong (China) and use it as a transfer point to log in to the CVM located in North America.

## Solution
1. Purchase a Windows CVM located in Hong Kong (China) as a **jump server**.
> 
> - In the “1. Select a model” of the “Custom Configuration” page, choose **Hong Kong, China**.
> [Click here to purchase >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1®ionId=5&zoneId=0&instanceType=S2ne.SMALL2&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=BANDWIDTH_PREPAID&loginSet=SET_PASSWORD)
> - Windows operating system supports login to both Windows and Linux CVMs located in North America, which is recommended to purchase.
> - **When purchasing the Windows CVM located in Hong Kong (China), you need to buy at least 1 Mbps bandwidth. Otherwise, you cannot log in to the jump server.**
>
2. After the purchase is completed, log in to the Windows CVM located in Hong Kong (China) based on your needs:
 - [Log in to the Windows instance using the RDP file](https://intl.cloud.tencent.com/document/product/213/5435)
 - [Logging into Windows instance via remote desktop](https://intl.cloud.tencent.com/document/product/213/32498)
 - [Logging into Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496)
3. Log in to your CVM located in North America from the Windows CVM located in Hong Kong (China) based on your needs:
 - Log in to a Linux CVM located in North America
    - [Log into Linux instance using standard login method](https://intl.cloud.tencent.com/document/product/213/5436)
    - [Logging into Linux instance via remote login tools](https://intl.cloud.tencent.com/document/product/213/32502)
    - [Logging into Linux instance via SSH key](https://intl.cloud.tencent.com/document/product/213/32501).
 - Log in to a Windows CVM located in North America 
    - [Log in to the Windows instance using the RDP file](https://intl.cloud.tencent.com/document/product/213/5435)
    - [Logging into Windows instance via remote desktop](https://intl.cloud.tencent.com/document/product/213/32498)
    - [Logging into Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).

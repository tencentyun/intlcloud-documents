## Introduction
Anti-DDoS Pro provides Tencent Cloud public IPs with stronger anti-DDoS capability. It supports Tencent Cloud services including CVM, CLB, NAT, WAF, etc.
You can change the IPs you want to protect by modifying the resources bound to an Anti-DDoS Pro instance.

## Prerequisites
Before changing the IPs you want to protect, make sure you have [purchased an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748) and [bound the instance to an IP](https://intl.cloud.tencent.com/document/product/1029/31750).

## Directions
1. Log in to [Anti-DDoS Pro Console](https://https://console.cloud.tencent.com/dayu/bgp_v2), choose **Resource List**, and select a region.
 - For single IP instances, select the **Single IP Instance** tab.
 - For multi-IP instances, select the **Multi-IP Instance** tab.
2. Click **Change Resource** in the Operation column to the right of the target instance.
3. On the **Bind Resource** page, select **Resource Type** and **select the resource(s) to be associated** according to your needs.
  - A single IP instance can only be bound to one resource.
	 ![](https://main.qcloudimg.com/raw/22904a13d680e76b8e158fc0a5b395b0.png)
 - For multi-IP instances, you can select multiple items in **Resource Type** and **Select resource(s) to be associated**. The number of resources selected in **Select resource(s) to be associated** cannot exceed the **Number of IPs** you set when [purchasing the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).
![](https://main.qcloudimg.com/raw/5f3d248141bb1ca481e267719f564521.png)
4. Click **OK**.

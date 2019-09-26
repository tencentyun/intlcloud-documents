## Operation Scenarios
Anti-DDoS Pro provides Tencent Cloud public network IP with stronger anti-DDoS capability. It supports Tencent Cloud services like CVM, CLB, NAT, and WAF.
You can change the protected object by modifying the bound resources of an Anti-DDoS Pro instance.

## Prerequisites
Before changing the protected object, make sure you have purchased Anti-DDoS Pro instance ([see here](https://intl.cloud.tencent.com/document/product/1029/31748)) and bound it with IPs of protected objects ([see here](https://intl.cloud.tencent.com/document/product/1029/31750)).

## Steps
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro** -> **Resource List**, and then select a region.
 - For Single IP instance, select the **Single IP Instance** tab.
 - For Multi-IP instance, select the **Multi-IP Instance** tab.
2. Click **Change Resource** in the line of the Anti-DDoS Pro instance.
3. On the **Bind Resource** page, select **Associated Resource Type** and **Select Associated Resource** according to the actual protection demand.
  - A Single IP instance can only be bound with one resource.
	 ![](https://main.qcloudimg.com/raw/22904a13d680e76b8e158fc0a5b395b0.png)
 - For Multi-IP instances, you can select multiple items in **Associated Resource Type** and **Associated Resource**. The number of **Associated Resource** cannot exceed **IP Number** set when you [purchase the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).
![](https://main.qcloudimg.com/raw/5f3d248141bb1ca481e267719f564521.png)
4. Click **OK**.

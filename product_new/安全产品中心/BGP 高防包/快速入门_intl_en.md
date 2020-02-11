Anti-DDoS Pro provides Tencent Cloud public IPs with higher anti-DDoS capability. It supports Tencent Cloud services such as CVM, CLB, NAT, and WAF. It is easy to access and requires no IP changes.
Currently, Anti-DDoS Pro offers two types of instances, single IP instances and multi-IP instances.
## Prerequisites
You need to [purchase an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748) before you can bind it to the IP addresses you want to protect.

## Directions
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and go to **Anti-DDoS Pro** > **Resource List**.
• For single IP instances, go to the **Single IP Instance** tab.
• For multi-IP instances, go to the **Multi-IP Instance** tab.
1. Select the region of the Anti-DDoS Pro instance you want to use and click **Bind Resource** to the right of the instance.
![](https://main.qcloudimg.com/raw/4fc76e35b8a449cd8a3606b86ca93998.png)
3. On the **Bind Resource** page, select **Resource Type** and resources you want to associate.
  - One single IP instance can only be bound to one resource.
	 ![](https://main.qcloudimg.com/raw/a6531effe9b2fa348ed7f67b515039d3.png)
 - For multi-IP instances, you can select multiple resource types and resources. The number of resources to be associated cannot exceed the **Number of IPs** you choose when [purchasing the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).
 ![](https://main.qcloudimg.com/raw/3b08e8d8e9dae86401eb3221ec2bbe47.png)

 > Only whitelisted users can bind hosted IPs to an Anti-DDoS Pro instance. If you need the feature, please [contact us](https://intl.cloud.tencent.com/support) or [submit a ticket](https://console.cloud.tencent.com/workorder/category) to get whitelisted.
4. Click **OK**.


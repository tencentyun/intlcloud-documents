## Operation Scenarios
Anti-DDoS Pro provides Tencent Cloud public IPs with stronger anti-DDoS capability. It supports Tencent Cloud services such as CVM, CLB, NAT, and WAF.
You can change or unbind the protected IPs bound to Anti-DDoS Pro instances based on your actual business needs.

## Prerequisites
You need to purchase an Anti-DDoS Pro instance and [bind a protected IP](https://intl.cloud.tencent.com/document/product/1029/31750) to it before you can change or unbind protected IPs

## Directions
### Changing the IPs to be protected
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** > **Resource List** on the left sidebar, and select a region at the top.
 - For single IP instances, select the **Single IP Instance** tab.
 - For multi-IP instances, select the **Multi-IP Instance** tab.
2. Click **Change Resource** in the "Operation" column to the right of the target instance.
3. On the **Bind Resource** page, select **Resource Type** and **Resources to Associate** according to your needs.
  - A single IP instance can only be bound to one resource.
	  -If your Anti-DDoS Pro instance is a multi-IP instance, you can select multiple options for **Resource Type** and **Resources to Associate**. The number of resources cannot exceed the **number of IPs** set when the instance is purchased.
4. Click **OK**.

### Unbinding protected IPs
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** > **Resource List** on the left sidebar, and select a region at the top.
	- For single IP instances, select the **Single IP Instance** tab.
	- For multi-IP instances, select the **Multi-IP Instance** tab.
2. Click **More** > **Unbind** in the "Operation" column to the right of the target instance and click **OK** in the pop-up dialog box.

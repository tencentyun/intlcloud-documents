
Anti-DDoS Pro provides Tencent Cloud public IPs with stronger anti-DDoS capability. It supports Tencent Cloud services including CVM, CLB, NAT, and WAF.
You can add protected IPs to or delete them from Anti-DDoS Pro instances as needed.
## Prerequisite
You have set a protected IP and purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance.

## Directions
1. Log in to the [Anti-DDoS Pro (New) Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Service Packs** on the left sidebar.
2. Click the **Protected Resource** on the right of the target Anti-DDoS Pro instance.
3. On the **Protected Resource** page, select a resource type and a resource instance as needed.
  - Resource type: supports public cloud resources with public IPs such as CVM, CLB, and WAF.
  - Select resource: to add one or more resource instances to the protected IP, tick the checkbox for the resource ID. The number of selected resource instances cannot exceed the number of protected IPs that can be bound.
  - Selected: to delete the selected resource instance, click **Delete** on the right of it.
	![](https://main.qcloudimg.com/raw/cec2b2d9446ecd8bfeea22656b8311d4.png)
>?Unbinding a blocked IP from Anti-DDoS Pro instances is not allowed.
4. Click **OK**.



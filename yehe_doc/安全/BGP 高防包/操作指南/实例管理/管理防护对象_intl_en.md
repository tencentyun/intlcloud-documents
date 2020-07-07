
Anti-DDoS Pro provides Tencent Cloud public IPs with stronger anti-DDoS capability. It supports Tencent Cloud services such as CVM, CLB, NAT, and WAF.
You can add or remove the protected IPs bound to Anti-DDoS Pro instances based on your actual business needs.

## Prerequisites
You need to [purchase an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/36115) and set the protected object's IP first.

## Directions
1. Log in to the [new Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Anti-DDoS Pro Instance** on the left sidebar.
2. Click **Manage Protected Object** in the "Operation" column on the right of the target instance.
3. On the **Manage Protected Object** page, select "Resource Type" and "Resource Instance" as needed.
  - Resource Type: resources with public IPs in the public cloud are supported, such as CVM, CLB, and WAF.
  - Resource Instance: click the checkbox before a resource ID to add the resource as a protected object of the Anti-DDoS Pro instance. You can select multiple instances (no more than the number of bindable IPs).
  - Selected: click the "Delete" icon after a resource to remove it from the list of protected objects of the Anti-DDoS Pro instance.
	![](https://main.qcloudimg.com/raw/cec2b2d9446ecd8bfeea22656b8311d4.png)
4. Click **OK**.



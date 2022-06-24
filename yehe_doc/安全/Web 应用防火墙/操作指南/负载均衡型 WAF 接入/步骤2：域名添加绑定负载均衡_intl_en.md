This document describes how to bind a domain name to a CLB instance in the WAF console.

## Directions

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Asset Center** > **Domain Name List** on the left sidebar.
2. On the domain name list page, click **Add domain name**, configure relevant parameters, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/7951e99bbdc30affdf236e6e5988238e.png)

**Field description**
 - **Instance**: Select the CLB type and an instance name.
 - **Domain name**: Enter the domain name to be protected, such as `clb.technicalsupport.cn`.
 - **Proxy**: Select whether proxy services including Anti-DDoS and CDN are used based on the actual conditions.

>?If you select **Yes**, WAF will get real client IPs, which may be forged, from the XFF field as the source IPs.

 - **Chinese Mainland regions:** Select as needed.
 - **Global regions:** Select as needed.
 - **CLB listener**: Select as needed.

3. Click **OK** to return to the domain name list, where you can view the protected domain name `clb.technicalsupport.cn` and the ID, name, VIP, and listener information of the CLB instance.
![](https://qcloudimg.tencent-cloud.cn/raw/6f5890f34608445292250c4f69a4dd47.png)

## Subsequent Operations
After the domain name is bound to a CLB instance, you can proceed to [Step 3. Verify the Configuration](https://intl.cloud.tencent.com/document/product/627/34721).

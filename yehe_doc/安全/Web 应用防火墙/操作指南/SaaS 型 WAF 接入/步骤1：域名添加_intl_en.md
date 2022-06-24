This document describes how to connect a domain name to SaaS WAF. Before using WAF to protect your web business, you need to connect the website to WAF; otherwise, WAF protection cannot take effect.

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Asset Center** > **Domain Name List** on the left sidebar.
2. Click **Add domain name**.
3. On the page that appears, configure the basic parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/747c84043ef0ae7fa6dbab5539be46fe.png)

**Field description**
 - **Instance:** Select **SaaS** and the target instance on the right.
 - **Domain name**: Enter the domain name to be protected, such as `saas.technicalsupport.cn`.
 - **Server configuration**: Select a protocol and port as needed. For more port options, see [Port Access](https://intl.cloud.tencent.com/document/product/627/47411).
   - Select the **HTTP** protocol and enter a port.
   - Select the **HTTPS** protocol and enter a port. Then, you need to configure the associated certificate, forced HTTPS redirection, and HTTPS forwarding method.
      - Associate certificate: Click **Associate certificate** and select a Tencent Cloud-managed or external certificate as needed.
      - Force HTTP redirect: To enable forced HTTPS redirect, you need to select both HTTP and HTTPS access protocols.
      - HTTPS origin-pull method: Select an origin-pull method as needed: HTTP or HTTPS.

>?For HTTP as an origin-pull method, you can specify a port for origin-pull. For HTTPS, the open port is also used for origin-pull.

 - **Proxy:** Select whether proxy services including Anti-DDoS and CDN are used based on the actual conditions.

>?If you select **Yes**, WAF will get real client IPs, which may be forged, from the XFF field as the source IPs.

 - **Origin address:** Enter the IP or domain name as needed.
    - **IP:** Enter up to 20 IPv4 or IPv6 addresses and separate them with line breaks.
    - **Domain name:** Enter the origin domain name. Note that it must be different from the protected domain name.
    - **Weighted round robin:** Use this method when you set multiple origin server IPs for forwarding.
 - **Load balancing policy:** Select RR (default option) or IP hash as needed.

4. After configuring the basic parameters, you can configure advanced parameters as needed. Click **OK** to save the settings.
 ![](https://qcloudimg.tencent-cloud.cn/raw/1913a958424173c89c4aa04914f8f8c9.png)

**Field description**
 - **Connection method**: Persistent connection is used for forwarding by default. Make sure that the origin server supports persistent connection; otherwise, even if persistent connection is selected, non-persistent connection will still be used.
 - **Enable HTTP 2.0**: Make sure that your origin server supports HTTP 2.0 and enable it; otherwise, even if HTTP 2.0 is enabled, it will be downgraded to 1.1.
 - **Enable WebSocket**: If your website uses WebSocket, we recommend you select **Yes**. 
 - **Enable Anycast IP**: All instances in the same region under the current account use the same Anycast IP.

5. After the configuration, you can see the newly added domain name in the domain name list. The current page prompts that you haven't configured a CNAME record. You need to [perform local testing](https://intl.cloud.tencent.com/document/product/627/35652) and then [modify DNS resolution](https://intl.cloud.tencent.com/document/product/627/35653).
![](https://qcloudimg.tencent-cloud.cn/raw/998a5ab556a792d5d23092ec11003231.png)

>?WAF assigns a unique CNAME to each domain name added to WAF regardless of whether it is top-level or second-level.

## Subsequent Operations
After adding a domain name, you can proceed to the following steps:
- [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652)
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/document/product/627/35654)

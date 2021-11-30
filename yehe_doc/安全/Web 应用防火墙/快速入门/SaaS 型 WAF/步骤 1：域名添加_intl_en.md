This document describes how to add a domain name in the WAF console.
## Directions
To enable WAF detect the target domain name, you need to add it in the WAF console. The following takes `waf.qcloudwaf.com` as an example in configuration.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Instance Management** -> **Instance List** on the left sidebar to enter the instance list.
2. Select an instance for the domain name, and click **Domain Name Connection** to enter the domain name connection page.
3. Click **Add domains** to enter the basic setting page.

  - **Domain configuration**
     1. For **Domain Name**, enter the domain name to be protected, for example, `waf.qcloudwaf.com`.
     2. Select a protocol and port as needed. For example, select HTTP and port 80, or select HTTPS and port 443.
     3. Select an origin-pull method as needed: HTTP or HTTPS.
     >?For HTTP as an origin-pull method, you can specify a port for origin-pull. For HTTPS, the open port is also used for origin-pull.
     4. Select a Tencent Cloud hosting certificate or your own certificate as needed.
     5. For **Real Server Address**, enter the public IP address or domain name of the real server of the website to be protected.   
 - **Other configurations**
 If you have connected your domain name to an intermediate proxy device before WAF is used, select **Yes**. Otherwise, select **No**.
3. Click **Save** to complete the configuration. You can view the added domain name in the domain name list.
4. Click the domain name to enter its details page, where you can see the CNAME assigned by WAF.

>?WAF assigns a unique CNAME to each domain name added to WAF regardless of whether it is top-level or second-level.

## Subsequent Operations
After adding a domain name, you can proceed to the following steps:
- [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652)
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/document/product/627/35654)

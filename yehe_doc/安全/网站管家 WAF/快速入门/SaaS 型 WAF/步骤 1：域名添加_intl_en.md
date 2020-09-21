In order for WAF to recognize a domain name to be protected, you need to add it to WAF first. The following uses protection of `waf.qcloudwaf.com` as an example to describe how to configure a domain name.
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the domain name configuration page.
2. Click **Add Domain Name** to enter the basic configuration page.
![](https://main.qcloudimg.com/raw/9e14c97169bacf7fca99411c5278457b.png)
 - **Domain name configuration**
     1. In the "Domain Name" input box, enter the domain name to be protected, which is `waf.qcloudwaf.com` in this example.
     2. Select the protocol and port as needed; for example, you can select HTTP and port 80 or select HTTPS and port 443.
     3. You can select HTTP or HTTPS as the HTTPS origin-pull method.
>?You can specify an origin-pull port for HTTP, which is the same as the open port for external connections. But you cannot specify an origin-pull port for HTTPS.
     4. You can select a Tencent Cloud-hosted certificate or your own certificate.
     5. In the "Real Server IP" input box, enter the actual IP address of the real server of the website to be protected, i.e., public IP address of the real server.
 - **Other configurations****
 If there is another intermediate proxy device connected before WAF, select **Yes**; otherwise, select **No**.
3. Click **Save** to complete the configuration. Then, you can view the domain name just added in the domain name list.
4. Click the domain name to enter its details page. You can view the CNAME record allocated to the website by WAF.
 ![](https://main.qcloudimg.com/raw/9541ea01c087959b5f2882ca846faa02.png)
>?WAF will allocate a unique CNAME record to each domain name added to WAF (no matter whether it is top-level or second-level).

1. Make sure that your local computer can properly access the website.
2. Enter the address `http://wow.qcloudwaf.com/?test=alert(123)` in your browser to access it.
>!`wow.qcloudwaf.com` is the domain name used in this example, which should be replaced with the one you actually added.
3. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/attack) and select **Web Application Firewall** > **Attack Details** on the left sidebar to enter the attack log query page; then, click **CLB WAF** to query CLB protection logs.
4. Select the protected domain name just added and click **Query**. If the attack type is "XSS attack", the WAF configuration has taken effect.
![](https://main.qcloudimg.com/raw/02c681b1624a804d85c72f4ac97b91ec.png)
>?If the domain name is not configured with DNS, you can verify the connection validity as instructed in [Step 2. Verify and Test](https://cloud.tencent.com/document/product/627/18632) in Getting Started with SaaS WAF.

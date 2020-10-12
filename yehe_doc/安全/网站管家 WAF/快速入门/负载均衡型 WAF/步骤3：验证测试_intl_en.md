1. By binding domain names to a CLB listener, WAF can protect traffic to the domain names passing through the CLB listener. To check whether the CLB WAF is running, ensure that your local computer can access the domain names added to different CLB instances.
>? To check whether the access to domain names added in CLB is normal for IPv4 domain name requests, see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). For IPv6 domain name requests, see [Getting Started with IPv6 CLB](https://intl.cloud.tencent.com/document/product/214/34560).
2. Enter the URL `http://wow.qcloudwaf.com/?test=alert(123)` in your browser to access the monitoring website.
>! `wow.qcloudwaf.com` is a sample domain name. Please replace it with the actual domain name that has been added.
3. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/attack). In the left sidebar, choose **Log Services** > **Attack Logs** to go to the attack log query page.
4. Select a protected domain name and click **Search**. If the attack type appears as "XSS attack", the WAF configuration has taken effect.
![](https://main.qcloudimg.com/raw/5bb81ca8874cb8723b6638b83351b729.png)

This document describes how to check whether the CLB WAF is running.
### Directions

1. By binding domain names to a CLB listener, WAF can protect traffic to the domain names passing through the CLB listener. To check whether the CLB WAF is running, ensure that your local computer can access the domain names added to different CLB instances.
>?To check whether an IPv4 domain name added to CLB can be accessed, please see **Verifying the CLB Service** in [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
2. Open `http://wow.qcloudwaf.com/?test=alert(123)` in a browser.
>! `wow.qcloudwaf.com` is a sample domain name. Please replace it with the actual domain name that has been added.
3. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/attack), click **Log Services** -> **Attack Logs** in the left sidebar to search for logs.
4. Select a protected domain name and click **Search**. If the attack type appears as **XSS attack**, the WAF configuration has taken effect.



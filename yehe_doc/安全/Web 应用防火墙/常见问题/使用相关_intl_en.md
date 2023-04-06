### How do I download access logs of the last 180 days?
When Access Logs is enabled, WAF stores the logs for at least 180 days. You can query and download access logs of the last 30 days. To download logs of the last 180 days, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2).

### Does WAF support health check?
Yes. WAF checks the status of all real server IPs at L4 and L7. If a real server fails the health check too many times and exceeds the check threshold, it will be isolated. For more information, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2).

### Does WAF support session persistence?
Yes。 WAF supports session persistence. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&level3_id=867&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=15&scene_code=29995&step=2) to activate this feature.

### Will logging still be available once WAF is disabled for the domain name list?
No. Once WAF is disabled, all its protection features are unavailable, and only the traffic forwarding mode starts to run instead, with no logs recorded.

### When will a configuration change take effect?
In general, a configuration change takes effect within 10 seconds.
>? It applies to connection configurations (including setting the real server, link mode, and whether to enable HTTP2.0).

### The VIP of WAF-protected domain name is blocked due to DDoS attacks. What should I do?
WAF VIP addresses come with 2-GB Anti-DDoS Basic protection bandwidth. When you need to recover your business immediately after the VIP is blocked, purchase an [Anti-DDoS Pro](https://console.cloud.tencent.com/ddos/ddos-pro/protection-config) instance and bind it to the VIP address.

### If the uploaded files are blocked, will they still be blocked with HTTPS or SFTP?
If WAF is disabled, the file will not be blocked. If WAF is enabled and the blocking mode is set, WAF will block malicious files uploaded over HTTP or HTTPS, but will not block files uploaded over SFTP. SFTP is a non-HTTP or non-HTTPS protocol beyond the protection of WAF.

### Will the persistent connection be disconnected when the WAF certificate is changed?
No. Updating the certificate will reload nginx, and the thread will not be recycled until the end of the old request session, so it will not be disconnected.

### What cipher suite does the SaaS WAF or CLB WAF support?
- SaaS WAF does not support SSL cipher suites.
- CLB WAF supports:
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK
- WAF supports the following TLS versions:
	- TLSv1, TLSv1.1, and TLSv1.2.
	- Cipher suites: EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5.
>?
>- SaaS WAF supports ECDHE cipher suites by default (such as TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA).
>- Customization for TLS protocol and cipher suite is available in the Exclusive edition.

### How do I query the module hit by a block page?
1. When a malicious request is detected, WAF blocks the request and returns a block page with a UUID.
![](https://qcloudimg.tencent-cloud.cn/raw/9b640ca21de15ff9a3acb243edfe1c14.png)
2. You can copy the UUID and search for it on the [Attack Logs page](https://console.cloud.tencent.com/guanjia/tea-attacklog).
>?
>- Specify the query period.
>- Check information of the hit rule in the log fields: `attack_type`, `rule_id`, and `attack_content`.

![](https://qcloudimg.tencent-cloud.cn/raw/d3fa8e94f8cea3fd660fc8425dbfbfef.png)

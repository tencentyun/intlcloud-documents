### Does WAF support health check?
Health check is enabled for WAF by default. WAF checks the connection status of all real server IPs. For the real server IP that does not respond, WAF will not forward requests to this IP until its connection status becomes normal.

### Does WAF support session persistence?
Session persistence is supported and enabled by default in WAF.

### Will logging still be available once WAF is disabled for the domain name list?
Once WAF is disabled, all its protection features are unavailable, and only the traffic forwarding mode starts to run instead, with no logs recorded.

### When will a configuration change take effect?
In general, a configuration change takes effect within 10 seconds.
>?It applies to connection configurations (including setting the real server, link mode, and whether to enable HTTP2.0), instead of protection configurations.

### What should I do if the VIP address of my WAF-protected domain name is blocked due to DDoS?
WAF provides anti-DDoS Basic capabilities (2 G) for VIP addresses by default. In case of an urgent need to resume your business for a VIP address blocked by anti-DDoS Basic, you can:
- Log in to the [DDoS Protection Console](https://console.cloud.tencent.com/ddos/unblock/list), and unblock the VIP address manually. You are allowed to do so three times each month.
- Or buy a [Anti-DDoS Pro](https://console.cloud.tencent.com/ddos/ddos-pro/protection-config) instance, and bind it to your WAF-protected VIP address.

You are allowed to remove blocking manually only three times per month. The system resets the count of blocking removals at zero o'clock on the 1st day of every month, and the remaining number of allowed removals from last month is not carried over to this month.

### If the uploaded files are blocked, will they still be blocked with HTTPS or SFTP?
If WAF is disabled, the file will not be blocked. If WAF is enabled and the blocking mode is set, WAF will block malicious files uploaded over HTTP or HTTPS, but will not block files uploaded over SFTP. SFTP is a non-HTTP or non-HTTPS protocol beyond the protection of WAF.


### Will the persistent connection be disconnected for changing the WAF certificate?
No. Renewing the certificate will reload nginx, and the thread will not be recycled until the end of the old request session, so it will not be disconnected.

### What cipher suite does the SaaS WAF or CLB WAF support?
- SaaS WAF does not support setting SSL cipher suites.
- CLB WAF supports:
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK
- WAF supports the following TLS versions:
	- TLSv1, TLSv1.1, and TLSv1.2.
	- Cipher suite: EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5.
>?Customization for TLS protocol and cipher suite is available in the Dedicated edition.

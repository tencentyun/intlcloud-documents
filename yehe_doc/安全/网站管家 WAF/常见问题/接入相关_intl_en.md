### Is WAF available to servers outside Tencent Cloud?

 WAF can be connected with servers in data centers outside Tencent Cloud. WAF protects servers in any public networks, including but not limited to Tencent Cloud, and clouds and IDCs from other vendors. 
>! Domain names connected in the Chinese mainland must be ICP filed as required by the Ministry of Industry and Information Technology of China.

### Does WAF support HTTPS protection?

WAF fully supports HTTPS services. You just need to upload the SSL certificate and private key as instructed or select the Tencent Cloud-hosted certificate to use WAF for HTTPS traffic protection.

### Does the WAF QPS limit apply to the entire instance, or to a single domain name?
The QPS limit in WAF is for the entire instance. For example, if three domain names are protected, the total QPS of the three domain names cannot exceed the limit. If the QPS limit of the purchased instance is exceeded, speed will be limited and packets will be lost.

### Can the real server IP added to WAF be the private IP of a Tencent Cloud CVM instance?
When adding a domain name to WAF, the real server address must be a domain name or a public IP, such as CVM public IP, CLB public IP, or Egress IP of other local IDCs, while a CVM private IP is not supported.

### Can Anti-DDoS Pro instances be used for WAF?
Yes, you can empower WAF with high DDoS protection capability simply by selecting IPs specified in a WAF instance on the configuration page in the Anti-DDoS Pro console. For more information, please see [Combination of Anti-DDoS Pro and Web Application Firewall](https://intl.cloud.tencent.com/document/product/1029/31768).

### How to use WAF together with CDN or Anti-DDoS Pro services?
- You can use WAF with Anti-DDoS Pro directly, or use it with CDN by setting the CDN origin server IP as the IP of a WAF instance. Recommended deployment architecture: Client -> CDN -> WAF + Anti-DDoS Pro -> CLB -> Real server.
- If you need the CDN and Anti-DDoS capabilities, simply set the CNAME provided after the connection to WAF as the CDN origin server, and associate Anti-DDoS Pro with the WAF instance. In this way, the user traffic, after going through CDN, is forwarded to WAF, which has the capability of cleansing high-traffic DDoS attacks, and finally reaches the real server for full protection.

### How many forwarding IPs can be set for one protected domain name in WAF?
Up to 20 forwarding IPs can be set for one protected domain name in WAF.

### How does the traffic balancing work when multiple real servers are configured in WAF?
If multiple forwarding IPs are configured, WAF achieves load balancing for access requests by polling.

### Does WAF support health check?
Health check is enabled for WAF by default. WAF checks the connection status of all real server IPs. For the real server IP that does not respond, WAF will not forward requests to this IP until its connection status becomes normal.

### Does WAF support session persistence?
Session persistence is supported and enabled by default in WAF.

### How long does it take for configuration changes to take effect in the WAF console?

In general, a configuration change takes effect within 10 seconds.

### Does WAF automatically add a forwarding IP range to a security group?

WAF does not automatically add a forwarding IP range to a security group. To do so, please see [Getting Started](https://intl.cloud.tencent.com/document/product/627/18635).

### If the uploaded files are blocked, will they still be blocked with HTTPS or SFTP?

If WAF is disabled, the file will not be blocked. If WAF is enabled and the blocking mode is set, WAF will block malicious files uploaded over HTTP or HTTPS, but will not block files uploaded over SFTP. SFTP is a non-HTTP or non-HTTPS protocol beyond the protection of WAF.

### Is the SSL mutual authentication supported by both the SaaS WAF and CLB WAF?
It is supported by CLB WAF but not by SaaS WAF.

### What cipher suite does the SaaS WAF or CLB WAF support?
- SaaS WAF does not support setting SSL cipher suites.
- CLB WAF supports:
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK
- WAF supports the following TLS versions:
	- TLSv1, TLSv1.1, and TLSv1.2.
	- Cipher suite: EECDH+CHACHA20:EECDH+AES128:RSA+AES128:EECDH+AES256:RSA+AES256:EECDH+3DES:RSA+3DES:!MD5.
	>?Customization for TLS protocol and cipher suite is available in the Dedicated edition.

### Can non-Tencent Cloud servers use Web Application Firewall (WAF)?

 WAF can be connected with servers in data centers outside Tencent Cloud. WAF protects servers in any public networks, including but not limited to Tencent Cloud, and clouds and IDCs from other vendors. 
>Domain names connected in Mainland China must be ICP licensed as required by MIIT.

### Does WAF support HTTPS protection?

WAF fully supports HTTPS services. You just need to upload the SSL certificate and private key as instructed, or select the Tencent Cloud hosting certificate to make WAF protect HTTPS traffic.

### Does the WAF QPS limit apply to the entire instance, or to a single domain name?
The QPS limit in WAF is for the entire instance. For example, if three domain names are under protection of the WAF, the total QPS of the three domains names cannot exceed the upper limit. If the QPS limit of the purchased instance is exceeded, speed limit is triggered, which will result in packet loss.

### Can the real server IP added to WAF be a private IP in Tencent Cloud CVM?
When adding a domain name to WAF, you must enter a public IP or domain name as real server address, including CVM public IP, CLB public IP, or Egress IP from other local IDCs, and cannot enter a CVM private IP.

### Can WAF use Anti-DDoS Pro directly?
Yes, you can empower WAF with high DDoS protection capability simply by selecting IPs specified in a WAF instance in the Anti-DDoS Pro console configuration page. For more information, please see [Anti-DDoS Pro access practice](https://intl.cloud.tencent.com/document/product/1029/31768).

### How does WAF connect with CDN or Anti-DDoS Pro?
- WAF can be associated directly with Anti-DDoS Pro as long as the CDN origin server points to the IP specified in the WAF instance. The best deployment architecture is: client > CDN > WAF + Anti-DDoS Pro > CLB > real server.
- If you need the CDN and Anti-DDoS capabilities, simply set the CNAME provided after the connection to WAF to CDN origin server, and associate Anti-DDoS Pro with the WAF instance. The user traffic, after going through CDN, is forwarded to WAF, which has the capability of cleaning high-traffic DDOS attacks, and finally reaches the real server for full protection.

### How many intermediate IPs can I set for a WAF-protected domain name?
You can set up to 20 ones for a WAF-protected domain name.

### How does WAF handle load when configuring multiple real servers?
In case of multiple intermediate IPs, WAF will load balance access requests with Round Robin algorithm.

### Does WAF support health check?
In WAF, health check is enabled by default. WAF will detect if any real server IP is inaccessible. If a real server IP does not respond, WAF will stop forwarding requests to this IP until it goes back to normal.

### Does WAF support session persistence?
Session persistence is enabled in WAF by default.

### How long does it roughly take for a configuration change to take effect in the WAF console?

In general, a configuration change takes effect within 10 seconds.

Will WAF automatically add an intermediate IP range to a security group?

No, WAF won’t automatically add an intermediate IP range to a security group. To add intermediate IPs to a security group, see [Getting Started with WAF](https://intl.cloud.tencent.com/document/product/627/18635).

### If the uploaded files are blocked, will they still be blocked with HTTPS or SFTP?

They won’t be blocked if WAF is disabled. However, if you enable block mode in WAF, it blocks malicious files uploaded with HTTP or HTTPS, but does not block any files uploaded with SFTP, a non-HTTP or -HTTPS protocol beyond protection of WAF.

### Do SaaS WAF and CLB WAF support SSL mutual authentication?
CLB WAF supports SSL mutual authentication, while SaaS WAF does not.

### Which cipher suites are supported by SaaS WAF and CLB WAF?
- SaaS WAF does not support SSL cipher suite settings.
- CLB WAF supports the following cipher suite.
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK

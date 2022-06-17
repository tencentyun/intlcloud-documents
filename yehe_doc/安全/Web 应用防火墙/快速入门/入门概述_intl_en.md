This document describes how to quickly deploy and use a WAF instance. Specifically, purchase a WAF instance, organize the website domain name information, perform domain name connection and protection configuration, and get an overview of the business and security through the reports and stay on top of security status. You can view traffic processing details in attack logs and then adjust the protection configuration accordingly to meet special business needs. You can also use CM to configure different types of custom alarms and notification channels for more efficient Ops.

## Step 1. Purchase an instance 
You can purchase multiple WAF instances. Multi-instance management better suits your business division and management requirements and allows you to achieve nearby access and protection of multi-region active-active instances in a unified manner.
- For more information on instance purchase, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/627/11730).
- For more information on instance management and renewal, see [Instance Management](https://intl.cloud.tencent.com/document/product/627/47530).

## Step 2. Connect your website 
There are SaaS WAF and CLB WAF instances.

### Domain name connection guide for SaaS WAF
To protect your website, SaaS WAF assigns a CNAME to your domain name under protection, modifies the DNS resolution record of your website, and forwards the web requests received by your website to WAF. Used with security groups, SaaS WAF can prevent direct attacks toward the real server of your website. To achieve the above, you need to follow the steps below:
 - [Step 1. Add a domain name](https://intl.cloud.tencent.com/document/product/627/35651)
 - [Step 2. Perform local testing](https://intl.cloud.tencent.com/document/product/627/35652)
 - [Step 3. Modify DNS resolution](https://intl.cloud.tencent.com/document/product/627/35653)
 - [Step 4. Set a security group](https://intl.cloud.tencent.com/document/product/627/35654)
 - [Step 5. Verify the configuration](https://intl.cloud.tencent.com/document/product/627/42223)

### Domain name connection guide for CLB WAF
CLB WAF associates with Tencent Cloud Layer-7 CLB (listener) cluster by your domain name, and detects and purges HTTP or HTTPS traffic that goes through the CLB instance for side-channel threats. In this way, it can provide protection without interrupting your traffic forwarding. To achieve the above, you need to follow the steps below:
 - [Step 1. Confirm CLB configuration](https://intl.cloud.tencent.com/document/product/627/34719)
 - [Step 2. Bind a domain name to the CLB instance](https://intl.cloud.tencent.com/document/product/627/34720)
 - [Step 3. Verify the configuration](https://intl.cloud.tencent.com/document/product/627/34721)

## Step 3. Configure the protection 
WAF will protect the traffic to the connected website. It has multiple detection and protection modules to help your website tackle different types of security threats. The rule engine is enabled by default and used to defend against common web application attacks such as SQL injection, XSS, and web shell upload. Other modules can be enabled and configured with protection rules manually as needed.


## Step 4. Analyze logs
By default, WAF logs attacks only. After purchasing and activating the log service, you can have all access requests logged by domain name.

### Attack log
An attack log records the time, source IP, type, and details of an attack to facilitate real-time threat check and analysis as well as protection policy adjustment, fully meeting the needs of routine security Ops and business.

Currently, attacks are displayed in an aggregated manner; that is, logs of the same type from the same request source IP within a specific period are displayed as one log to reduce your Ops workload and improve the efficiency. Additionally, you can query attack logs with full-text search, fuzzy search, and search by filter. For more information, see [Attack Logs](https://intl.cloud.tencent.com/document/product/627/35649).

### Access log
Access logging is used to record access logs of domain names protected by WAF. It allows you to query and download access logs generated in the last 30 days and retain them for at least 180 days. For more information, see [Access Log](https://intl.cloud.tencent.com/document/product/627/35648).

## Step 5. Generate a security report
After your website is connected to WAF for protection, you can go to the WAF overview page to query the current total number of domain names, connected website conditions, instance conditions, website business and attack traffic analysis data in the last 30 days, and rule updates. In this way, you can have a better picture of the overall security of your website business. For more information, see [Access Log](https://intl.cloud.tencent.com/document/product/627/35648).

## Step 6. Configure alarms in CM
After your website is connected to WAF protection, you can configure alarms in CM. Then, WAF will send you alarm notifications when exceptions are detected in the website request traffic and business traffic, so you can stay informed of your business security changes. In this way, you can quickly respond to exceptions and adjust WAF policies to ensure business stability and security. For more information, see [WAF Alerting with Cloud Monitor](https://intl.cloud.tencent.com/document/product/627/42222).

You can configure the same domain name into instances of the same type in different regions to separate the connection configurations of forwarding and protecting resources while using the same protection policy.

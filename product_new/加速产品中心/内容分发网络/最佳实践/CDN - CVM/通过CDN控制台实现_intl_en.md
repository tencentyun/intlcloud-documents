This document describes how to accelerate access to CVM instances through CDN in the console.

## Prerequisites
1. You have signed up for a Tencent Cloud account and verified your identity.
2. You have activated the CVM service. For more information, please see [Getting started with CVM](https://intl.cloud.tencent.com/document/product/213/2936).


## Operation Guide

### Adding a domain name

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar to enter the domain name management page, and click **Create Distribution**.
![](https://main.qcloudimg.com/raw/d301ff1eea5fe534ce09ec5964e8c82b.png)

### Configuring the domain name
![](https://main.qcloudimg.com/raw/ec7ea324171295b8fd0321e226d0e0a3.png)
1. Enter the **domain name** to be accelerated.
Wildcard domain names are supported, such as `*.test.com`. Up to 10 domain names can be connected in batches in one single operation.
The domain name should meet the following conditions:
	- ICP filing for the domain name has been obtained from the MIIT
	- The domain name has never been connected to Tencent Cloud CDN
2. Select the **project** of the domain name.
The project is shared by all Tencent Cloud products. You can add a project in [Project Management](https://console.cloud.tencent.com/project).
3. Select **Origin Server Type** and enter the **Origin Server Configuration**.
For more information on origin server types, please see [Connecting domain names to CDN](https://intl.cloud.tencent.com/document/product/228/5734).
Enter your **CVM public network address** in the origin server settings.

### Configuring the acceleration service

Based on your business needs, select **Business Type** and set **Basic Configuration** and **Cache Expiration Configuration**.
![](https://main.qcloudimg.com/raw/6264633c18801547e4aece61a94009cb.png)
1. **Business Type**
The business type determines the resource platform to be scheduled by the domain name. The acceleration configuration varies by resource platform. Please select a business type based on your business conditions:
	- Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
	- Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
	- Streaming VOD acceleration: Suitable for VOD acceleration scenarios.
2. **Basic Configuration**
CDN provides the Ignore Query String switch, which allows you to control whether to filter parameters after **"?"** in end users' request URLs. You can use this feature for flexible version control or token-based authentication. For more information, please see [Ignore query string configuration](https://intl.cloud.tencent.com/doc/product/228/6291).
3. **Cache expiration configuration**
Cache expiration configuration refers to the set of expiration rules that CDN cache nodes should comply with when caching your business content. For more information, please see [Cache expiration configuration](https://intl.cloud.tencent.com/doc/product/228/6290).

### Completing the connection
After entering all configuration items on the **Create Distribution** page, click **Submit** to add the domain name and wait for domain name configuration to be delivered over the entire network, which usually takes 5 to 10 minutes.

### Configuring CNAME
After successfully adding a domain name, You can view the acceleration CNAME assigned by CDN on the **Domain Management** page. You need to add a CNAME record for the domain name through your DNS service provider (such as DNSPod). Acceleration services will become available after **the DNS configuration takes effect**. For more information, please see [CNAME Configuration](https://intl.cloud.tencent.com/doc/product/228/3121).


>According to regulations, if the origin server is at an accelerated domain name of Tencent Cloud CVM, the domain name configured for the host header should obtain an ICP filing through Tencent Cloud. For more information, please see [Host header configuration](https://intl.cloud.tencent.com/document/product/228/6293).


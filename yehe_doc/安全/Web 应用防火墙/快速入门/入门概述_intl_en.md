Tencent Cloud WAF offers two types, SaaS and CLB, which vary in the way to connect domain names. To use this service, please follow the directions below based on your actual needs.
## SaaS WAF 
To protect your website, SaaS WAF assigns a CNAME to your domain name under protection, modifies the DNS resolution record of your website, and forwards the web requests received by your website to WAF. Used with security groups, SaaS WAF can prevent direct attacks toward the real server of your website. To achieve the above, you need to follow the steps below:
- [Step 1: Add a Domain Name](https://intl.cloud.tencent.com/document/product/627/35651)
- [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652)
- [Step 3. Modify DNS Resolution](https://intl.cloud.tencent.com/document/product/627/35653)
- [Step 4. Set a Security Group](https://intl.cloud.tencent.com/document/product/627/35654)

## CLB WAF 
CLB WAF associates with Tencent Cloud Layer-7 CLB (listener) cluster by your domain name, and detects and purges HTTP or HTTPS traffic that goes through the CLB for side-channel threats. In this way, it can provide protection without interrupting your traffic forwarding, provided you finish the steps below:
- [Step 1: confirm Cloud Load Balancer configuration](https://intl.cloud.tencent.com/document/product/627/34719)
- [Step 2: add and bind Cloud Load Balancer to the domain name](https://intl.cloud.tencent.com/document/product/627/34720)
- [Step 3: verify the test](https://intl.cloud.tencent.com/document/product/627/34721)

>CLB WAF is now available in Beta. To use it, please submit an application, and we will process it for you as soon as possible.

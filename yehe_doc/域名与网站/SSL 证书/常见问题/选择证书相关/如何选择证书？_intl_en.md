### Which certificate should I choose?
- If the website owner is an individual (without a business license), you can only apply for DV SSL certificates.
- For financial and payment enterprises, EV SSL certificates are recommended.
- For general enterprises, OV SSL certificates and SSL certificates with a higher trust level are recommended.
- For website URLs being called as a mobile websites or interface, OV SSL certificates and SSL certificates with a higher trust level are recommended.

### How do I choose a certificate provider?
Choose an appropriate certificate provider based on each SSL certificate’s browser compatibility test report and your enterprise’s business requirements.
For more information, see [Browser Compatibility Test Report](https://intl.cloud.tencent.com/document/product/1007/30165).

### How do I choose a certificate based on the number of supported domain names?
Tencent Cloud provides the following 4 types of domain names:
- **Single-domain SSL certificate**: only one domain name can be bound. This can be a second-level domain name like `tencent.com`, or a third-level domain name like `example.tencent.com`. **However, binding all sub-domain names under a second-level domain name is not supported**. Up to 100 levels of domain name are supported.
- **Multi-domain name**: a single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names stated on Tencent Cloud's official website.
- **Wildcard domain name**: only 1 wildcard domain name with only 1 wildcard can be bound, such as `*.tencent.com` and `*.example.tencent.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.tencent.com` is not supported.
- **Multi-wildcard domain name**: multiple wildcard domain names with each containing only 1 wildcard can be bound, such as `*.tencent.com` and `*.example.tencent.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.tencent.com` is not supported.

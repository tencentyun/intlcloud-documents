### How can I choose a certificate type?
- If the website owner is an individual (without a business license for enterprise), only DV SSL certificates can be applied for.
- For financial and payment enterprises, EV SSL certificates are recommended.
- For general enterprises, OV SSL certificates and SSL certificates with a higher trust level are recommended.
- For website URLs being called and mobile websites, OV SSL certificates and SSL certificates with a higher trust level are recommended.

### How can I choose a certificate provider?
Choose an appropriate certificate provider based on the browser compatibility test report of SSL certificates and your enterprise business requirements.
For more information, see [Browser Compatibility Test Report](https://intl.cloud.tencent.com/document/product/1007/30165).

### How can I choose a certificate based on the number of domain names?
Tencent Cloud provides the following 4 types of domain names:
- **Single-domain name**: only 1 domain name can be bound. It can be a second-level domain name like `example.tencent.com`, a third-level domain name like `example.example.tencent.com`, or a first-level domain name like `tencent.com`. **However, binding all sub-domain names under a first-level domain name is not supported.** Up to 100 levels of domain names are supported.
- **Multi-domain name**: a single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names stated on Tencent Cloud's official website.
- **Wildcard domain name**: only 1 wildcard domain name with only 1 wildcard can be bound, such as `*.tencent.com` and `*.example.tencent.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.tencent.com` is not supported.
- **Multi-wildcard domain name**: multiple wildcard domain names with each containing only 1 wildcard can be bound, such as `*.tencent.com` and `*.example.tencent.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.tencent.com` is not supported.

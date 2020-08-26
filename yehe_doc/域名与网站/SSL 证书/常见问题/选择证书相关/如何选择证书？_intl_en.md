### How do I choose which SSL certificate type to use?
- If the entity of your website is an individual (that is, you do not have a business license), you can only apply for a Domain Validated (DV) free certificate or a DV paid certificate.
- For financial and payment enterprises, Extended Validation (EV) certificates are recommended.
- For general enterprises, Organization Validated (OV) or higher-level certificates are recommended.
- For API calling or websites for mobile terminals, OV or higher-level certificates are recommended.

### How do I choose which SSL certificate brand to use?
You can choose an SSL certificate brand by comparing the browser compatibility test reports of various SSL certificate brands with your particular business needs.
For more information, see [Browser Compatibility Test Report](https://intl.cloud.tencent.com/document/product/1007/30165).

### How do I choose the number of domain names supported?
Tencent Cloud provides the following 4 types of domain names:
- **Single-domain name**: only 1 domain name can be bound. It can be a second-level domain name such as `example.domain.com`, a third-level domain name such as `example.example.domain.com`, or a first-level domain such as `domain.com`. **However, binding all sub-domain names under a first-level domain name is not supported.** Up to 100 levels of domain names can be supported.
- **Multi-domain name**: a single certificate can be bound to multiple domain names, subject to the maximum number of supported domain names stated on Tencent Cloud's official website.
 
- **Wildcard domain name**: only 1 wildcard domain name with only 1 wildcard can be bound, such as `*.domain.com` and `*.example.domain.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.domain.com` is not supported.
- **Multi-wildcard domain name**: multiple wildcard domain names with each containing only 1 wildcard can be bound, such as `*.domain.com` and `*.example.domain.com` (up to 100 levels). A wildcard domain name with multiple wildcards like `*.*.domain.com` is not supported.

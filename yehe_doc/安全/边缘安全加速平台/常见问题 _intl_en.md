### How can I connect my site to EdgeOne?
EdgeOne supports NS and CNAME connection.

### What security capabilities does EdgeOne have?
It can prevent web application layer, DDoS, CC, bot, and crawler attacks and allows you to configure complicated custom access control rules based on your business needs.

### Does EdgeOne support cross-region accerlation?
EdgeOne deploys edge nodes in to fully meet your cross-region business needs. For specific available regions, [contact us](https://intl.cloud.tencent.com/contact-us).

### Does EdgeOne support sites not deployed on Tencent Cloud?
Yes. For more details, please [contact us](https://intl.cloud.tencent.com/contact-us).

### Does EdgeOne support API operations?
Yes. EdgeOne supports TencentCloud API and Terraform API. 

### Does EdgeOne support dynamic acceleration?
Yes. It supports scenarios where requests for dynamic/static hybrid resources need to be accelerated. It can optimize the request response time and stability to deliver a high-quality and smooth access experience for websites.

### What site business security protection capabilities does EdgeOne offer?
EdgeOne provides web and bot protection for HTTP and HTTPS-based website businesses. Specific web protection rules include those for web security, OWASP rules, custom characteristics, and frequency control.

### What non-site business security protection capabilities does EdgeOne offer?
EdgeOne provides DDoS attack protection for TCP and UDP applications with specified ports, such as detection and protection against common types of DDoS attack, filtering rules by port, protocol, source IP region, and custom packet characteristic, and UDP watermark protection (coming soon).

### The monitoring data I see in Cloud Monitor and EdgeOne are not the same.

Data trends on Cloud Monitor and EdgeOne are generally consistent. However when it comes to the 1-minute granularity, the data can be slightly different. See below for details:

- **Cloud Monitor**: Collect data from edge servers and aggregate the data with 1-minute granularity on the domain name level. This can guarantee the timeliness and stability. But it only provides data related to key metrics on the domain name level.
- **EdgeOne**: Collect and analyze logs in real-time upon receiving the request, and then print out the result. It supports more metrics, such as traffic and requests by the device type and browser type. But the print-out time can be affected in case of request surges. 

Assume that a user requests a 1 GB file. The download starts at 10:00:00 and ends at 10:01:40.
- **Cloud Monitor**: Every edge server reports the metric data at a 1-minute interval. Data of this event is recorded at both 10:01 and 10:02. 
- **EdgeOne**: Every edge server prints a log when the download ends (10:01:40). The data is recorded at 10:01.

Therefore, data from Cloud Monitor and EdgeOne can differ at a 1-minute granularity due to the difference of sampling rules.
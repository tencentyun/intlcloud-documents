With globally distributed edge nodes, [Tencent Cloud EdgeOne](https://intl.cloud.tencent.com/document/product/1145/45961) offers CDN acceleration combined with comprehensive edge security services, including DDoS mitigation, web protection, bot management and custom rules, enabling more flexible and more robust protection capabilities.

To protect your domain names connected to CDN, migrate your service to EdgeOne as follows.

## Directions

### Step 1: Decide the protection scope

As EdgeOne service is provided based on [sites](https://intl.cloud.tencent.com/document/product/1145/46435), you should determine how many sites needed for your domain names. See examples below:

| CDN Domain Name                                      |  EdgeOne Site         | Description                                                         |
| ------------------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| `www.example.com`<br/>`test.example.com`<br/>`image.example.com` | `example.com`               | Since these subdomain names are under one primary domain name (example.com), only one site is needed. |
| `www.example.com`<br/>`test.example.com`<br/>`www.site.com`      | `example.com`<br />`site.com` | Since these subdomain names are under two primary domain names (example.com, site.com), two sites are needed. |


### Step 2: Add sites and acceleration domain names

Go to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) to add your site and acceleration domain name. For detailed steps, see [Quick Start](https://www.tencentcloud.com/document/product/1145/54208).

To add a site, you need to subscribe to an EdgeOne plan. The Standard plan is recommended as it offers DDoS mitigation, web protection, CC protection and bot management along with limited security traffic and requests. For more details, see [EdgeOne Plans](https://intl.cloud.tencent.com/document/product/1145/48705).

>?Security features (including DDoS mitigation and web protection) are enabled automatically once your acceleration domain name is added to EdgeOne. To customize the security configuration as needed, refer to Step 3.


### (Optional) Step 3: Customize security policies

Custom security policies such as IP blocklist/allowlist, regional blocking and web protection rules can be created to suit your needs. For configuration details, see the documents below:

- [DDoS Mitigation](https://intl.cloud.tencent.com/document/product/1145/47795)
- [Web Protection](https://intl.cloud.tencent.com/document/product/1145/46729)
- [Bot Management](https://intl.cloud.tencent.com/document/product/1145/47912)


## CDN Refund

To return unused CDN resources, submit your purchase records via [a ticket](https://console.intl.cloud.tencent. com/workorder/category). Fees will be sent back based on the percentage of remaining usage.

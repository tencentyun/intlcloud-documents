Smart Acceleration is a route optimization service, which always selects the best route for your business according to the network condition in real time, so as to lower the network latency, reduce connection and request failures. Smart Acceleration is a value-added feature of EdgeOne.
>?The EdgeOne console is now only available to beta users. [Contact us](https://intl.cloud.tencent.com/contact-us) to join the beta.

## Use Cases
#### Dynamic resources
Smart Acceleration can be used in scenarios where dynamic content needs to be requested frequently, including online game, ecommerce, finance, payment, and online education.

#### Dynamic and static resources
For dynamic content use cases, you can refer to the above scenarios. Your static content still provides service through data cached on edge servers. In addition, when any cached content expires, it will be quickly updated through smart acceleration.

## Directions
### Enabling Smart Acceleration for a Site 

>? **Smart Acceleration** is a paid service.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site acceleration** > **Network optimization** on the left sidebar.
2. On the **Smart acceleration** page, select the target site, and enable/disable the feature.


### Enabling Smart Acceleration for a Subdomain
You can also enable Smart Acceleration for a specific subdomain.

1. Go to the [Rule engine](https://console.cloud.tencent.com/edgeone/rules) page, select the site and click ![](https://qcloudimg.tencent-cloud.cn/raw/0f0a8aa7913c1c31284b692eadbccd85.png)
2. Complete the parameters as instructed below, and click **Save and publish**. For more information, see [Configuring Rule Engine](https://cloud.tencent.com/document/product/1552/70901).

Parameters:
 - Match type: Host
 - Operator: Equals to 
 - Value: Subdomain
 - Operation: Smart Acceleration 
 - On/Off: Toggle on or off the feature as necessary
 
## Must-knows
- If your site supports **Content Acceleration**, **Smart Acceleration** only works on subdomains in Sec-MCA mode but not Content Acceleration mode.
- Make sure you have added a record at your domain name provider. See [Domain Name Service](https://cloud.tencent.com/document/product/1552/70825).
- Smart Acceleration is a value-added service. 
>? For more billing details, please submit a ticket or contact your sales rep.

# Release Notes at Tencent Cloud International

To improve the business connection and protection configuration experience outside the Chinese mainland, WAF was upgraded on June 2, 2022, with the web console 2.0 released. After the upgrade, connection is more stable, protection is more powerful, and traffic management is more refined, with value-added capabilities of bot traffic management and log service supported. In addition, the console allows you to switch between regions in and outside the Chinese mainland to better manage instance resources by region. 

Different types of WAF instances are impacted as follows:

- SaaS WAF: The region attributes of WAF instances remain unchanged, the system automatically adds region fields according to the attributes, and the console supports management by region.

- CLB WAF: WAF instances in the Chinese mainland support connecting and protecting web businesses for CLB instances in the Chinese mainland, and those outside the Chinese mainland support those of CLB instances outside the Chinese mainland.

After **this** upgrade to web console 2.0, you can enjoy the following product capabilities and configurations:

## Cross-region resource data isolation


#### The console allows you to switch between regions in and outside the Chinese mainland as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/b609ce00f74d56ffa5663501d0a1bc2e.png)
![](https://qcloudimg.tencent-cloud.cn/raw/5eefbaf3b13428f007001ce34da6fd68.png)
## More convenient domain name connection

#### Upgraded domain name connection and management

**You can manage multiple instances in a unified manner to improve the routine security Ops efficiency.** SaaS WAF instances support custom weight-based IP forwarding as well as multi-domain name forwarding to enable complex business connections.

#### Domain name connection guide

A domain name connection guide is added, providing more detailed directions after a domain name is added and facilitating business connection.

#### Custom traffic tagging

SaaS WAF instances support custom traffic tagging to meet the requirements of more complex business analysis and linked protection.

#### Client information logging

SaaS WAF instances allow you to enable the transfer of business client source IP address and port information. This complements XFF records to ensure business compliance in finance and ecommerce industries.

## Protection capability upgrade

#### Quick protection switch

You can quickly enable or disable all protection modules and certain features of certain protection modules. This facilitates routine Ops troubleshooting, accelerates problem locating, and ensures business continuity.

#### Refined traffic management

IP blocklist/allowlist is upgraded to blocklist/allowlist management. Custom policy rules that were previously set to "allow" are upgraded to precise allowlist rules, and other custom policy rules are upgraded to access control rules. Rule configuration and execution are not affected by the upgrade.

The precise allowlist feature implements refined traffic management during routine security Ops, improving the traffic control efficiency and effect while ensuring business security.

 

### Value-added capability upgrade - commercial release of bot traffic management

The newly upgraded bot protection system integrates the browser bot defense module, threat intelligence module, as well as big data and AI algorithm model and analysis engine. It provides visualized traffic analysis by risk level and more intuitive threat handling policies.

As a SaaS service provider, you need to manage many domain names. Connecting these domain names to acceleration and security services is tedious and troublesome. In addition, HTTPS access requires certificate application, deployment, and update, which will incur unbearably high Ops costs.

EdgeOne domain aliases can extend EdgeOne security and acceleration capabilities to your users, and you can quickly connect merchant domain names simply through minimal configuration. The platform also supports certificate application and automatic update, saving purchase and maintenance costs and allowing you to focus on business growth.

## How It Works
<img src="https://qcloudimg.tencent-cloud.cn/raw/93fa371442a74bdc00358f2978da504e.png" width=900px>

You can quickly connect merchant domain names to EdgeOne through four simple steps:
<dx-steps>
- Connect the target domain name (such as `*.example.com` as shown above) in the EdgeOne console or through APIs.
- After connecting the target domain name (`*.example.com`), configure a domain alias for it (such as `shop.a.com` as shown above).
- Add the CNAME record of `shop.a.com` > `*.example.com` at your DNS service provider.
- Apply for a free certificate for the domain alias `shop.a.com`.
  </dx-steps>

## Use Cases
- **Use case 1:** You are a SaaS service provider managing many domain names with the same configuration, and want to quickly connect them to acceleration and security capabilities.   
- **Use case 2:** Many merchant domain names point to the SaaS service provider domain name, and the application, deployment, and update of certificates for these domain names involve a heavy workload. You want to get certificate application and automatic update capabilities from a platform.  
- **Use case 3:** You want to have multiple primary/secondary domain names for business disaster recovery; for example, when a domain name becomes unavailable due to invalidated ICP filing, a secondary domain name can be quickly provided to ensure the service availability.

## Benefits to the Customer
- **Cost reduction**: EdgeOne implements certificate application and automatic update, so you don't need to invest resources to maintain domain name certificates.
- **Configuration simplification**: You can configure many merchant domain names through simple operations.   
- **Security and acceleration**: You can reuse EdgeOne's acceleration and security capabilities of the target domain name after binding a merchant domain name.   

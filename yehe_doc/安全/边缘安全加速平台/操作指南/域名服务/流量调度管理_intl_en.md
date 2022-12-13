## Overview
Traffic scheduling management is a multi-CDN smart resolution and scheduling tool provided by EdgeOne. It supports custom traffic scheduling policies between the origin server and service providers to implement smooth canary migration of traffic and flexible allocation of services, thereby ensuring a high service availability.

#### Use Cases
- Canary migration: When a new service provider is added, canary switch is required to ensure the service availability and smooth migration.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/AZKx839_%E5%BA%94%E7%94%A8%E5%9C%BA%E6%99%AF%EF%BC%9A%E7%81%B0%E5%BA%A6.png" width=700px>
- Multi-vendor scheduling: If businesses are large in scale and sensitive, traffic can be flexibly allocated to multiple vendors to spread risks and implement disaster recovery.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pXZN880_%E5%BA%94%E7%94%A8%E5%9C%BA%E6%99%AF%EF%BC%9A%E5%A4%9A%E5%8E%82%E5%95%86.png" width=700px>

#### Features
- Simple management: You can implement traffic scheduling management simply by selecting a domain name, adding a service provider, and adding a scheduling policy.
- Fast access: You can implement fast access only by adding the CNAME record allocated by EdgeOne at your DNS service provider.
- Multiple scheduling modes: Ratio-based and region-based scheduling modes are available to meet various requirements.
- Multiple scenarios: You can use either the origin server or services provided by other CDN vendors, implement canary switch, and use services from different vendors at the same time.

## Prerequisites
You have [purchased](https://intl.cloud.tencent.com/document/product/1145/45964) the EdgeOne Enterprise plan and [connected the site](https://intl.cloud.tencent.com/document/product/1145/45966) in CNAME access mode.

## Adding a Traffic Scheduling Policy
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site** > **Domain Name Service** > **Traffic Scheduling Management**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jafs647_%E6%B7%BB%E5%8A%A0%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AD%96%E7%95%A5-1.%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AE%A1%E7%90%86%E9%A1%B5%E9%9D%A2.png)
2. On the **Traffic Scheduling Management** tab, click **Add scheduling policy**, select the target domain name, and click **Create**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/PTJu605_%E6%B7%BB%E5%8A%A0%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AD%96%E7%95%A5-2.%E5%88%9B%E5%BB%BA%E7%AD%96%E7%95%A5.png)
3. Click **Add service provider**, configure parameters such as the service provider name and CNAME record as needed, and click **Next**.
>?The default service provider is EdgeOne, which cannot be modified or deleted. You can add a domain name of the origin server or a CNAME domain name of another CDN service provider.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Y6A2803_%E6%B7%BB%E5%8A%A0%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AD%96%E7%95%A5-3.%E6%B7%BB%E5%8A%A0%E6%9C%8D%E5%8A%A1%E5%95%86.png)
4. Click **Add policy**, select the split zone/region, configure the multi-service provider scheduling policy, and click **Submit configuration**. You can select multiple service providers and set their weights.
>?
>- By default, all traffic passes EdgeOne. This is the base policy, which cannot be deleted but can be changed to another service provider.
>- Split zone/Region settings support countries/regions, ISPs and provinces in the Chinese mainland, and states in the US and India.
>- Finer-grained regions/split zones have a higher priority. For example, if you select the origin server for Beijing, service provider A for the Chinese mainland, and service provider B for the default split zone, then traffic in Beijing region will pass the origin server, traffic in other regions in the Chinese mainland will pass service provider A, and overseas traffic will pass service provider B.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/t33y727_%E6%B7%BB%E5%8A%A0%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AD%96%E7%95%A5-4.%E6%B7%BB%E5%8A%A0%E7%AD%96%E7%95%A5.png)
5. The traffic scheduling CNAME should be identical to the default domain name CNAME. After the policy is added, if the domain name resolution has been switched, no change is required, and the policy will take effect immediately in the production environment; otherwise, you need to switch the domain name resolution at your DNS service provider.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rfgt684_%E6%B7%BB%E5%8A%A0%E6%B5%81%E9%87%8F%E8%B0%83%E5%BA%A6%E7%AD%96%E7%95%A5-5.%E6%B7%BB%E5%8A%A0%E7%AD%96%E7%95%A5%E5%AE%8C%E6%88%90.png)

## Managing a Traffic Scheduling Policy
You can edit, disable, enable, and delete a policy on the [**Domain Name Service**](https://console.cloud.tencent.com/edgeone/dns) > **Traffic Scheduling Management** tab.
### Disabling a policy
Disabling a traffic scheduling policy will void it, and all traffic will be scheduled to EdgeOne.
### Enabling a policy
You can enable a disabled policy to resume traffic scheduling management, after which traffic will be scheduled as configured, rather than to EdgeOne.
### Deleting a policy
You can delete a disabled policy. This does not affect the service but cannot be recovered. Proceed with caution. 
### Managing a policy
Click **Manage** to enter the **Scheduling Policy Management** page, where you can add, delete, modify, and disable a service provider and scheduling policy.
>?
>- Changing the service provider already referenced by a policy will take effect immediately.
>- Deleting, modifying, enabling, and disabling a policy will take effect immediately.
>- The service provider already referenced by a policy cannot be deleted.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/QYZj764_%E7%AE%A1%E7%90%86%E7%AD%96%E7%95%A5.png)

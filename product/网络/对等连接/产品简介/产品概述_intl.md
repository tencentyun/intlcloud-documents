

VPC peering connection is a cross-VPC network interconnection service for office data synchronization that allows connectivity between the two VPCs as if they belong to the same network. Intra-region or cross-region connectivity can be implemented between two VPCs of the same or different users by configuring routing policies at both ends of the connections. Peering connections do not depend on a single piece of hardware, so there is no single point of failure or bandwidth bottleneck.
Cross-region connectivity is a general term for Tencent Cloud's resources within different regions communicating with each other, including VPC cross-region connectivity (i.e. cross-regional peering connection) and basic network cross-region connectivity.

## Product Advantages

Peering connection have the following advantages over Internet transfer.

### High quality

Sharing the same self-built internal network with Tencent Group's businesses, it is not affected by the quality of public network, and thus is greatly improved in terms of availability, latency and packet loss.

### High security

- Protected against DDoS attacks by Tencent's [Dayu Anti-DDoS](/document/product/297), it has high security.
- It bypasses the wide area Internet and ISP linkages, avoiding the risk that packets may be intercepted when they are transmitted over public networks.

### Cost-effective

Platinum, Gold and Silver levels of services are available to choose from based on your business requirements, so as to deploy services separately and save costs.

- Platinum: suitable for businesses most sensitive to transfer quality, such as payment and game acceleration.
- Gold: suitable for businesses that require transfer of key business data, such as enterprise business data transfer, ERP, etc.
- Silver: suitable for cost-sensitive and jitter-insensitive businesses that require high security, such as remote data backup.

> **Note:**
> Use cases supported by platinum, gold and silver are as follows:
>
> 1. Gold: Supports all regions.
> 2. Platinum and silver: Support the monthly 95th percentile billing mode & some lines (Beijing, Shanghai, Guangzhou, South Korea, Hong Kong). Their functionality is under internal trial. If necessary, please [submit a ticket](https://console.cloud.tencent.com/workorder) for application.

This article aims to help users improve the security and reliability of their CVM instances.

## Security and Network

- **Limited access**: restrict access by using a firewall ([Security Group](https://intl.cloud.tencent.com/document/product/213/12452)) to only allow the trusted addresses to access instances. The security group should also have stringent rules such as limiting access to ports and by IP addresses.
- **Security level**: different security group rules can be created for instance groups of different security levels to ensure that instances running important business cannot be easily accessed by external sources.
- **Network logical isolation**: use [VPC](https://intl.cloud.tencent.com/document/product/213/5227) to divide resources into logical zones.
- **Account permission management:** when it is necessary to allow multiple different accounts to access the same set of cloud resources, you can manage permissions to cloud resources using the [policy mechanism](https://intl.cloud.tencent.com/document/product/598/10601).
- **Secure login:** log in to your Linux instances using the [SSH key](https://intl.cloud.tencent.com/document/product/213/6092) whenever possible. For the instances that you [log in with a password](https://intl.cloud.tencent.com/document/product/213/6093), the password needs to be changed regularly.

## Storage

- **Hardware storage:** for data that requires high reliability, use Tencent Cloud's cloud disks to ensure the persistent storage and reliability of data. Try not to use [Local Disks](https://intl.cloud.tencent.com/document/product/213/5798) for storage. For more information, see the [Cloud Block Storage Product Documentation](https://intl.cloud.tencent.com/document/product/362).
- **Database:** for databases that are frequently accessed and whose capacity frequently changes, use Tencent Cloud TencentDB.

## Backup and Recovery

- **Intra-region instance backup**: you can back up your instances and business data using **custom images** and **CBS snapshots**. For more information, refer to [CBS Snapshot](https://intl.cloud.tencent.com/document/product/362/31638) and [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
- **Cross-region instance backup**: you can copy and back up instances across regions by [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943).
- **Blocking instance failures**: you can use [EIPs](https://intl.cloud.tencent.com/document/product/213/5733) for domain name mapping to ensure that the server can quickly redirect the service IP address to another CVM instance when it is unavailable, thereby shielding instance failures.

## Monitoring and Alarms
- **Monitoring and event response**: periodically check monitoring data and set proper alarms. For more information, refer to the [Tencent Cloud Observability Platform Product Documentation](https://intl.cloud.tencent.com/document/product/248).
- **Handling request spikes**: with [Auto Scaling](https://intl.cloud.tencent.com/document/product/377), the stability of CVMs during peak hours can be guaranteed and unhealthy instances can be replaced automatically.

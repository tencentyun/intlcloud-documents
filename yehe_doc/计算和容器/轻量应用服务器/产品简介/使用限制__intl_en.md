>?For more information on the differences between Lighthouse and CVM, please see [Comparison with CVM](https://intl.cloud.tencent.com/document/product/1103/41521).
>

## General Limits
 - After an instance is created, its public and private IPs cannot be changed.
 - Currently, cloud disks cannot be mounted as instance data disks.
 - An instance supports the overall upgrade of the configuration (computing, storage, and network) on a package basis but not package downgrade. For more information, please see [Upgrading Instance Package](https://intl.cloud.tencent.com/document/product/1103/41407).

## Quota Limits
 - Up to **10** instances can be created in each region under one account.
 - Up to **100** firewall rules can be created for each Lighthouse instance.
 - Up to **10** SSH key pairs can be created in each region under one account.
 - Up to **20** custom images can be created in each region.
 - Snapshot quota limits:
  - Snapshots cannot be created for instances on the storage package.
  - The maximum number of free snapshots in each region is the number of created instances (excluding instances to be repossessed and instances on the storage package) multiplied by 2 and cannot exceed 10.

## ICP Filing Limits
- When using a Lighthouse instance to provide website services in the Chinese mainland, you need to apply for ICP filing.
- Up to 5 filed websites can be hosted on one Lighthouse instance.
- Lighthouse doesn't support generating ICP filing authorization codes, and ICP filing can be conducted only under the account that has purchased Lighthouse.

## Private Network Connectivity Limits
There are certain limits on private network connectivity between Lighthouse and other Tencent Cloud services. For more information, please see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).

This document introduces how to migrate the resources in a BWP to other BWPs.

## Restrictions
- Only bill-by-IP accounts support this resource migration feature, and traditional account types need to be upgraded before using this feature. For more information about Upgrading, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- This migration feature is only supported by BGP BWPs and AIA BGP BWPs, but not by Anycast accelerated BGP BWPs and China Mobile/Unicom/Telecom BWPs. For more information about different types of BWPs, please see [Bandwidth Type](https://intl.cloud.tencent.com/document/product/684/15254).
- BGP IPs can only be migrated in BGP BWPs, while AIA BGP IPs can only be migrated in AIA BGP BWPs.


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. Select the region in the upper-left corner of the "Bandwidth Package" page, and click the target instance ID in the instance list.
3. Select the public IP or CLB resource to be migrated, and click **Migrating a Bandwidth Package** on the instance details page.
4. Select the bandwidth package to be migrated to, and click **OK** in the pop-up window "Migrating a Bandwidth Package".
![]()


## Overview

A multi-AZ is created by combining multiple AZs in the same region. A multi-AZ deployed cluster has better disaster recovery capabilities than a single-AZ deployed cluster and can protect your database instances from IDC-level failure or AZ outages. An existing single-AZ deployed cluster can be automatically upgraded to a multi-AZ one through online data migration without business interruptions. 

## Billing

 The multi-AZ feature is currently available free of charge; that is, a single-AZ deployed cluster can be upgraded to a multi-AZ one for free.

## Use Limits

This feature is currently unavailable in Shenzhen Finance, Jakarta, and Mumbai regions and will be available in more regions and AZs in the future.

## Notes

- If [Reading Local Nodes Only](https://intl.cloud.tencent.com/document/product/239/41049) is not required, upgrading to multi-AZ deployment will involve metadata migration only without affecting the service, which generally take less than three minutes to complete.
- If [Reading Local Nodes Only](https://intl.cloud.tencent.com/document/product/239/41049) is required, you will need to upgrade the proxy version and Redis kernel minor version, which will involve data migration and may take hours to complete. There will be one or several momentary disconnections within three minutes after the upgrade is completed, so make sure that your business has an automatic reconnection mechanism.

## Prerequisites

- The cluster region has at least two AZs.
- The database is on v4.0 or later.
- The instance is in **Running** status.

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. Click the **instance ID** of the target instance in blue to enter the **Instance Details** page.
5. In the **Basic Info** section on the **Instance Details** page, click **Upgrade to Support Multi-AZ Deployment** after **AZ**.
![](https://main.qcloudimg.com/raw/1fb0cc13e207c84446d64a3a725c5c1c.png)
6. In the **Upgrade to Support Multi-AZ Deployment** window, learn more about the impact of upgrading to multi-AZ deployment, confirm whether to support [Reading Local Nodes Only](https://intl.cloud.tencent.com/document/product/239/41049), and click **OK**.
7. The **Instance Status** in **Basic Info** becomes **Upgrading to support multi-AZ deployment**. Wait for the status to become **Running**.

## Related APIs

| API                                                 | Description |
| :----------------------------------------------------------- | :--------------- |
| [UpgradeVersionToMultiAvailabilityZones](https://intl.cloud.tencent.com/document/product/239/40162) | Upgrades instance to support multi-AZ deployment |


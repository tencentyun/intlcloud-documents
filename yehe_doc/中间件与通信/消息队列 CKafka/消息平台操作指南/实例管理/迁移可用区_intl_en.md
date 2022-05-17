## Overview

You can migrate a **CKafka Pro Edition** instance to another AZ in the same region. All its attributes, configurations, and connection address will stay unchanged after the migration. The time it takes to migrate the instance is subject to the instance's data volume.

For example, you can migrate to a new AZ in the following scenarios:

- If you want to modify an instance's type, but the current AZ doesn't support the new instance type, you can migrate the instance to an AZ supporting the new type.
- If the current AZ has no remaining resources for scaling, you can also migrate the instance to another AZ in the same region with sufficient resources to meet your business needs.

## Prerequisites

- The instance is running.
- The region where the instance is located has multiple AZs to support cross-AZ migration.

## Billing Description

This feature is free of charge. There is no charge even for migrating an instance from a single AZ to multiple AZs.

## Description

- If the original instance is deployed in a single AZ, you can switch the AZ or upgrade to [multi-AZ deployment](https://intl.cloud.tencent.com/document/product/597/40243).
- If the original instance is deployed in multiple AZs, you can switch AZs but cannot downgrade to single-AZ deployment.

## Migration Type

| Migration Type | Applicable Scenario |
| :----------------------------- | :----------------------------------------------------------- |
| Migration from one AZ to another AZ | The AZ where the instance is located is under full load or other conditions that affect the instance performance. |
| Migration from one AZ to multiple AZs | You can improve the disaster recovery capability of the instance and implement cross-data center disaster recovery. Source and replica instances are located in different AZs. Multi-AZ instances can withstand higher levels of disasters than single-AZ instances. For example, the latter can tolerate server- and rack-level failures, while the former can tolerate data center-level failures. |



## Directions

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the **Basic Info** module, click **Edit** on the right of the current AZ and select the AZ you want to switch to.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f8307326974bbae58af6d0d1c21b6ce7.png)
4. Click **OK**. It will take 5–10 minutes to complete the configuration adjustment. You can view the progress in the **Status** column in the instance list.
![](https://qcloudimg.tencent-cloud.cn/raw/7a2e65ad428af0ffeec2a3342fe7fe61.png)

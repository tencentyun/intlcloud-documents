
You can migrate a TencentDB for MySQL instance to another AZ in the same region. All its attributes, configurations, and connection address will stay unchanged after the migration. The time it takes to migrate the instance is subject to the instance's data volume.

For example, you can migrate to a new AZ in the following scenarios:
- If you want to modify an instance's type, but the current AZ doesn't support the new instance type, you can migrate the instance to an AZ supporting the new type.
- If the current AZ has no remaining resources for scaling, you can also migrate the instance to another AZ in the same region with sufficient resources to meet your business needs.

## Prerequisites
- The instance is running.
- The region where the instance is located has multiple AZs to support cross-AZ migration.

## Billing Description
This feature is free of charge. There is no charge even for migrating an instance from a single AZ to multiple AZs.

## Feature Description
- The instance will be momentarily affected when its AZ is switched; therefore, make sure that your application has an automatic reconnection mechanism.
- AZ migration will not result in a VIP change.
- The source instance is not decoupled from the read-only instances after AZ migration and can still be synced with them.
- You can choose the AZ of read-only instances.
- Read-Only instances don't support cross-region migration.
- No access through RO group (removal) can be made during migration switch.
- If the target instance has a task lock on the cloud platform during the DTS task, cross-AZ migration cannot be performed.
- If there are ongoing DTS tasks, after AZ migration, you need to restart such tasks.
- DTS export will fail if the source instance undergoes a cross-AZ migration switch during dumper export.
- For AZ migration under the two-node or three-node architecture, the selection of the source and replica AZs is subject to the remaining resources in the new AZ and region. You can select the new AZ during migration in the console, and the replica AZ option will be automatically updated.

## Migration Type

| Migration Type | Applicable Scenario | Supported Instance Types |
|---------|---------|---------|
| Migration from one AZ to another AZ | The AZ where the instance is located is under full load or other conditions that affect the instance performance. | Source, read-only, and DR instances |
| Migration from one AZ to multiple AZs | You can improve the disaster recovery capability of the instance and implement cross-data center disaster recovery. Source and replica instances are located in different AZs. Multi-AZ instances can withstand higher levels of disasters than single-AZ instances. For example, the latter can tolerate server- and rack-level failures, while the former can tolerate data center-level failures. | Source, read-only, and DR instances |
| Migration from multiple AZs to one AZ | You want to meet specific feature requirements. | Source, read-only, and DR instances |

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an **instance ID** or **Manage** in the **Operation** column to enter the instance details page.
2. On the **Instance Details** page, select **Basic Info** > **Region/AZ** and click **Migrate to New AZ**, or select **Availability Info** > **Deployment Mode** and click **Modify Replica AZ**.
![](https://qcloudimg.tencent-cloud.cn/raw/cd1bd1b09029548391ba986c61027907.png)
3. In the pop-up window, adjust the relevant configurations and click **Submit** after confirming that everything is correct.
 - **New AZ**: you can change the source AZ in the drop-down list or select **Yes** for **Multi-AZ Deployment** to modify the replica AZ.
 - **Delay Threshold for Data Consistency Check**: this option is available only when you change the source AZ. The threshold can be an integer between 1 and 10 seconds.
>! There may be a delay during the data consistency check. You need to set a data delay threshold. The database consistency check will be paused when the delay exceeds the set value and will be resumed when the delay drops below the threshold. If the threshold value is too small, the migration may take longer.
 - **Switch Time**: you can choose to switch during the maintenance time or upon migration completion. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
![](https://qcloudimg.tencent-cloud.cn/raw/33577bc75f50cb9805478f71b372e07f.png)


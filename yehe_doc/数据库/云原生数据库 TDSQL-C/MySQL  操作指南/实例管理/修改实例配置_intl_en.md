
An underprovisioned instance will underperform, while an overprovisioned instance will be faster but more expensive, you can adjust the instance specifications to strike a balance between cost and performance.
This document describes how to modify the computing specification and storage capacity of a TDSQL-C for MySQL instance.

## Configuration Adjustment Capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a secondary database with high specs will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the **Instance List** tab, locate the target instance and select **More** > **Adjust Configurations** in the **Operation** column.
3. On the instance configuration adjustment page, select the target configuration and click **Buy Now**.
>!Instance configuration adjustment may cause a momentary disconnection, which may affect your business. We recommend you do so during off-peak hours.
>
You can also specify the time to automatically execute the configuration adjustment.
 - If you select **Upon upgrade completion**, a momentary disconnection will be immediately triggered once the configuration adjustment is completed.
 - If you select **During maintenance time**, a momentary disconnection and switch will be triggered within the **maintenance window** of the instance. For more information on the maintenance window, see [Modifying Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/1098/44631).

![](https://qcloudimg.tencent-cloud.cn/raw/65de803d93d5feb3193aebd7dc05f057.png)


If your instance is overprovisioned or underprovisioned, your business needs cannot be best met, and you can adjust its specifications to fully utilize resources and reduce unnecessary costs.
This document describes how to adjust the compute specifications of a TDSQL-C for MySQL instance.

## Configuration Adjustment Capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a high-specced secondary database will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
On the cluster list page, proceed based on the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. On the **Cluster Details** tab, find the target instance, and click the icon ![](https://qcloudimg.tencent-cloud.cn/raw/41dc489c5cb922241a02d3a1a44a2a94.png) or click **Adjust Configurations** to enter the configuration adjustment page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Hu7Y126_34.png)
3. On the instance configuration adjustment page, select the target configuration and click **Buy Now**.
>!Adjusting the instance configuration may cause a restart. Make sure that your business has a reconnection mechanism.
>
You can also specify the time to automatically execute the configuration adjustment.
 - If you select **Upon upgrade completion**, a momentary disconnection will be immediately triggered once the configuration adjustment is completed.
 - If you select **During maintenance time**, the switch will be triggered within the **maintenance window** of the instance, causing a momentary disconnection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fWiU321_35.png)
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster and click the cluster ID or **Management** in the**Operation** column in the cluster list to enter the cluster management page.
2. On the **Instance List** tab, locate the desired instance and select **More** > **Adjust Configurations** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7hxI522_36.png)
3. On the instance configuration adjustment page, select the target configuration and click **Buy Now**.
>!Adjusting the instance configuration may cause a restart. Make sure that your business has a reconnection mechanism.
>
You can also specify the time to automatically execute the configuration adjustment.
 - If you select **Upon upgrade completion**, a momentary disconnection will be immediately triggered once the configuration adjustment is completed.
 - If you select **During maintenance time**, the switch will be triggered within the **maintenance window** of the instance, causing a momentary disconnection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QMKf711_37.png)

:::
</dx-tabs>

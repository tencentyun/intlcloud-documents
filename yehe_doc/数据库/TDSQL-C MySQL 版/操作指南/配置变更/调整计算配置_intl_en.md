If your instance is overprovisioned or underprovisioned, your business needs cannot be best met, and you can adjust its specifications to fully utilize resources and reduce unnecessary costs.
This document describes how to adjust the compute specifications of a TDSQL-C for MySQL instance.

## Configuration adjustment capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a high-specced secondary database will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
On the cluster list page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the target cluster in the cluster list on the left to enter the cluster management page.
2. On the **Cluster Details** tab, hover over the target instance and click **Adjust Configurations**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/LweX570_78.png)
3. On the instance configuration adjustment page, select the target configuration and click **Buy Now**.
>!Adjusting the instance configuration may cause a restart. Make sure that your business has a reconnection mechanism.
>
You can also specify the time to automatically execute the configuration adjustment.
 - If you select **Upon upgrade completion**, a momentary disconnection will be immediately triggered once the configuration adjustment is completed.
 - If you select **During maintenance time**, a momentary disconnection and switch will be triggered within the **maintenance time** of the instance. For more information, see [Modifying Instance Maintenance Time](https://www.tencentcloud.com/document/product/1098/53399).
![](https://qcloudimg.tencent-cloud.cn/raw/248fb7d57f0b0d3a1844a7d48b74643b.png)
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster and click the cluster ID or **Management** in the**Operation** column in the cluster list to enter the cluster management page.
2. On the **Instance List** tab, find the target instance and select **More** > **Adjust Configurations** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/7e890b021f4ab5adb6f476c2266d24b3.png)
3. On the instance configuration adjustment page, select the target configuration and click **Buy Now**.
>!Adjusting the instance configuration may cause a restart. Make sure that your business has a reconnection mechanism.
>
You can also specify the time to automatically execute the configuration adjustment.
 - If you select **Upon upgrade completion**, a momentary disconnection will be immediately triggered once the configuration adjustment is completed.
 - If you select **During maintenance time**, a momentary disconnection and switch will be triggered within the **maintenance time** of the instance. For more information, see [Modifying Instance Maintenance Time](https://www.tencentcloud.com/document/product/1098/53399).
![](https://qcloudimg.tencent-cloud.cn/raw/248fb7d57f0b0d3a1844a7d48b74643b.png)

:::
</dx-tabs>

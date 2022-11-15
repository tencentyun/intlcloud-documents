If the cluster storage space cannot meet your business needs, you can adjust it as needed.
This document describes how to adjust the storage space of a TDSQL-C for MySQL cluster.

>!
> - If the storage space is monthly subscribed, and you need to reduce it, [submit a ticket](https://console.tencentcloud.com/workorder/category).
>- If the storage space is monthly subscribed, you can expand it in the console. To use a storage space larger than the maximum storage space of the compute specifications, upgrade the compute specifications for the read-write instance. For more information, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).
> - If the storage space is monthly subscribed, the new storage space will be charged from the time it is adjusted until the cluster expires.
> - If the storage space is pay-as-you-go, you don’t need to expand it. The maximum storage space you can use is the same as that of the computing specification for the read-write instance. To use more storage space, you can upgrade the compute specifications for the read-write instance. For more information, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430)

## Configuration Adjustment Capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a high-specced secondary database will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click ID of the target cluster in the cluster list or **Management** in the **Operation** column to enter the cluster management page.
2. Select **Cluster Details** > **Configuration Info** > **Database Storage (Used/Total)** and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
3. In the pop-up window, select the storage space and click **OK** to make the payment.

>! If the storage space is monthly subscribed, the new storage space after adjustment must be larger than the used one. The change in storage billing mode has no impact on the existing business.

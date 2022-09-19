If the cluster storage space cannot meet your business needs, you can adjust the cluster storage space configuration.
This document describes how to adjust the storage space of TDSQL-C for MySQL.

>!
>- If the storage space billing mode is pay-as-you-go, you don't need to expand the storage space, and the maximum space you can use is the maximum storage space of the computing specification of the read-write instance. To use a larger storage space, upgrade the computing specification of the instance. For more information on computing specifications and corresponding maximum storage spaces, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).
>- If the storage space billing mode is monthly subscription, you can adjust the cluster storage space in the console. To use a storage space larger than the maximum storage space of the computing specification of the read-write instance, upgrade the computing specification. For more information on computing specifications and corresponding maximum storage spaces, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).
>- If the storage space billing mode is monthly subscription, the valid billing duration of the new storage space will start at the adjustment time and end at the cluster expiration time.

## Configuration adjustment capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a high-specced secondary database will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
2. Select **Cluster Details** > **Configuration Info** > **Database Storage (Used/Total)** and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
3. In the pop-up window, select the storage space and click **OK** to make the payment.
>!For the monthly subscription billing mode, the new storage space specified here must be larger than the used space. The change in storage billing mode has no impact on the existing business.

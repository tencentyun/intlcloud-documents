If the cluster storage space cannot meet your business needs, you can adjust it as needed.
This document describes how to adjust the storage space of a TDSQL-C for MySQL cluster.

>!
> - If the storage space is pay-as-you-go, you don’t need to expand it. The maximum storage space you can use is the same as that of the computing specification for the read-write instance. To use more storage space, you can upgrade the compute specifications for the read-write instance. In addition, you can switch the storage billing mode from pay-as-you-go to monthly subscription, and you can also adjust storage space during the switch. For more information, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).
>- If the storage space billing mode is monthly subscription, you can adjust the cluster storage space in the console. To use a storage space larger than the maximum storage space of the current compute specifications, upgrade the compute specifications of the read-write instance instance. For more information, see [Product Specifications](https://www.tencentcloud.com/document/product/1098/46430).
> - If the storage space is monthly subscribed, the new storage space will be charged from the time it is adjusted until the cluster expires.

## Configuration Adjustment Capabilities
TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. In cross-server configuration adjustment, no data migration is required; therefore, configuration upgrade/downgrade can be completed within seconds.
During instance configuration adjustment, a high-specced secondary database will be created automatically. Then, it will be automatically promoted to the primary database, and the original primary database will be disconnected to complete the configuration adjustment.

## Directions
**Scenario 1: The storage billing mode is pay-as-you-go, and you need to use a storage space larger than the maximum storage space of the current compute specifications**
If the storage space is pay-as-you-go, you don’t need to expand it. The maximum storage space you can use is the same as that of the computing specification for the read-write instance. To use more storage space, you can upgrade the compute specifications for the read-write instance. For directions, see [Adjusting Compute Configuration](https://www.tencentcloud.com/document/product/1098/50176). For more information on compute node specifications and corresponding maximum storage spaces, see [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).

**Scenario 2: The storage billing mode is pay-as-you-go, and you need to switch it to monthly subscription and specify the storage space**
On the cluster list page, proceed based on the actually used view mode:
<dx-tabs>
::: Tab view
1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. Select the billing mode on the cluster management page and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/haTN610_21.png)
3. In the setting window that pops up, select **Monthly Subscription** for the billing mode, specify the storage space size, and click **OK** to make the payment.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xuLW831_22.png)
>! If the storage space is monthly subscribed, the new storage space after adjustment must be larger than the used one. The change in storage billing mode has no impact on the existing business.
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click ID of the target cluster in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. Select **Cluster Details** > **Configuration Info** > **Database Storage (Used/Total)** and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
>?You can also click **Billing Info** > **Storage Billing** on the cluster details page, and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png) for adjustment.
3. In the pop-up window, select **Monthly Subscription** for the billing mode, specify the storage space size, and click **OK** to make the payment.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/LziR876_25.png)
>! If the storage space is monthly subscribed, the new storage space after adjustment must be larger than the used one. The change in storage billing mode has no impact on the existing business.
:::
</dx-tabs>

**Scenario 3: The storage billing mode is monthly subscription, and you need to adjust the storage space**
On the cluster list page, proceed based on the actually used view mode:
<dx-tabs>
::: Tab view

1. Log in to the [ TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click the target cluster in the cluster list on the left to enter the cluster management page.
2. Select the billing mode on the cluster management page and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/npjZ651_27.png)
>?You can also adjust the distributed storage module under the cluster details page by clicking **Expand** next to the storage specification.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/8phc012_28.png)
3. In the pop-up window, select the storage space and click **OK** to make the payment.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3th5190_29.png)
>! If the storage space is monthly subscribed, the new storage space after adjustment must be larger than the used one. The change in storage billing mode has no impact on the existing business.
:::
::: List view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), and click ID of the target cluster in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. Select **Cluster Details** > **Configuration Info** > **Database Storage (Used/Total)** and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png).
>?You can also click **Billing Info** > **Storage Billing** on the cluster details page, and click ![](https://qcloudimg.tencent-cloud.cn/raw/1ccd57694a24dfdf2b486ef8f7e42d63.png) for adjustment.
3. In the pop-up window, select the storage space and click **OK** to make the payment.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/miSI683_32.png)
>! If the storage space is monthly subscribed, the new storage space after adjustment must be larger than the used one. The change in storage billing mode has no impact on the existing business.
:::
</dx-tabs>

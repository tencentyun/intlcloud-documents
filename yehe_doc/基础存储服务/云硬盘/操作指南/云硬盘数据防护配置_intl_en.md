## Overview
Cloud disks will be repossessed by the system due to expiration or overdue payment. To avoid data loss in these cases, you can strengthen the data protection of cloud disks in the following two ways:
 - **[Expiry/Overdue Protection](#ExpirationProtection)**: After expiry/overdue protection is enabled for cloud disks, the system will automatically protect your data by creating a snapshot if your cloud disk is repossessed due to expiration or overdue payments.
 - **[Snapshot Protection](#SnapshotProtection)**: After snapshot protection is enabled, the scheduled snapshot policy will be associated with a cloud disk by default when it is created.


<dx-alert infotype="explain" title="">
- For more information on the repossession mechanism and overdue payment processing of cloud disks, see [Overdue Policy](https://intl.cloud.tencent.com/document/product/362/31625).
- Currently, users in the Chinese mainland can enjoy a free snapshot tier of 80 GB. The snapshot capacity that exceeds the free tier or doesn't meet the free tier policy will incur fees. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
</dx-alert>



## Directions
### Setting expiry/overdue protection for cloud disks[](id:ExpirationProtection)
1. Log in to the CVM console and select **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs/index)** on the left sidebar.
2. At the top of the **Cloud Block Storage** page, select the region of the cloud disk.
3. Configure the parameter in the following ways as needed:
<dx-tabs>
::: Setting the parameter for one cloud disk
1. Select <img src="https://main.qcloudimg.com/raw/551a994b0ba17786ee196ee2c67635a4.png" style="margin:-3px 0px"> in the top-right corner to open the **Display Settings** window.
2. In the **Display Settings** pop-up window, select **Expiry/Overdue Protection** and click **OK**.
Set other fields as needed.

3. Toggle on **Expiry/Overdue Protection** on the row of the target cloud disk.

:::
::: Configuring the parameter for multiple cloud disks

1. On the **Cloud Disk List** page, select cloud disks and click **Expiry/Overdue Protection** above the list.


2. In the **Expiry/Overdue Protection** pop-up window, click **OK**.
:::
::: Setting the parameter for all the cloud disks in an AZ
1. In the top-right corner of the page, select **Cloud Disk Data Protection Configuration**.
2. In the **Cloud Disk Data Protection Configuration** pop-up window, select **Expiry/Overdue Protection** and select the AZ from the drop-down list.

3. Click **Save**.
:::
</dx-tabs>

### Setting snapshot protection[](id:SnapshotProtection)
1. Log in to the CVM console and select **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs/index)** on the left sidebar.
2. At the top of the **Cloud Block Storage** page, select the region of the cloud disk.
3. Configure the parameter in the following ways as needed:
<dx-tabs>
::: Associating a cloud disk with a scheduled snapshot policy during creation
1. On the **Cloud Block Storage** page, click **Create** above the list.
2. In the **Purchase Data Disk** pop-up window, select **Scheduled Snapshot** and select a scheduled snapshot policy from the drop-down list.

<dx-alert infotype="explain" title="">
For more information on other parameters, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).
</dx-alert>
3. After the cloud disk is created successfully, it can be associated with the selected scheduled snapshot policy.
:::
::: Associating a cloud disk with the default scheduled snapshot policy on the cloud disk purchase page
1. In the top-right corner of the **Cloud Block Storage** page, select **Cloud Disk Data Protection Configuration**.
2. In the **Cloud Disk Data Protection Configuration** pop-up window, select **Snapshot Protection for New Cloud Disks** and select the AZ from the drop-down list.

3. Click **Save**.
<dx-alert infotype="explain" title="">
When you create a cloud disk in the selected AZ, **Scheduled Snapshot** will be selected by default, that is, the cloud disk will be associated with the policy by default. You can deselect the option as needed.
</dx-alert>

:::
</dx-tabs>

## References
- [Creating cloud disks](https://intl.cloud.tencent.com/document/product/362/5744)
- [Scheduled Snapshots](https://intl.cloud.tencent.com/document/product/362/35238)

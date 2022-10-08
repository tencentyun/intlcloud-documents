## Overview
For cloud disks with the data backup point quota configured, Tencent Cloud will automatically create a data backup point for data backup. You can set the quota when purchasing a cloud disk or adjust/return the quota for an existing cloud disk as needed.

This document describes how to adjust the data backup point quota of a cloud disk and the billing details after the adjustment.


<dx-alert infotype="notice" title="">
- Currently, only one data backup point is supported.
- The billing of the data backup point quota is only related to the size of the cloud disk.
- When the number of data backup points becomes 0 after adjustment/return, the data backup point of the existing data disk will be deleted. To retain a backup point, you can convert it into a snapshot as instructed in [Converting Data Backup Point into Snapshot](https://intl.cloud.tencent.com/document/product/362/50029).
</dx-alert>


## Billing After the Adjustment[](id:description)

<dx-tabs>
::: Increasing the data backup point quota
#### Billing rules
- For cloud disks in different billing modes:
 - **Monthly subscribed cloud disks**: To increase the data backup point quota, you need to make up the price difference between new and old configurations for the rest of the lifecycle, subject to the details as displayed on the payment page.
 - **Pay-as-you-go cloud disks**: The adjustment takes effect immediately, and the cloud disks will be billed by the new configuration.
- Billing rules for monthly subscribed cloud disks:
The price difference should be made up based on the number of days. Configuration upgrade fees = price difference for upgrade per month * number of months for upgrade * applicable discount.
 - Price difference for the upgrade per month: Unit price difference between the new and old configurations.
 - Number of months for upgrade: Upgrade fees are calculated by month based on the number of days.
 - Number of days for upgrade = resource expiration time - current time
 - Number of months for upgrade = number of days for upgrade / (365/12)
 - Applicable discount: The applicable discount is matched based on the number of months for upgrade as effective at the official website.

<dx-alert infotype="explain" title="">
- This operation doesn't affect the resource expiration time.
- This operation allows you to use vouchers and free credits for fees deduction.
</dx-alert>




:::
::: Reducing/Returning the data backup point quota

#### Billing rules
- For cloud disks in different billing modes:
  - **Monthly subscribed cloud disks**: After the data backup point quota is reduced, the price difference between the value of the new configuration and the value in the rest of the lifecycle will be refunded, subject to the details as displayed on the payment page.
  - **Pay-as-you-go cloud disks**: The adjustment takes effect immediately, and the cloud disks will be billed by the new configuration.
- Billing rules for monthly subscribed cloud disks:
  Refund for downgrade = fees of original specification - fees of new specification. For more information, see [Refund](https://intl.cloud.tencent.com/document/product/362/36875).
  - If the refund is greater than 0, the data backup point quota will be reduced, and fees will be returned to your Tencent Cloud account accordingly.
  - If the refund is equal to or smaller than 0, the data backup point quota will be reduced, but no fees will be returned.
 - If you use a discount or voucher for purchase, the discount amount and voucher will not be refunded.




:::
</dx-tabs>



## Directions

### Increasing the data backup point quota
You can increase the data backup point quota in the following ways:

<dx-tabs>
::: Increasing the data backup point quota in the console

If the [use limits](https://intl.cloud.tencent.com/document/product/362/50021#restrictions) are met, you can increase the data backup point quota in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs) and select the region of the cloud disk at the top of the page.
2. Find the target cloud disk in the list and select **More** > **Adjust Data Backup Point Quota** on the right.

3. In the **Adjust Data Backup Point Quota** pop-up window, select the target configuration.
4. Click **Next**, confirm the billing details, and select **I have read and agree to the billing details for adjusting the data backup point quota**.
5. Click **OK**.

:::
::: Increasing the data backup point quota via an API
You can use the `ModifyDiskBackupQuota` API to adjust the data backup point quota of a specified cloud disk.
:::
</dx-tabs>




### Reducing/Returning the data backup point quota
You can reduce/return the data backup point quota in the following ways:

<dx-tabs>
::: Reducing/Returning the data backup point quota in the console
If the [use limits](https://intl.cloud.tencent.com/document/product/362/50021#restrictions) are met, you can reduce/return the data backup point quota in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs) and select the region of the cloud disk at the top of the page.
2. Find the target cloud disk in the list and select **More** > **Adjust Data Backup Point Quota** on the right.

3. In the **Adjust Data Backup Point Quota** pop-up window, select the target configuration.
4. Click **Next**, confirm the billing details, and select **I have read and agree to the billing details for adjusting the data backup point quota**.
5. Click **OK**.
:::
::: Reducing/Returning the data backup point quota via an API
You can use the `ModifyDiskBackupQuota` API to adjust the data backup point quota of a specified cloud disk.
:::
</dx-tabs>

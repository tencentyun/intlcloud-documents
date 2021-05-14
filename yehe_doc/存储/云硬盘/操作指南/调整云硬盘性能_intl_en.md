
The performance of a cloud disk depends on its capacity. You can improve the performance to the maximum level by adjusting its capacity. After the basic performance of an enhanced SSD reaches the ceiling, you can configure and adjust extra performance to achieve even higher performance anytime when prerequisites are met. For more information, see [Enhanced SSD Performance](https://intl.cloud.tencent.com/document/product/362/39611).
>!
>- Currently, only **Enhanced SSD** supports independent performance adjustment.
>- The [extra performance](https://intl.cloud.tencent.com/document/product/362/39611#extra-performance) can be independently adjusted only after the [basic performance](https://intl.cloud.tencent.com/document/product/362/39611#basic-performance) reaches the ceiling.
>- The performance adjustment will not affect your cloud disks or businesses.



## Performance Adjustment Billing

### Performance upgrade

- For pay-as-you-go cloud disks: the performance upgrade takes effect immediately, and the cloud disks will be charged by the new configuration.

### Performance downgrade

- For pay-as-you-go cloud disks: the performance downgrade takes effect immediately, and the cloud disks will be charged by the new configuration.

## Performance Upgrade

#### Performance upgrade via the console
When prerequisites are met, you can upgrade performance in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Click **More** > **Adjust Performance** under the **Operation** column of the selected cloud disk.
4. Select a target configuration in the pop-up window.
5. Select descriptions and start the adjustment.

#### Performance upgrade via an API
You can use the `ModifyDiskExtraPerformance` API to upgrade performance of a specified cloud disk.


## Performance Downgrade

#### Performance downgrade via the console
When prerequisites are met, you can downgrade performance in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Click **More** > **Adjust Performance** under the **Operation** column of the selected cloud disk.
4. Select a target configuration in the pop-up window.
5. Select descriptions and start the adjustment.

#### Performance downgrade via an API
You can use the `ModifyDiskExtraPerformance` API to downgrade performance of a specified cloud disk.


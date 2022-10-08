
The performance of a cloud disk depends on its capacity. You can improve the performance to the maximum level by adjusting its capacity. After the basic performance of an enhanced SSD reaches the ceiling, you can configure and adjust extra performance to achieve even higher performance anytime when prerequisites are met. For more information, see [Enhanced SSD Performance](https://intl.cloud.tencent.com/document/product/362/39611).


<dx-alert infotype="notice" title="">
- Currently, only **Enhanced SSD** supports independent performance adjustment.
- The [extra performance](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) can be independently adjusted only after the [basic performance](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD) reaches the ceiling.
- The performance adjustment will not affect your cloud disks or businesses.
</dx-alert>




## Performance Adjustment Billing

### Performance upgrade

- For cloud disks featuring monthly subscription: you need to make up the price difference between new and old configurations for the rest of the lifecycle. You can view the actual details on the payment page.
- For pay-as-you-go cloud disks: the performance upgrade takes effect immediately, and the cloud disks will be charged by the new configuration.

### Performance downgrade

- For cloud disks featuring monthly subscription: the price difference between the value of new configurations and the value in the rest of the lifecycle is refunded. You can view the actual details on the payment page.
- For pay-as-you-go cloud disks: the performance upgrade takes effect immediately, and the cloud disks will be charged by the new configuration.

## Performance Upgrade
<dx-tabs>
::: Performance upgrade via the console
When prerequisites are met, you can upgrade performance in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Select **More** > **Adjust Performance** for the target cloud disk.
4. Select a target configuration in the pop-up window.
5. Select descriptions and start the adjustment.
:::
::: Performance upgrade via an API
You can use the `ModifyDiskExtraPerformance` API to upgrade performance of a specified cloud disk. For detailed directions, see [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).
:::
</dx-tabs>

## Performance Downgrade
<dx-tabs>
::: Performance downgrade via the console
When prerequisites are met, you can downgrade performance in the following ways:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Select **More** > **Adjust Performance** for the target cloud disk.
4. Select a target configuration in the pop-up window.
5. Select descriptions and start the adjustment.
:::
::: Performance downgrade via an API
You can use the `ModifyDiskExtraPerformance` API to downgrade performance of a specified cloud disk. For detailed directions, see [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).
:::
</dx-tabs>


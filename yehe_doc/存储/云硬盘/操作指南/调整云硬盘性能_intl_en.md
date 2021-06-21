
The performance of a cloud disk depends on its capacity. You can improve the performance by adjusting its capacity till it reaches the ceiling. When the ceiling is reached, you can purchase extra performance to get even higher performance. Note that the extra performance is only available for enhanced SSD instances. For more information, see [Enhanced SSD Performance](https://intl.cloud.tencent.com/document/product/362/39611).
>!
>- Currently, only **Enhanced SSD** supports independent performance adjustment.
>- The [extra performance](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) can be independently adjusted only after the [basic performance](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD) reaches the ceiling.
>- The performance adjustment will not affect the running of your cloud disks and businesses.



## Performance Adjustment Billing

### Upgrading

- For pay-as-you-go cloud disks, the performance upgrade takes effect immediately, and the cloud disks are charged by the new configuration right away.

### Downgrading


- For pay-as-you-go cloud disks, the performance upgrade takes effect immediately, and the cloud disks are charged by the new configuration right away.

## Performance Upgrade

#### Upgrading a disk via the console
When prerequisites are met, you can upgrade a disk as instructed below in the console: 

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Click **More** > **Adjust Performance** under the **Operation** column of the selected cloud disk.
4. Select a target configuration in the pop-up window.
5. Read and confirm the notes and start the adjustment.

#### Upgrading a disk via API
You can also use the `ModifyDiskExtraPerformance` API to upgrade a specified cloud disk. For detailed directions, see [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).


## Performance Downgrade

#### Downgrading a disk via the console
When prerequisites are met, you can downgrade a disk as instructed below in the console:

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Select the region and the cloud disk that requires performance adjustment.
3. Click **More** > **Adjust Performance** under the **Operation** column of the selected cloud disk.
4. Select a target configuration in the pop-up window.
5. Read and confirm the notes and start the adjustment.

#### Downgrading a disk via API
You can also use the `ModifyDiskExtraPerformance` API to downgrade a specified cloud disk. For detailed directions, see [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).


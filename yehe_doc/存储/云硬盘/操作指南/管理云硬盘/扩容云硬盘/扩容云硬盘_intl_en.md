## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data in it.
After a cloud disk is expanded, you need to either assign its expanded capacity to an existing partition, or format it into an independent new partition. For more information, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).
>! MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.

## Expanding Data Disks
### Expanding data disks via the CBS console
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Locate the cloud disk to be expanded, and select **More** > **Expand** in the **Operation** column.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Expanding data disk via the CVM Console
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. Locate the CVM on which you want to expand the data disk, and select **More** -> **Resource Adjustment** -> **Expand Data Disk** in the **Operation** column.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Assign its expanded capacity to an existing partition, or format it into an independent new partition. Depending on the operating system of the CVM, see [Extending Partitions and File Systems (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) or [Extending Partitions and File Systems (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Expanding data disk via API
You can use the `ResizeCbsStorage` API to expand the specified cloud disks. For more information, see [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).

## Expanding System Disks
If a system disk is a cloud disk, its capacity can be expanded. However, you have to [reinstall the operating system](https://intl.cloud.tencent.com/document/product/213/4933) of the CVM to implement the expansion.

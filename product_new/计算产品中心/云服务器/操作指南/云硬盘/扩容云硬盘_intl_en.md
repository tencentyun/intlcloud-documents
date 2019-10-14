## Scenario
A cloud disk is an expandable storage device on the cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data.
After a cloud disk is expanded, you need to allocate the added capacity to existing partitions or new partitions. Please refer to [Expanding Windows File System](https://intl.cloud.tencent.com/document/product/362/6737) or [Expanding Linux File System]( https://intl.cloud.tencent.com/document/product/362/6738).
> MBR disks support a maximum disk capacity of 2TB. If your disk is a MBR disk and needs to be expanded to more than 2TB, we recommend that you create and mount a new data disk, initialize it to GPT, and copy the data on the MBR disk to the new disk.

## Expanding data disks
### Expanding via the Cloud Block Storage (CBS) Console
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs).
2. Select **More** > **Expand** to the right of the cloud disk you want to expand.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Allocate the added capacity to existing partitions or new partitions. For details, see [Expanding Windows File System](https://intl.cloud.tencent.com/document/product/362/6737) or [Expanding Linux File System]( https://intl.cloud.tencent.com/document/product/362/6738) depending on the operating system of the cloud services you want to use.

### Expanding via the CVM Console
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Select **More** > **Resource Adjustment** > **Adjust Disk** to the right of the CVM you want to make change to.
3. Select a new capacity. It must be greater than or equal to the current capacity.
4. Complete the payment.
5. Allocate the added capacity to existing partitions or new partitions. For details, see [Expanding Windows File System](https://intl.cloud.tencent.com/document/product/362/6737) or [Expanding Linux File System]( https://intl.cloud.tencent.com/document/product/362/6738) depending on the operating system of the cloud services you want to use.

### Expanding via API
You can create a snapshot with the ResizeCbsStorage API. For details, see [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310).

## Expanding system disks
If a system disk is a cloud disk, you can expand it, but only by [reinstall the system](https://intl.cloud.tencent.com/document/product/213/4933) of the CVM.

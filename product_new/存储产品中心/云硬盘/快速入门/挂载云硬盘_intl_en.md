This article helps you understand how to mount cloud disks by using mounting an empty elastic cloud disk called `cbs-test` to a CVM in the Beijing region as an example. For more information on mounting cloud disks, see [Mounting cloud disks](https://intl.cloud.tencent.com/document/product/362/31594).
>Cloud disks can only be mounted to CVMs in the same availability zone.

## Prerequisites
- You have already [created a cloud disk](https://intl.cloud.tencent.com/document/product/362/31647), `cbs-test`.
You must ensure that you have an available CVM under the region and availability zone where you create the cloud disk (in this example, Beijing Zone 1). For information on how to purchase and launch a CVM, see [Purchase and launch a CVM](https://intl.cloud.tencent.com/document/product/213/4855).

## Connecting to a CVM instance
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. In the cloud disk list page, click **More**>**Mount** in the row of the `cbs-test` cloud disk.
3. In the pop-up box select the cloud disk to be mounted to the CVM, and click **OK**.
  >You can check **Release upon instance termination** according to actual circumstances.
  >
  Return to the cloud disk list page. The cloud disk status is now **Mounting**, indicating that the cloud disk is in the process of being mounted to a CVM. When the CVM status is **Mounted**, it indicates that mounting to a CVM is successful.


## Subsequent Operations
After the cloud disk is mounted, the cloud disk is used as the CVM’s data disk. The status is offline by default. You must perform initialization operations such as formatting, partitioning, and creating a file system on the data disk. For more information, see [Initializing cloud disk](https://intl.cloud.tencent.com/document/product/362/31646).


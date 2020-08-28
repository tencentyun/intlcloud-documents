## Cloud disk purchase channels

Tencent Cloud provides two ways for you to purchase cloud disks, either through the console or via API. 

<span id="CreateDisk"></span>
### Purchasing directly through the console
1. Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs), select a region and click **Create**.
2. Configure the cloud disk type and capacity.
3. Select a billing method.
4. Confirm the order and then pay.
5. The cloud disk is created immediately after the order payment. Cloud disk can be used after being mounted and initialized.

### Using snapshots to purchase through the console
If you want to save the snapshot data of a data disk to a new disk by default, you can use snapshot to create a cloud disk in the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot). You can also configure the **Snapshot** parameter to specify the target snapshot for creating a disk when you [purchase it separately through the console](#CreateDisk).
1.Go to [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) on the console.
2. In the row of the target snapshot, select **More**>**Create new disk**.
3. Configure the cloud disk type and capacity.
 >When you use snapshot to create a cloud disk, the capacity size must not be smaller than the snapshot size. If you do not specify the cloud disk capacity, the capacity will be the same as that of the snapshot by default.
4. Select a billing method.
5. Confirm the order and then pay.
6. The cloud disk is created immediately after the order payment. Cloud disk can be used after being mounted and initialized.

### Purchasing along with a CVM
- When you purchase a Tencent Cloud CVM, you can also purchase a non-elastic cloud disk by setting **System Disk** to cloud disk. For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).
- You can purchase an elastic cloud disk by setting the **Data Disk** parameter when purchasing a CVM. For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).

### Purchasing through an API
You can use the `CreateDisks` API to create a cloud disk. For more information, see [Creating cloud disks](https://intl.cloud.tencent.com/document/product/362/16312).

## Purchase channels for local disks
Currently, local disks can be purchased only when you purchase a High-IO or Big-Data CVM instance, and cannot be purchased separately. For more information, see [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).


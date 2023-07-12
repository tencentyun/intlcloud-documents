## Cloud Disk Purchase Channels

Tencent Cloud provides two ways for you to purchase cloud disks, either through the console or via API.


### Purchasing in the console[](id:CreateDisk)
1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs), select a region, and click **Create**.
2. Configure the cloud disk type and capacity.
3. Set **Billing Mode**. If you select **Monthly Subscription**, you need to set the **Purchase Validity Period**.
4. After confirming the order, make the payment using account balance, online banking, WeChat Pay, or QQ Wallet.
5. The cloud disk is created immediately after the order payment. Cloud disk can be used after being mounted and initialized.

### Using snapshots to purchase through the console
If you want to save the snapshot data of a data disk to a new disk by default, you can use a snapshot to create a cloud disk on the [**Snapshot List**](https://console.cloud.tencent.com/cvm/snapshot) page. You can also configure the **Snapshots** parameter to specify a snapshot for cloud disk creation when [purchasing a cloud disk in the console](#CreateDisk).
1. Go to the [Snapshot List](https://console.cloud.tencent.com/cvm/snapshot) page.
2. On the row of the target snapshot, select **More** > **Create Cloud Disk**.
3. Configure the cloud disk type and capacity.
<dx-alert infotype="explain" title="">
When you create a cloud disk with a snapshot, the disk capacity cannot be smaller than that of the snapshot. If you don't specify the capacity of the cloud disk, the capacity is equal to that of the snapshot by default.
</dx-alert>
4. Set **Billing Mode**. If you select **Monthly Subscription**, you need to set the **Purchase Validity Period**.
5. After confirming the order, make the payment using account balance, online banking, WeChat Pay, or QQ Wallet.
6. The cloud disk is created immediately after the order payment. Cloud disk can be used after being mounted and initialized.

### Purchasing along with a CVM
- You can purchase a non-elastic cloud disk by purchasing a CVM instance and setting a cloud disk as the **system disk**. For more information, see [Creating Instances](/doc/product/213/4855).
- You can purchase an elastic cloud disk by purchasing a CVM instance and setting the **Data Disk** parameter. For more information, see [Creating Instances](/doc/product/213/4855).

### Purchasing through an API
You can use the `CreateDisks` API to create a cloud disk. For more information, see [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).

## Purchase channels for local disks

Currently, local disks can only be purchased when you purchase a High I/O or Big Data CVM instance. Separate purchase is not supported. For more information, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).



You can create a cloud disk and connect it to any CVM instance in the same availability zone. Through block storage device mapping, the cloud disk is recognized and used by CVM instances. You can also launch a new cloud disk based on the snapshots you just created. For more information, please see [Create Cloud Disk from Snapshot](/doc/product/362/5757). The created cloud disk can reach its optimal performance without warm-up.

The method to create cloud disk varies with types of cloud disks. 

## Creating an Elastic Cloud Disk 

### Creating an elastic cloud disk in console

1) Log in to the [CBS Console](https://console.cloud.tencent.com/cvm/cbs), and then click **Create** to purchase a cloud disk.

2) In the pop-up box, select a region/availability zone, billing method (only "Prepaid" is supported), capacity, quantity and purchased usage period, and then click **OK**.

3) On the payment page, click **Confirm Payment** to complete the purchase. On the [Cloud Disk List Page](https://console.cloud.tencent.com/cvm/cbs), you can view the purchased cloud disks. The elastic cloud disk you just purchased is unnamed by default and displayed as <font color="red">To Be Mounted</font>.

> Note:
> 
- An elastic cloud disk can be freely mounted and unmounted between CVMs in the same availability zone.
- The capacity of a single disk can be set to 10-4,000 GB, and a maximum of 10 elastic cloud disks can be created at a time.
- To keep the data disk snapshot on the new disk, enable **Create Disk Using Snapshot** on the page and select the snapshot you want. The default disk capacity equals the size of the selected snapshot. You can change the capacity to a value greater than the default value.

### Creating an elastic cloud disk using snapshot
If you need to keep the data disk snapshot on the new created disk, you can select this method.

1) Log in to the [Snapshot Console](https://console.cloud.tencent.com/cvm/snapshot), and click **Create Cloud Disk** next to the snapshot you want to purchase the disk.

2) In the pop-up box, select a region/availability zone, billing method (only "Prepaid" is supported), capacity, quantity and purchased usage period, and then click **OK**.
> Note:
> 
- An elastic cloud disk can be freely mounted and unmounted between CVMs in the same availability zone.
- The default capacity of a new disk equals the size of the snapshot. You can change the capacity to a value greater than the default value.
- A maximum of 10 elastic cloud disks can be created at a time.

3) On the payment page, click **Confirm Payment** to complete the purchase. On the [Cloud Disk List Page](https://console.cloud.tencent.com/cvm/cbs), you can view the purchased cloud disks. The elastic cloud disk you just purchased is named From snap-xxxxxxxx by default and displayed as <font color="red">To Be Mounted</font>.




## Creating a Non-Elastic Cloud Disk
### Creating a non-elastic could disk in console
Non-elastic cloud disks are cloud disks created with instances and have the same lifecycle as instances. For more information about how to create an instance with non-elastic cloud disk selected, please see [Purchase and Launch Instances](/doc/product/213/4855).

### Creating a non-elastic cloud disk using API
Non-elastic cloud disks are cloud disks created with instances and have the same lifecycle as instances. For more information about how to create an instance with non-elastic cloud disk selected, please see [API RunInstances](https://intl.cloud.tencent.com/doc/api/229/1248) and [API RunInstancesHour](https://intl.cloud.tencent.com/doc/api/229/1350)

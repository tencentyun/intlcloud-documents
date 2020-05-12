## Introduction to LVM
Logical Volume Manager (LVM) divides your disks or partitions into units of physical extents (PEs) with the same size by creating a logical layer over the disks and partitions. It works by combining different disks or partitions into the same volume group (VG), so that you can create logical volumes (LVs) within the VG, and file systems on the LVs.
Compared with using disk partitions directly, LVM supports scaling your file systems elastically.
- The file system is no longer limited by the size of physical disk. Instead, it can be distributed across multiple disks:
For example, you can purchase 3 elastic cloud disks of 4 TB, and use LVM to create a massive file system up to 12 TB.
- You can resize the LVs dynamically instead of repartitioning your disks.
When the LVM VG capacity cannot meet your needs, you can purchase a separate elastic cloud disk to mount on your CVM instance, and scale your VG by adding the cloud disk to it.

## Building LVM
>The following example uses 3 elastic cloud disks to create a dynamically resizable file system through LVM:
![](https://main.qcloudimg.com/raw/81086e80477ff7e374e7c3f0fe9d2788.png)

### Step 1 Create physical volume (PV)
1. [log In to the Linux CVM](https://intl.cloud.tencent.com/document/product/213/5436) as root user.
2. Run the following command to create PVs:
```
pvcreate <disk path 1> ... <disk path N>
```
Take `/dev/vdc`, `/dev/vdd` and `/dev/vde` as an example, then run:
```
pvcreate /dev/vdc /dev/vdd /dev/vde
```
The following figure shows the command output when the creation is successful:
![](https://main.qcloudimg.com/raw/5b92a6c7878e22906599af48bfa09d95.png)
3. View physical volumes in the current system with the
```
lvmdiskscan | grep LVM
```
![](https://main.qcloudimg.com/raw/1de75af4a49c2deea689a2576eb075d9.png)

### Step 2 Create volume group (VG)
1. Run the following command to create a volume group:
```
vgcreate [-s <specified PE size>] <VG name> <PV path>.
```
Assume you want to create a VG named “lvm_demo0”, then run
```
vgcreate lvm_demo0 /dev/vdc /dev/vdd
```
The following figure shows the command output when the creation is successful:
![](https://main.qcloudimg.com/raw/3b8dba3329f62e85d2075fad10898632.png)
 When "Volume group" <VG name> "successfully created" is displayed, your VG has been created successfully.
 - Once created, you can add a new PV to the VG with the
```
vgextend VG name New PV path
```
The following figure shows the command output when the operation is successful:
![](https://main.qcloudimg.com/raw/105e5a77472f173ffd4a58624f20a863.png)
 - Once created, you can run `vgs`, `vgdisplay` or other commands to view the VG(s) in the current system, as shown below:
![](https://main.qcloudimg.com/raw/309c991d32cf4b801ddbe8d898f1bfbb.png)

### Step 3 Create logical volume (LV)
1. Run the following command to create a LV:
```
lvcreate [-L <LV size>][-n <LV name>] <VG name>.
```
Assume you want to create an 8 GB logical volume named "lv_0", then run
```
lvcreate -L 8G -n lv_0 lvm_demo0.
```
The following figure shows the command output when the creation is successful:
![](https://main.qcloudimg.com/raw/ed6d2f827ae7c4a4630bf17e24d90df2.png)
>Run `pvs`, and you can see that the 8 GB comes solely from the `/dev/vdc` as shown below:
>[](https://main.qcloudimg.com/raw/2718d08f7c74b7b469a23473a1398dfe.png)

### Step 4 Create and mount file system
1. Create a file system on an existing LV using the command
```
mkfs.ext3 /dev/lvm_demo0/lv_0.
```
2. Mount the file system with the
```
mount /dev/lvm_demo0/lv_0 vg0/.
```
The following figure shows the command output when the mount is successful:
![](https://main.qcloudimg.com/raw/2a7701636c2604d67e0743de4f9a6af1.png)

### Step 5 Perform dynamic scaling on your logical volume and file system
>LVs can be scaled dynamically only when the VG capacity is not fully occupied. When you scale a LV’s capacity, you also need to scale the file system created on this LV.

1. Scale a LV by running this command
```
lvextend [-L +/- <capacity amount>] <LV path>.
```
Assume you want to scale up the capacity of LV named “lv_0” by 4 GB, then run
```
lvextend -L +4G /dev/lvm_demo0/lv_0.
```
The following figure shows the command output when the scaling is successful:
![](https://main.qcloudimg.com/raw/eccd7d6aec587eb90ec655a384367595.png)

> Run `pvs`, and you can find that `/dev/vdc` has been fully used, and 2 G has been used from `/dev/vdd` as shown below:
>[](https://main.qcloudimg.com/raw/189155ca377ef9550c4587ca78ab5b27.png)
2. Scale the file system with the command
```
resize2fs /dev/lvm_demo0/lv_0.
```
The following figure shows the command output when the scaling is successful:
![](https://main.qcloudimg.com/raw/2e37f35678014ab1ca398fe5470a754b.png)
Once completed, you can run the following command to see if the capacity of your LV has been changed to 12 GB:

```
df -h
```

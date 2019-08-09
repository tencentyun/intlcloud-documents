An instance can recognize the connected cloud disk and regard it as an HDD cloud disk. You can use any file system to format and partition the cloud block storage device, and create file systems. Any data written to the file systems is then written to the cloud disk and is transparent to the applications that use the device. The data disks are offline by default, and cannot be used before being partitioned and formatted. This document shows how to partition and format disks in the Windows system.

The path to "Disk Management" may vary with the Windows version (Windows 2012, Windows 2008, Windows 2003, etc.), but the steps to partition and format the disks are basically the same.

This document will guide you through the mounting, partitioning and formatting of data disks in Windows 2012.

## Prerequisites
- Make sure you have [connected cloud disk to the CVM instance](/doc/product/362/5745), and [logged in to Windows instance](/doc/product/213/5435).
- <font color="red">After formatting, all the data in the data disk will be cleared. Before formatting, make sure there is no data in the data disk or important data has been backed up. To avoid service exceptions, ensure that the CVM has stopped external services before formatting.</font>
- If you purchased multiple cloud disks, it is recommended to set a custom name for the elastic cloud disk that stores important data and set auto renewal for it to prevent the impact on your business due to the failure to renew the expired elastic cloud disk in a timely manner. 
- You can locate a cloud disk quickly based on the custom name or the private IP of associated CVM in [CBS Console](https://console.cloud.tencent.com/cvm/cbs).

## Making a Disk Online, and Partitioning and Formatting the Disk in Windows 2012
### Making a disk online
In Windows 2012, you can go to **Start** -> **Server Management** -> **Tools** -> **Computer Management** -> **Disk Management** to manage disks.

Click **Start**:

![](https://main.qcloudimg.com/raw/b0f8bc5b77972807c94274245f57f695.png)

Click **Server Management**:

![](https://main.qcloudimg.com/raw/d582ebea07d7b9a3634429ec6077458a.png)

Click **Tools** -> **Computer Management**:

![](https://main.qcloudimg.com/raw/62c88537707bb943d103f3aeaebdd5ea.png)

Click **Disk Management**:

![](https://main.qcloudimg.com/raw/5b3e2698b88aa49048407f45dbf99b32.png)

As shown in the figure below, right click on Disk 1, and then select **Online**:

![](https://main.qcloudimg.com/raw/745b4ec44900b46bbcf74b1bf31b87b5.png)

If the disk already contains data (non-empty disk), you can ignore the following steps. Reformatting or partitioning a non-empty disk will <font color="red">clear all existing data on it</font>.

### (Optional) Select **GPT** or **MBR** 

Select **GPT** or **MBR** :

![](https://main.qcloudimg.com/raw/5a385d39dade7289c83683477659cd2f.png)
![](https://main.qcloudimg.com/raw/058b256cea0f31d9fc0e7ebea1ebb353.png)


> **Note:**
> Only GPT partitioning format is supported when disk is larger than 2 TB. If you are not sure whether the disk capacity will exceed this value after subsequent expansion, GPT partitioning format is recommended; if you're sure that the disk capacity will not exceed this value, you're recommended to select MBR partitioning for a better compatibility.

### (Optional) Partitioning a disk
Right-click in the unallocated space and select **New Simple Volume**:

![](https://main.qcloudimg.com/raw/75bb03ce4c9838c50d3ee83349d8f458.png)

In the **New Simple Volume Wizard** pop-up window, click **Next**:
![](https://main.qcloudimg.com/raw/6d69a186bcaeb8af76f8afb9a87bed65.jpg)


Enter the desired disk size for the partition, and then click **Next**:
![](https://main.qcloudimg.com/raw/5cdad86adf5f429678d8fc9ebeb01a04.png)

Enter the drive letter, and then click **Next**:

![](https://main.qcloudimg.com/raw/bdc7a25a05e22d7a41ab64f6b44bd99a.jpg)

Choose to format the partition, select file system, and then click **Next**:
![](https://main.qcloudimg.com/raw/cdb416973c2065f1fa024f096a92bc82.jpg)


Click **Finish** to create the new simple volume:

![](https://main.qcloudimg.com/raw/b9012a1b1a31379883eae79e0bcd1dba.jpg)

Check the new partition:

![](https://main.qcloudimg.com/raw/0d03bb0e63f728b44f7d9425f8328f73.jpg)

![](https://main.qcloudimg.com/raw/88c8cacaedd8f4c0c0f6bdcd133f39ae.jpg)



## Online Setting
In the Windows operating system, you often need to set online in disk management. To make it easier for you to use elastic cloud disk, we recommend making the following modifications to the operating system:

Open the cmd command line and execute the following command:
```
diskpart
san policy=onlineall
```
![](https://main.qcloudimg.com/raw/2c6c9747904011e2f24e2e77714c10a6.png)

After this operation, when an elastic cloud disk with valid file system is remounted to Windows CVM, you can use this disk directly without additional operations.

## Mounting a data disk automatically when launching new instance using custom images and data disk snapshots
When a new CVM instance is launched, if you specify ***custom image*** and ***data disk snapshot***, Tencent Cloud's cloud disk can be automatically mounted after the launch of CVM instance (read and write data directly without the need to perform operations such as addition, partitioning and formatting). You need to perform some operations on the original instance before making custom images and data disk snapshots, which will be described in detail below.

On the Windows system, if you want the cloud disk produced from the specified data disk snapshot to be automatically mounted to the new CVM instance, the specified custom image and data disk snapshot must meet the following requirements:

- The SAN policy in the custom image is `onlineAll`. Public images for Windows provided by Tencent Cloud have been configured as such, but it is recommended to check the configuration before creating any custom image by following the step below:
![](https://main.qcloudimg.com/raw/e6f24c6ce5866c91b68644c854712098.png)

- The data disk must have been formatted as `ntfs` or `fat32` before you make a snapshot.

Only when both of the conditions are met can the data disk of the launched Windows CVM instance be automatically recognized and mounted.

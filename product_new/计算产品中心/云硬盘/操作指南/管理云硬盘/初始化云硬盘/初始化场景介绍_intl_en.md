After a cloud disk is manually mounted, the cloud disk is used as the CVM’s data disk. The default status is offline. You must perform initialization operations such as formatting, partitioning and creating a file system. We recommend you select an initialization method according to your actual use cases:
- If the entire disk is presented as one independent partition (that is, there are not multiple logical disks such as D disk/vdb1 and E disk/vdb2), we strongly recommend you not use partitions, and directly create the file system on bare devices.
- If the entire disk needs to be presented as multiple logical partitions (that is, there are multiple logical disks), you need to perform the partitioning first, then create the file system on a partition. 

Common disk partition styles are Main Boot Record (MBR) and Guid Partition Table (GPT). If the disk partition format is changed after the disk is put into use, original data on the disk will be erased. Therefore, select an appropriate partition style according to actual needs.
Basics of the two partition styles are shown in the following table.

| Partition style | Maximum supported disk capacity | Number of partitions supported | Partition tool |
|---------|---------|---------|---------|
|MBR | 2TB |<li>4 primary partitions</li><li>3 primary partitions and 1 extended partition</li>|Windows operating system: Disk management</br>Linux operating system:<ul><li>fdisk tool</li><li>parted tool</li></ul> |
|GPT | 18EB</br>Currently, cloud disk supports a maximum capacity of 16TB | No limit on number of partitions | Windows operating system: Disk management</br>Linux operating system: parted tool|

Select the appropriate operations guide according to disk capacity and the CVM‘s operating system type:
- For disk capacity less than 2TB:
 - [Initializing cloud disks (Windows)](https://intl.cloud.tencent.com/document/product/362/31597#initializing-cloud-disks-(windows))
 - [Initializing cloud disks (Linux)](https://intl.cloud.tencent.com/document/product/362/31597#initializing-cloud-disks-(linux))
- For disk capacity larger than or equal to 2TB:
 - [Initializing cloud disks (Windows)](https://intl.cloud.tencent.com/document/product/362/31598#initializing-cloud-disks-(windows))
 - [Initializing cloud disks (Linux)](https://intl.cloud.tencent.com/document/product/362/31598#initializing-cloud-disks-(linux))










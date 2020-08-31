## Introduction to RAID
RAID (Redundant Array of Independent Disks) combines multiple disks into a disk array in order to improve data read and write performance and reliability. Meanwhile, the operating system will use the disk array as a single hard disk. RAID has multiple levels at present. The following will introduce RAID0, RAID1, RAID01 and RAID10. Depending on the level of RAID, the disk array offers improvement benefits in data integration, fault tolerance, and throughput or capacity compared with a large hard disk with considerable capacity.

>Note:
>- please [renew](https://intl.cloud.tencent.com/document/product/362/36874) your elastic cloud disk that is about expire to avoid impact on your RAID array due to forced isolation of the disk.
>- We recommend you use partitions of the same size when creating RAID 1, RAID 01, and RAID 10 for minimal waste of disk capacity.

 The following is a comparison of different RAID levels:
<table>
     <tr>
         <th nowrap="nowrap">RAID Level</th>  
         <th>Description</th>  
		 <th>Pros and Cons</th>
		 <th>Scenarios (Recommended)</th>
     </tr>
	 <tr>
         <td>RAID 0</td>
				 <td>Storage mode: Data are striped and stored in different disks.<br/></br>Virtual disk size: the combined capacity of all disks in the array.</td>
		 </td>
		 <ul><li><b>Pros</b>: Read and write can be synchronized. </br>Theoretically, the read and write rate can be N times that of a single disk (N is the number of disks in RAID0), despite practical limitations such as file size, file system size, etc.</li>
		 <li><b>Cons</b>: No data redundancy. If a single disk is damaged, it is likely to cause all data lost in the most serious cases.</li></ul></td>
		 <td>Require a higher level of I/O performance, and have backed up data through other means or there is no need for data backup.</td>
     </tr> 
	 <tr>
         <td>RAID 1</td>
         <td>Storage mode: Data are stored through image memory into disks.<br /></br>Virtual disk size: depends on the capacity of the disk with the smallest one in the array.</td>
		 </td>
		 <ul><li><b>Pros</b>:<ul>
		 <li>Fast read.</li>
		 <li>High data reliability. Damage to a single disk will not result in unrepairable data.</li>
		 </ul>
		 <li><b>Cons</b>:<ul>
		 <li>Low disk utilization.</li>
		 <li>The write speed is limited by that of a single disk.</li>
		 </ul></ul>
		 </td>
		 <td>Require high read performance and backups of written data.</td>
     </tr>
	 <tr>
         <td>RAID 01</td>
         <td>First deal with data through RAID0, then RAID1.</td>
		 <td><ul><li><b>Pros</b>: Take into both RAID0 and RAID1 advantages.</li>
		 <li><b>Cons</b>:<ul><li>Costs are relatively high and it is essential to use at least 4 disks.</li><li>The damage of a single disk will make the other disks unavailable in the same array.</li></td>
		 <td   rowspan="2">-</td>
     </tr>
	 <tr>
         <td>RAID 10</td>
         <td> Build RAID 1 with multiple disks, and then build RAID 0 with more than one RAID 1.</td>
		 <td><ul><li><b>Pros</b>: Take into both RAID0 and RAID1 advantages.</li>
		 <li><b>Cons</b>: Costs are relatively high and it is essential to use at least 4 disks.</li></td>
     </tr>
</table>



## Building RAID
>The following describes how to build RAID 0 on CentOS by using 4 Tencent Cloud elastic cloud disks. The operation may vary for different operating systems (OS) and RAID levels. Since this document is for reference only, for detailed instructions and differences, please see the product documentation for a specific OS or relevant RAID documents.

Linux kernel provides a MD module that manages RAID devices, so you may create RAID 0 by directly calling this module using the mdadm tool.
![](https://main.qcloudimg.com/raw/a7e717737b22456319cde4ec4bc0c8e1.png)

1. [log In to the Linux CVM] (https://intl.cloud.tencent.com/document/product/213/5436) as root user.
2. Run the following command to install mdadm.
```
yum install mdadm -y
```
success result is as shown below:
![](https://main.qcloudimg.com/raw/9ae334a316638ebc8e8b95a587c6e8b5.png)
3. Run the following command to create RAID 0 using mdadm.
```
mdadm --create /dev/md0 --level=0 --raid-devices=4 /dev/vd[cdef]1
```
success result is as shown below:
![](https://main.qcloudimg.com/raw/7c2d92dc0cf8225d56c6696127e1a6ce.png)
4. Run the following command to create a file system using mkfs (take EXT3 file system as an example).
```
mkfs.ext3 /dev/md0
```
success result is as shown below:
![](https://main.qcloudimg.com/raw/ed6291597a03923a46914ff39005c90e.png)
5. Run the following commands in sequence to mount the file system.
```
mkdir md0/
mount /dev/md0 md0/
tree md0
```
success result is as shown below:
![](https://main.qcloudimg.com/raw/c77863517336227b6dc5dc0180935e46.png)
6. Run the following command to view the file system details and record its UUID (take `c5d8a204:c28853ba:3882e9f8:62d078de` as an example) as shown below:
```
mdadm --detail --scan
```
![](https://main.qcloudimg.com/raw/bd258e727fc5ca5ee67ffe7ffeddea2a.png)
7. Run the following command to edit mdadm configuration file.
```
vi /etc/mdadm.conf
```
8. In Edit mode, enter your configuration information.
It is recommended to write the following configuration for elastic cloud disks:
```
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 1-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 2-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 3-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 4-part1 
ARRAY logical device path metadata= UUID=
```
Assume the logical device path is /dev/md0 and metadata is 1.2, and you should enter:
```
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 1-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 2-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 3-part1 
DEVICE /dev/disk/by-id/virtio-ID of elastic cloud disk 4-part1 
ARRAY /dev/md0 metadata=1.2 UUID=3c2adec2:14cf1fa7:999c29c5:7d739349
```
9. Press Esc, enter `:wq` to save and exit.

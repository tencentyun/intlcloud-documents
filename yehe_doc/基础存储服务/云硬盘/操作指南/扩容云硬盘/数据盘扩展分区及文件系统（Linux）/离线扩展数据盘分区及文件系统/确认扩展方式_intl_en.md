## Overview
A cloud disk is an expandable storage device on cloud. After a cloud disk is created, you can expand its capacity at any time to increase its storage capacity without losing any data in it.
After [expanding cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/5747) on the console, you need to log in to the CVM instance to assign its expanded capacity to an existing partition using an appropriate method as needed. This document describes how to determine the expansion method on a Linux CVM.

<dx-alert infotype="notice" title="">
Extending the file system may affect the existing data. We recommend you manually [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) to back up your data before the operation.
</dx-alert>



## Prerequisite
- You have [expanded the cloud disk via the console](https://intl.cloud.tencent.com/document/product/362/5747).
- You have [mounted the cloud disk](https://intl.cloud.tencent.com/document/product/362/32401) to a Linux CVM and created a file system.
- You have [logged in to the Linux instance](https://intl.cloud.tencent.com/document/product/213/5436) that requires extending partitions and file systems.

## Directions
1. Run the following command as the root user to view the partition format of the cloud disk.[](id:fdisk)
```shellsession
fdisk -l
```
 - If the result only shows `/dev/vdb` without a partition, you need to extend the file system.
 ![](https://main.qcloudimg.com/raw/661ad0745c10a44035697cf4d03759f5.png)
 - If the result is as shown in the following two figures (which may vary according to the operating system), the GPT partition format should be used.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - If the result is as shown in the following figure (which may vary according to the operating system), the MBR partition format should be used.
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2. Choose the expansion method corresponding to the partition format obtained in [step 1](#fdisk).
<dx-alert infotype="notice" title="">
- MBR partition supports disk with a maximum capacity of 2 TB.
- When you partition a disk with a capacity greater than 2 TB, we recommend you create and mount a new data disk and use the GPT partition format to copy data. 
</dx-alert>
<table>
     <tr>
         <th nowrap="nowrap">Partition format</th>  
				 <th>Expansion method</th>  
         <th>Remarks</th>  
     </tr>
		 	 <tr>      
         <td>N/A</td>   
	     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/362/40952">Extending File Systems on Bare Devices</a></td>
			 <td>Applicable to scenarios where a file system is created directly on a bare device and <b>no partition is created</b>.</td>
     </tr>
	 <tr>      
         <td rowspan="2">GPT</td>   
	     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/362/39997">Extending GPT Partitions and File Systems (Larger than 2 TB)</a></td>
	     <td>Applicable to scenarios of direct formatting when no partition is created.</td>
     </tr> 
	 <tr>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/39997">Extending GPT Partitions and File Systems (Larger than 2 TB)</a></td> 
	     <td>Applicable to scenarios where the original partitions remain unchanged and a new GPT partition is created for expansion.</td>
     </tr> 
	 <tr>
         <td rowspan="2">MBR</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/362/39998">Extending MBR Partitions and File Systems (Smaller than 2 TB)</a></td> 
	     <td>Applicable to scenarios of direct formatting when no partition is created.</td>
     </tr> 
	 <tr>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/39998">Extending MBR Partitions and File Systems (Smaller than 2 TB)</a></td> 
	     <td>Applicable to scenarios where the original partitions remain unchanged and a new MBR partition is created for expansion.</td>
     </tr> 
</table>







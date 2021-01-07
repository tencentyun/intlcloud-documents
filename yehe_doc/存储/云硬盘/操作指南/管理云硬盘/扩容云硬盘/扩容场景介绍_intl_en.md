### Expanding the capacity of cloud system disks
If the cloud disk is a system disk, you can expand it using the following two methods.
- [Expanding cloud disks via the CVM console](https://intl.cloud.tencent.com/document/product/362/5747)
- [Reinstalling system](https://intl.cloud.tencent.com/document/product/362/5747)



### Expanding the capacity of cloud data disks

If the cloud disk is a data disk, you can expand it using the following three methods.
- [Expanding cloud disks via the CVM console](https://intl.cloud.tencent.com/document/product/362/5747)
- [Expanding cloud disks via the CBS console](https://intl.cloud.tencent.com/document/product/362/5747)
- [Expanding cloud disks via API](https://intl.cloud.tencent.com/document/product/362/5747)




Based on the **mounting** status of CBS data disks, you can expand their capacity by different methods.
- If the current CBS data disk **can be unmounted**, you can expand its capacity in the CBS console or via the [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310) API.
- If the current CBS data disk **cannot be unmounted**, you can expand its capacity in the CVM console or via the [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310) API.

>! If the maximum capacity of the cloud disk cannot meet your business needs, please try [building up RAID groups](https://intl.cloud.tencent.com/document/product/362/2932) or [building LVM logical volumes with multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2933).

Once the data disk capacity is expanded, you must perform the following operations for the instance to recognize and use the data disk:
<table>
     <tr>
         <th nowrap="nowrap">Before Expansion</th>  
         <th nowrap="nowrap">After Expansion</th>  
		 <th>Subsequent Operations</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">No file system is created.</td>
         <td>Disk capacity is less than 2 TB.</td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (smaller than 2 TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Disk capacity is greater than or equal to 2 TB.</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2 TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">File system has already been created.</td>
         <td>Disk capacity is less than 2 TB.</td>
    		 <td><ul><li>The expanded cloud disk is on a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a></li>
			 <li>The expanded cloud disk is on a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Disk capacity is greater than or equal to 2 TB.</td>
         <td>
				 <ul><li>GPT partition format:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extending partitions and file systems (Windows)</a> or <a href="https://intl.cloud.tencent.com/document/product/362/31602">extending partitions and file systems (Linux)</a></li>
				 <li>MBR partition format: Not supported.</li>MBR partition supports disk with a maximum capacity of 2 TB. When you partition disk with a capacity greater than 2 TB, we recommend that you create and mount a new data disk and use the GPT partition format to copy data.</ul>
				 </td>
     </tr>
</table>



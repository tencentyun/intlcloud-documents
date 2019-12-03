### Expanding the Capacity of Cloud System Disks

For data security considerations, you cannot expand the capacity of CVM system disks in the console directly. Instead, you must [reinstall the system](https://intl.cloud.tencent.com/document/product/213/4933) to expand the capacity of the system disks.
> When you reinstall the system to adjust the system disk capacity, you can only maintain or increase the capacity, but you cannot reduce the capacity.
>

### Expanding the Capacity of Cloud Data Disks

When cloud disks serve as data disks, you can expand the capacity of cloud disks either in the console or with an API. Note that you can only maintain or increase the capacity, but you cannot reduce the capacity.
Based on the **mounting** status of CBS, you can expand the capacity of a data disk by different means.
- If the current cloud data disk is **can be unmounted**, you can expand its capacity in the cloud disk console or through the [ResizeDisk](https://cloud.tencent.com/document/product/362/16310) API.
- If the current cloud data disk is **cannot be unmounted**, you can expand its capacity in the CVM instance console or through the [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310) API.

> If the maximum capacity of the cloud disk does not meet your business needs, you can try [Building Up RAID Groups](https://intl.cloud.tencent.com/document/product/362/2932) or [Building Up LVM Logic Volumes](https://intl.cloud.tencent.com/document/product/362/2933).
>
Once the data disk capacity is expanded, you must perform the subsequent operations before the instance can recognize and use the data disk:
<table>
     <tr>
         <th nowrap="nowrap">Before Expansion</th>  
         <th nowrap="nowrap">After Expansion</th>  
		 <th>Subsequent Operations</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">No file system is created.</td>
         <td>Disk capacity is less than than 2 TB.</td>
		 <td><a href="https://cloud.tencent.com/document/product/362/6734">Initialize cloud disks (less than 2 TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Disk capacity is greater than or equal to 2 TB.</td>
         <td><a href="https://cloud.tencent.com/document/product/362/6735">Initialize cloud disks (greater than or equal to 2 TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">File system is already created.</td>
         <td>Disk capacity is less than 2 TB.</td>
    		 <td><ul><li>The expanded cloud disk is a Windows CVM instance: <a href="https://cloud.tencent.com/document/product/362/6737">Expand partitions and file systems (Windows).</a></li>
			 <li>The expanded cloud disk is a Linux CVM instance: <a href="https://cloud.tencent.com/document/product/362/6738">Expand partitions and file systems (Linux)</a>.</li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Disk capacity is greater than or equal to 2 TB.</td>
         <td>
				 <ul><li>GPT partition format: <a href="https://cloud.tencent.com/document/product/362/6737">Expand partitions and file systems (Windows)</a> or <a href="https://cloud.tencent.com/document/product/362/6738">expand partitions and file systems (Linux)</a></li>
				 <li>MBR partition format: Not supported.</li>The MBR partition format supports a maximum disk capacity of 2 TB. If your disk partition is in the MBR format and you want to expand its capacity to beyond 2 TB, we recommend that you create and mount a new data disk, adopt the GPT partition format, and copy the data to the new disk.</ul>
				 </td>
     </tr>
</table>

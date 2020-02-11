### Expanding the capacity of cloud system disks

For data security, CVM cloud disks cannot be expanded directly in the console. You must [reinstall the system](https://intl.cloud.tencent.com/document/product/213/4933) to expand the capacity of the system disks.
> When reinstalling the system to adjust the system disk capacity, you can only maintain or increase the capacity, not reduce it.
>

### Expanding the capacity of cloud data disks

Cloud disks that serve as data disks can be expanded directly in the console or via an API. Note that you can only maintain or increase the capacity, not reduce it.
Based on the **mounting** status of CBS data disks, you can expand their capacity by different means.
- If the current CBS data disk **can be unmounted**, you can expand its capacity in CBS console or via the [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310) API.
- If the current CBS data disk **cannot be unmounted**, you can expand its capacity in CVM instance console or via the [ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310) API.

> If the maximum capacity of the cloud disk cannot meet your business needs, you can try [building up RAID groups](https://intl.cloud.tencent.com/document/product/362/2932) or [building up LVM logic volumes](https://intl.cloud.tencent.com/document/product/362/2933).
>
Once the data disk capacity is expanded, you must perform the following operations for the instance to recognize and use the data disk:
<table>
     <tr>
         <th nowrap="nowrap">Before Expansion</th>  
         <th nowrap="nowrap">After Expansion</th>  
		 <th>Subsequent Operations</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">No file system is created.</td>
         <td>Disk capacity is less than than 2 TB.</td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initialize cloud disks (less than 2 TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Disk capacity is greater than or equal to 2 TB.</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initialize cloud disks (greater than or equal to 2 TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">File system has already been created.</td>
         <td>Disk capacity is less than 2 TB.</td>
    		 <td><ul><li>The expanded disk is a Windows CVM cloud disk: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Expand partitions and file systems (Windows).</a></li>
			 <li>The expanded disk is a Linux CVM cloud disk: <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expand partitions and file systems (Linux)</a>.</li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Disk capacity is greater than or equal to 2 TB.</td>
         <td>
				 <ul><li>GPT partition format: <a href="https://intl.cloud.tencent.com/document/product/362/31601">Expand partitions and file systems (Windows)</a> or <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expand partitions and file systems (Linux)</a></li>
				 <li>MBR partition format: Not supported.</li>MBR partition format supports a maximum disk capacity of 2TB. If your disk partition is in MBR format and its capacity needs to be expanded beyond 2TB, we recommend you create and mount a new data disk, and use GPT partition format to copy the data to the new disk.</ul>
				 </td>
     </tr>
</table>

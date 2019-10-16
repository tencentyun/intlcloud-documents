### Expanding cloud disks of the system disk type

For data security, CVM system disk cannot be directly expanded in the console. You must [reinstall system](https://intl.cloud.tencent.com/document/product/213/4933) to expand the system disk capacity.
>When the system disk capacity is changed by reinstalling the system, the capacity can only be maintained or expanded, not decreased.
>

### Expanding cloud disks of the data disk type

Cloud disk of the data disk type supports expansion operations through the console and API. Note that you can only maintain or expand the capacity, not reduce it.
Depending on whether the CBS data disk is **unmountable**, you can choose different operation entries to perform expansion on data disks.
- If the current disk is a **can be unmounted** CBS data disk, you can perform expansion operations through the cloud disk console or by using the [CBS ResizeDisk API](https://intl.cloud.tencent.com/document/product/362/16310).
- If the current disk is a **cannot be unmounted** CBS data disk, you can perform expansion operations through the CVM instance console or by using the [CVM ResizeInstanceDisks API](https://intl.cloud.tencent.com/document/product/362/16310).

>If the maximum capacity of the cloud disk still does not meet your business needs, you can [build RAID 0 using multiple elastic cloud disks](https://intl.cloud.tencent.com/document/product/362/2932) or [build LVM logical volumes](https://intl.cloud.tencent.com/document/product/362/2933).
>
After expanding the data disk, you must perform the subsequent operations before it can be recognized and used by the instance:
<table>
     <tr>
         <th nowrap="nowrap">Before Expansion</th>  
         <th nowrap="nowrap">After Expansion</th>  
		 <th>Subsequent Operations</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">No file system created</td>
         <td>Disk capacity smaller than 2TB</td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Initializing cloud disks (smaller than 2TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Disk capacity larger than or equal to 2TB</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Initializing cloud disks (larger than or equal to 2TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">A file system is already created</td>
         <td>Disk capacity smaller than 2TB</td>
    		 <td><ul><li>Expanded cloud disk belongs to a Windows CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31601">Expanding partitions and file systems (Windows)</a></li>
			 <li>Expanded cloud disk belongs to a Linux CVM:<a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Disk capacity larger than or equal to 2TB</td>
         <td>
				 <ul><li>Using the GPT partition format:<a href="https://intl.cloud.tencent.com/document/product/362/31601"> Expanding partitions and file systems (Windows)</a> or <a href="https://intl.cloud.tencent.com/document/product/362/31602">Expanding partitions and file systems (Linux)</a></li>
				 <li>Using the MBR partition format: Not supported</li>MBR partition format supports a maximum disk capacity of 2TB. If your disk partition is in MBR format, and it needs to be expanded to more than 2TB, we recommend you create and mount a new data disk, then use the GPT partition format and copy the data to the new disk.</ul>
				 </td>
     </tr>
</table>

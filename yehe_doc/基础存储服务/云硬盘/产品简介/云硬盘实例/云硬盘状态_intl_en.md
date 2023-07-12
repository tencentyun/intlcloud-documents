Cloud disk has the following status:

<table>
     <tr>
         <th>Status</th>  
         <th>Attribute</th>  
         <th>Description</th>  
     </tr>
	 <tr>      
         <td nowrap="nowrap">To be mounted</td>   
	     <td nowrap="nowrap">Stable status</td>
	     <td>The status after the cloud disk has been created and before it is mounted to a CVM.</td>
     </tr> 
	 <tr>      
         <td>Mounting</td>   
	     <td>Interim status</td>
	     <td>When the cloud disk is being mounted, it enters the **mounting** status.</td>
     </tr> 
	 <tr>      
         <td>Mounted</td>   
	     <td>Stable status</td>
	     <td>The status when the cloud disk has been mounted to a CVM in the same availability zone.</td>
     </tr> 
	 <tr>      
         <td>Unmounting</td>   
	     <td>Interim status</td>
	     <td>When the cloud disk is being unmounted, it enters the **unmounting** status.</td>
     </tr> 
	 <tr>      
         <td>To be repossessed</td>   
	     <td>Stable status</td>
	     <td>The status when a cloud disk that has not been renewed within the specified period after expiration, or a cloud disk with monthly subscription that has been manually terminated, is sent to the recycle bin after being suspended (the disk is unavailable, and can only store data) and forced to unmount.</td>
     </tr> 
	 <tr>      
         <td>Terminated</td>   
	     <td>Stable status</td>
	     <td>The cloud disk is not renewed and retrieved before its storage time in the recycle bin expires, or the termination operation is completed. The original cloud disk no longer exists, and data has been completely erased.</td>
     </tr> 
</table>

The conversion relationship between cloud disk statuses is shown in the following figure:
![](https://main.qcloudimg.com/raw/096ea77e63990160092f22bcc3ff69ad.png)

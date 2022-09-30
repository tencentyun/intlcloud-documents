## Use Limits on Cloud Disk
<table>
<tr>
		<th width="23%">Limit Type</th>
		<th>Description</th>
	</tr>
	<tr>
	  <td>Enhanced SSD usage</td>
		<td> 
		<ul style="margin-bottom:0px">
		<li>Currently, Enhanced SSD is only available in certain AZs and will be supported in more AZs in the future. You can check the information on the purchase page.</li>
		<li>The performance of Enhanced SSD is only guaranteed when it's attached to S5, M5, and SA2 models created after August 1, 2020, and all later generation models, for example, Standard S5, S6, and later.</b>
		<li>Enhanced SSD cannot be used as the system disk.</li>
		<li>Enhanced SSD cloud disks cannot be encrypted.</li>
		<li>Enhanced SSD cannot be upgraded from other disk types.</li>
	</ul>
	</td>
	</tr>
<tr>
	  <td>ulTra SSD usage</td>
		<td>
		<ul style="margin-bottom:0px">
		<li>Currently, ulTra SSD is only available in certain AZs and will be supported in more AZs in the future. You can check the information on the purchase page.</li>
		<li><b>ulTra SSD can only be purchased together with Standard Storage Optimized S5se instances.</b></li>
		<li>ulTra SSD cannot be purchased independently.</li>
		<li>ulTra SSD cannot be used as the system disk.</li>
		<li>ulTra SSD cannot be encrypted.</li>
		<li>ulTra SSD cannot be upgraded from other disk types.</li>
		</ul>
		</td>
	</tr>
	<tr>
		<td>Elastic cloud disk capability</td>
		<td>Starting from May 2018, all data disks purchased upon creation of CVMs are elastic cloud disks. You can detach them from and re-attach them to CVMs. This feature is supported in all availability zones.</td>
	</tr>
	<tr>
		<td>Cloud disk performances</td>
		<td>I/O specification applies to both input and output performance at the same time.<br/>For example, if a 1-TB SSD has a maximum random IOPS of 26,000, it means that both its read and write performance can reach this value. Due to performance limits, if the block size in this example is 4 KB or 8 KB, the maximum IOPS can be reached. If the block size is 16 KB, the maximum IOPS cannot be reached (throughput has already reached the limit of 260 MB/s).</td>
	</tr>
	<tr>
	<td>Max attachable elastic cloud disks per CVM</td>
	<td>Up to 20.</td>
	</tr>
		<tr>
	<td>Number of cloud disks created at a time</td>
	<td>Up to 50.</td>
	</tr>
		<tr>
	<td>Limits on the number of instances to which a cloud disk can be attached</td>
	<td>
	<ul style="margin-bottom:0px">
	<li>Cloud disks and instances (CVM or Lighthouse instances) to which they are attached must be in the same AZ.</li>
	<li><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud disks</a> of CVM instances are independent of <a href="https://intl.cloud.tencent.com/document/product/1103/46567">cloud disks</a> of Lighthouse instances. Cloud disks of CVM instances cannot be attached to Lighthouse instances, and vice versa.</li>
	</ul>
	</td>
	</tr>
	<tr>
		<td>Repossession of cloud disks in arrears</td>
		<td>When a monthly-subscribed cloud disk expires and you do not renew it within 7 days after the expiry, it will be forcibly unmounted from the CVM (if any), and moved to the recycle bin. For details about the repossession mechanism, see <a href="https://intl.cloud.tencent.com/document/product/362/31625">Arrears</a>.<br>Currently, when you <a href="https://intl.cloud.tencent.com/document/product/362/32401">mount</a> a monthly-subscribed cloud disk to monthly-subscribed CVM, the following renewal method are available:
			<ul style="margin-bottom:0;">
			<li>Renew the cloud disk when the associated CVM expires</li>
			<li>Renew the cloud disk automatically on a monthly basis after it expires.</li>
			<li>Mount directly without a renewal policy.</li>
			</ul>
		</td>
	</tr>
</table>


## Use Limits on Snapshot
<table>
<tr>
		<th width="23%">Limit Type</th>
		<th>Description</th>
	</tr>
		<tr>
		<td>Supported disk type</td>
		<td>You can only use the data disk snapshot to create elastic cloud disks, while using the system disk snapshot to create a custom image.</td>
	</tr>
		<tr>
	<td>Capacity of cloud disk created using a snapshot</td>
	<td>The capacity of the cloud disk created using a snapshot should be greater than or equal to that of the snapshot.</td>
	</tr>
			<tr>
			<td>Snapshot rollback</td>
			<td>Snapshot data can only be rolled back to the source cloud disk from which the snapshot was created. If you want to create a cloud disk with data in an existing snapshot, see <a href="https://intl.cloud.tencent.com/document/product/362/5757">Creating Cloud Disks Using Snapshots<a>.
		</td>
	</tr>
	<tr>
		<td>Total snapshot size</td>
		<td>No limit.</td>
	</tr>
	<tr>
		<td>Snapshot quota in one region</td>
		<td>64 + the number of cloud disks in the region * 64.</td>
	</tr>
</table>

## Use Limits on Scheduled Snapshot Policy
<table>
<tr>
		<th width="40%">Limit Type</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>Scheduled snapshot policy quota in one region</td>
		<td>A single Tencent Cloud account can set a maximum of 32 scheduled snapshot policies in each region.</td>
	</tr>
	<tr>
		<td>Number of scheduled snapshot policies being associated with one cloud disk</td>
		<td>A cloud disk can associate with a maximum of 10 scheduled snapshot policies in the same region.</td>
	</tr>
	<tr>
		<td>Number of cloud disks associated with one scheduled snapshot policy</td>
		<td>A scheduled snapshot policy can be associated with a maximum of 200 cloud disks in the same region.</td>
	</tr>
</table>

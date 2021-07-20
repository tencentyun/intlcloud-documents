## Use Limits on Cloud Disk
<table>
<tr>
		<th width="22%">Limit Type</th>
		<th>Description</th>
	</tr>
	<tr>
	  <td>Enhanced SSD usage</td>
		<td> 1. Currently, Enhanced SSD is only available in some availability zones. <br>2. The performance of Enhanced SSD is only guaranteed when it’s attached to S5, M5, and SA2 models created after August 1, 2020, and all later generation models. <br>3. Enhanced SSD cannot be used as the system disk.<br>4. Enhanced SSD cannot be encrypted.<br>5. Enhanced SSD cannot be upgraded from other disk types.</td>
	</tr>
<tr>
	  <td>Tremendous SSD usage</td>
		<td> 1. Currently, Tremendous SSD is only available in certain availability zones, as shown in the CBS purchase page. It will be supported in more availability zones.<br>2. <b>Tremendous SSD can only be purchased with the Standard Storage Optimized S5se CVM instance.</b><br>3. Tremendous SSD cannot be purchased independently.<br>4. Tremendous SSD cannot be used as the system disk.<br>5. Tremendous SSD cannot be encrypted.<br>6. Tremendous SSD cannot be upgraded from other disk types.</td>
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
	<td>One CVM can have a maximum of 20 cloud disks attached.</td>
	</tr>
		<tr>
	<td>Attaching</td>
	<td>A cloud disk can only be attached to a CVM in the same availability zone.</td>
	</tr>
</table>

## Use Limits on Snapshot
<table>
		<th width="22%">Limit Type</th>
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
		<td>A single Tencent Cloud account can set a maximum of 30 scheduled snapshot policies in each region.</td>
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

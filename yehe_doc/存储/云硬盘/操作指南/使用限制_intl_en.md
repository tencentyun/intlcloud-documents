## Use Limits on Cloud Disk
<table>
<tr>
		<th width="22%">Limit Type</th>
		<th>Description</th>
	</tr>
	<tr>
	  <td>Enhanced SSD usage</td>
		<td> 1. Currently, Enhanced SSD is only available in Guangzhou Zone 3, Guangzhou Zone 4, Shanghai Zone 2, Shanghai Zone 3, Shanghai Zone 5, Beijing Zone 3, Beijing Zone 4, Chengdu Zone 1, Chongqing Zone 1, Nanjing Zone 1, Nanjing Zone 2, and Qingyuan Zone 1. It will be supported in more availability zones.<br>2. Enhanced SSD only supports mounting to S5, M5, SA2, IT3, and D3 models created after August 1, 2020, or a new release in the future.<b>The performance of Enhanced SSD cannot be assured if it is mounted to earlier or existing instances.</b><br>3. Enhanced SSD cannot be used as the system disk.<br>4. Enhanced SSD cannot be encrypted.<br>5. Enhanced SSD cannot be upgraded from other disk types.</td>
	</tr>
	<tr>
		<td>Elastic cloud disk capability</td>
		<td>Starting in May 2018, all data disks purchased with CVMs are elastic cloud disks, which support unmounting and remounting to CVMs. This feature is supported in all availability zones.</a></td>
	</tr>
	<tr>
		<td>Cloud disk performances</td>
		<td>I/O performance takes effect concurrently.<br/>For example, if a 1-TB SSD has a maximum random IOPS of 26,000, its IOPS for both reads and writes can reach this value. Due to performance limits, if the block size in this example is 4 KB or 8 KB, the maximum IOPS can be reached. If the block size is 16 KB, the maximum IOPS cannot be reached (throughput has already reached the limit of 260 MB/s).</td>
	</tr>
		<tr>
	<td>Maximum number of elastic cloud disks mounted to one CVM</td>
	<td>One CVM can have a maximum of 20 cloud disks mounted.</td>
	</tr>
		<tr>
	<td>Cloud disks mounted to CVM</td>
	<td>A cloud disk can be mounted to any CVM in the same availability zone.</td>
	</tr>
	<tr>
		<td>Repossession of cloud disks in arrears</td>
		<td>If your monthly subscription cloud disk is not renewed within 7 days after it expires, it will be forcibly unmounted from a CVM (if any), and be repossessed to the recycle bin. For more information about the repossession mechanism, see <a href="https://intl.cloud.tencent.com/document/product/362/31625">Arrears</a>.<br>Currently, when you <a href="https://intl.cloud.tencent.com/document/product/362/32401">mount</a> a monthly subscription cloud disk to monthly subscription CVM, you can choose the following renewal method as needed:
			<ul style="margin-bottom:0;">
			<li>Set the same expiry time as the CVM.</li>
			<li>Renew cloud disk automatically on a monthly basis after it expires.</li>
			<li>Mount directly without a renewal policy.</li>
			</ul>
		</td>
	</tr>
</table>

## Use Limits on Snapshot
<table>
<tr>
		<th width="22%">Limit Type</th>
		<th>Description</th>
	</tr>
		<tr>
		<td>Type of cloud disks created using a snapshot</td>
		<td>You can only use the data disk snapshot to create elastic cloud disks, while using the system disk snapshot to create a custom image.</td>
	</tr>
		<tr>
	<td>Capacity of cloud disks created using a snapshot</td>
	<td>You can use a snapshot to create an elastic cloud disk whose capacity is greater than or equal to that of the snapshot.</td>
	</tr>
			<tr>
			<td>Snapshot rollback</td>
			<td>Snapshot data can only be rolled back to the source cloud disk where the snapshot was created. If you want to create cloud disks with existing snapshot, see <a href="https://intl.cloud.tencent.com/document/product/362/5757">Creating Cloud Disks Using Snapshots<a>.
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

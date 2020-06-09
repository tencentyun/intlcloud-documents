### Is snapshot available in all availability zones?
Yes, the snapshot feature is available in all availability zones.

### Does snapshot creation affect disk performance?
Creating a snapshot will occupy a small amount of the disk I/O. We recommend creating snapshots when business is slow.

### How long does it take to create a snapshot?
The time for creating a snapshot is subject to factors such as the number of disk writes, and the underlying read-write operations, but this process does not affect your use of the disk.

### Do I need to shut down the CVM to roll back snapshots?
- For a cloud disk that has been mounted to a CVM, you have to shut down the CVM during rollback.
- For a cloud disk that is not mounted, you can directly perform rollback.

### How is the size of the first full snapshot of a cloud disk calculated?
The first snapshot created on a cloud disk is a full snapshot that copies all the data of the cloud disk at a point in time. The snapshot size equals the used capacity of the cloud disk. For example, if the capacity of a cloud disk is 200 GB and 122 GB of its storage space is used, the size of the first full snapshot is 122 GB.

### Can I download or export CVM instance snapshots to a local device?
No. Snapshots cannot be downloaded or exported to local devices. You need to create a custom image from a snapshot and then export the image.

### Do automatic snapshots differ from or conflict with manual snapshots?
No. You can use both of them at the same time. However, you cannot create manual snapshots while automatic snapshots are being created.
- You cannot create a custom snapshot of a disk until its automatic disk snapshot has been created, and vice versa.
- If one snapshot created from a large disk lasts longer than two automatic snapshot intervals, the next automatic snapshot will be skipped automatically. For example, if you configure that the automatic snapshots will be created at 9:00, 10:00 and 11:00, the automatic snapshot being created at 9:00 lasts for 70 minutes and ends at 10:10, the next automatic snapshot will be created at 11:00 but not at 10:00.

### Can I create snapshots for local disks?
No. We recommend that you use data redundancy at the application layer or create deployment sets for clusters to improve the availability of applications.

### Are local snapshots deleted after I release the cloud disk?
No. You need to delete snapshots via console or API. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Why does the used disk capacity displayed in the file system differ from the snapshot size?
A cloud disk snapshot is a block-level clone or backup. In general, the snapshot capacity will be larger than the data amount displayed in the file system due to the fact that:
- The underlying data block stores metadata of the file system.
- Some data are deleted. Deleting data modifies the data block that has been written in, which will be backed up in snapshots.

### How can I prevent snapshots from being deleted by Tencent Cloud?
- Manual snapshots: they are never deleted by Tencent Cloud no matter whether their corresponding disk or instance has been released.
- Scheduled snapshots: to prevent them from being deleted, you can set the save cycle of scheduled snapshots to permanent retention. Then, only the earliest snapshots are deleted when the snapshot quota is reached. For more information, see [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/362/35238) and [Use Limits](https://intl.cloud.tencent.com/document/product/362/32406)

### How can I delete snapshots to reduce backup costs?
- For cloud disk snapshots, you can delete them directly via console or API. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).
- For snapshots associated with custom images, you must first delete custom images, and then [Delete Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).

### Are automatic snapshots deleted after the instance expires or the cloud disk is released?
No. Automatic snapshots will not be automatically deleted after the instance expires or the cloud disk is released, they are retained based on the save cycle policy of scheduled snapshots. To modify the policy of scheduled snapshots, see [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/362/35238)?

### How can I delete cloud disk snapshots from which an image is created?
- Snapshots from which a cloud disk is created: you can delete the snapshots separately, but then, you cannot operate a business that depends on the original snapshot data.
- Snapshots from which a custom image is created: you have to first delete the image, and then the snapshots.
- Snapshots from which an instance is created: you can delete the snapshots separately, but then, you cannot operate a business that depends on the original snapshot data..

### Will the snapshot policy fail to be executed if I create a custom image or cloud disk based on the scheduled snapshot?
No.


### Can a cloud disk have multiple automatic snapshot policies?
No.

### How can I avoid data loss due to incorrect operations?
You can create snapshots to back up data before you perform risky operations. For example, you can create a snapshot if you need to modify critical system files, migrate instances from a classic network to a VPC, back up data, restore an instance that was released accidentally, prevent network attacks, change operating systems, or provide data support for a production environment. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755). If an error occurs, you can [Roll Back Snapshots](https://intl.cloud.tencent.com/document/product/362/5756) to reduce risks.

### I created an instance in Guangzhou region and created snapshots for data disks of the instance. I purchased another instance in Guangzhou region after the previous one expired and was released. Can I roll back the snapshots to the new instance?
No. Snapshots can only be rolled back to the cloud disk in which they are created. You can use one of these snapshots to create a cloud disk and mount the cloud disk to the new instance. For more information, see [Creating Cloud Disks using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757) and [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).

### What are the differences between snapshots and images?
If no data disk is mounted to an instance and all data is written on the system disk, the data on the system disk cannot be protected by creating an image. Images cannot be scheduled for continuous backup. Once the system disk data is damaged, you can only recover the data to the state when the image was initially created. Therefore, images are not suitable for data protection. Specific differences are as follows:
<table>
		<tr>
		<th width="10%">Name</th>
		<td width="45%">Snapshots</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Images</a></td>
		</tr>
		<tr>
		<th>Characteristics</th>
			<td>Backup data of a cloud disk at a certain point in time</td>
	   	<td>CVM software configuration template, contains information including the operating system and pre-installed programs</td>
		</tr>
		<tr>
		<th>Use Cases</th>
		<td>
			</ul>
				<li>Regularly back up important business data</li>
				<li>Back up data before major operations</li>
				<li>Produce multiple copies of data</li>
			</ul>
		</td>
		<td>
			</ul>
				<li>Back up systems that remain unchanged in a short term</li>
				<li>Deploy applications in batches</li>
				<li>Migrate the system</li>
			</ul>
		</td>
		</tr>
</table>

### How can I migrate snapshot data from account A to account B?
Snapshots cannot be migrated. If needed, you can create an image from the snapshot that you want to migrate and share the image with another account.

### Can I create a custom image from data disk snapshots?
No. You must use system disk snapshots to create a custom image.




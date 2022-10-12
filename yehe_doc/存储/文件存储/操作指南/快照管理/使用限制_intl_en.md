The free beta of the Tencent Cloud Snapshot product is scheduled to end on August 15, 2022. During beta, all snapshots are stored for free. After beta, snapshot data will be stored, but billing will start. You can adjust your snapshot scale based on your business requirements before the end of beta.

- During beta, feature limitations are as follows:
<table>
	<tr><th>Item</th><th>Limitation During Beta</th></tr>
	<tr><td>Number of snapshots</td><td>Each file system has a snapshot quota of 100 snapshots.</td></tr>
	<tr><td>File system capacity allowed for snapshot creation</td><td>Less than 32 TiB (Allocated capacity. After file system mounting, you can run the `df -h` command to view the total capacity of the file system.)</td></tr>
	<tr><td>Number of scheduled snapshot policies</td><td>30</td></tr>
	<tr><td>Number of file systems that can be bound to a scheduled snapshot policy</td><td>200</td></tr>
</table>
- File system snapshots can be created by using either of the following methods: Copy-On-Write (COW) and Redirect-On-Write (ROW).
- If the snapshot status of a file system is **Migrating**, the snapshot of the file system has been taken (metadata captured and original file system data marked), and the migration is taking place.
- During snapshot migration, the file system can be used properly. You can overwrite, modify, and delete files in the file system without affecting snapshot data migration nor causing snapshot file loss.
- Creating the first snapshot for a file system may take a while as all data in the file system needs to be migrated, and follow-up snapshots are faster to create, because they are incremental or differential backups.
- Currently, only the Standard type supports snapshot, while the High-Performance and Turbo series don't. This support will be added for the High-Performance type on August 15, 2022.
- During snapshot migration, the I/O performance of the file system may decrease by about 15%. You are advised to configure scheduled snapshot policies and take snapshots during off-peak hours of businesses.

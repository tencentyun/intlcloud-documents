## Feature Description
When there is too much data in a cluster instance, you can store some cold data in a COS bucket and hot data on a CDWCH local disk to save storage costs without compromising CDWCH's data query performance. 
## Terms
- Hot data: Frequently accessed or recently created data, which is stored on the cloud or local disk selected at the time of cluster creation for efficient data access.
- Cold data: Less frequently accessed data, which can be stored on a cold data disk to save storage costs and meet data access needs.
- Tiered storage of hot/cold data provides three data moving methods. Parts that satisfy the TTL policy will be moved first; if the storage capacity is still exceeded, large parts will be moved first, as further described below: 
	- Storage capacity policy: Newly written data is stored to a hot data disk for efficient query. When the amount of stored hot data reaches the usage threshold, the data on the hot data disk will be automatically moved to the cold data disk to free up the storage space of the hot data disk.
	- TTL-based tiered storage policy: A TTL statement is added to the default storage policy to automatically move all data older than the time interval to a cold data disk.
	- Data can be manually moved between hot and cold data disks.

<dx-alert infotype="notice" title="Notes">
- This feature is applicable to CDWCH v21.3.9.83 or later. If your instance is not supported, upgrade it to v21.3.9.83 or later first.
- During tiering, the cluster will be restarted and become inaccessible.
- To use tiered storage, add the `SETTINGS storage_policy = 'hot_to_cold';` statement to specify the storage policy during table creation or dynamically modify the storage policy of the table (which must be `default` before the change).
- The storage policy cannot be modified once specified.
- The tiered storage feature cannot be disabled once enabled.
- Due to network restraints, you need to have a COS bucket in the same region as the cluster to perform tiered storage.
</dx-alert>

## Directions
1.	Log in to the [CDWCH console](https://console.cloud.tencent.com/cdwch). When creating a cluster, enable cold backup storage on the tiered storage page and select a previously created COS bucket (you need to purchase one in the same region).
According to the cluster policy, when the used storage space reaches 90%, a cold data tiering mechanism will be automatically triggered by default, where large data parts will be transferred from the local disk to the configured COS bucket first until the used space drops below the threshold. You can configure the tiering table with the following command as needed: `ALTER TABLE xx MODIFY SETTINGS storage_policy = 'hot_to_cold'`.
![](https://qcloudimg.tencent-cloud.cn/raw/5d6381188bebfd40af59703798268a05.jpg)
2. To enable data tiering after a cluster is created, select **Operation** > **More** > **Configure Hot-Cold Tiered Storage** in the cluster list.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ebbae0c4857b91bbc978efa7f65b5e61.jpg)
3. After tiering is configured, view or adjust the hot data tiering coefficient on the cluster details page.
![](https://qcloudimg.tencent-cloud.cn/raw/bb7212267332e901b769a3b4a3a68f3e.jpg)
4. If tiering is triggered, you can log in to the COS console and go to the COS bucket details page to query cold data files.

## Moving Hot-Cold Tiered Data
1. After tiered storage is enabled, the parameters of the default storage policy are as described below:
<table>
<thead>
<tr>
<th >Parameter</th>
<th >Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>move_factor</td>
<td>When the proportion of the available storage space of the hot data disk is below this value, the oldest data written to the hot data disk will be automatically moved to the cold data disk. The valid value is a floating point number between 0 (exclusive) and 1 (inclusive). The default value is 0.1, indicating that data will be automatically moved when the proportion of available storage space is below 10%. This parameter can be modified through the tiered storage policy in the console.</td>
</tr>
<tr>
<td>prefer_not_to_merge</td>
<td> Specifies whether to merge the data on the cold data disk. Valid values:<br> true: no<br>false (default): yes.</br></td>
</tr>
<tr>
<td>max_data_part_size</td>
<td> Maximum part size. Parts on the hot data disk exceeding this size will be moved to the cold data disk. The default value is 0 (unlimited).</td>
</tr>
</tbody>
</table>

2. Set the TTL-based tiered storage policy.
You can add a TTL statement to the default storage policy to automatically transfer all data older than the time interval to the cold data disk. You can also set the part expiration time by setting the TTL at the **table level** for data migration. The calculation result of the expression must be of the `Date` or `Datetime` type. **The TTL needs to be expressed by the `INTERVAL` operator of a `Datetime` or `Date` field**. For the moving characteristics of a part, all rows in the part must meet the moving expression.
You can add a TTL statement according to the following syntax. The TTL can be set to `TO DISK 'cold_disk'` or `TO VOLUME 'cold'` (with the same effect), and the name can be viewed through the `system.disks` and `system.storage_policies` system tables.
```
TTL 
 + INTERVAL 
 TO DISK 'cold_disk' 
```
Parameter description
<table>
<thead>
<tr>
<th >Parameter</th>
<th >Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>time_column</td>
<td>Column of `Date` or `Datetime` type .</td>
</tr>
<tr>
<td>number</td>
<td>Time interval in days, weeks, months, or years.</td>
</tr>
</tbody>
</table>
Example
To move all data older than 90 days (based on the date column) to the cold data disk, use the following table creation statement:
```
CREATE TABLE ttl_test_tbl
(
    `f1` String,
    `f2` String,
    `f3` Int64,
    `f4` Float64,
    `date` Date
)
ENGINE = MergeTree()
PARTITION BY date
ORDER BY f1
TTL date + INTERVAL 90 DAY TO DISK 'cold_disk'
SETTINGS storage_policy = 'hot_to_cold';
```

  - Change the TTL-based tiered storage policy
You can change the column of `Date` or `Datetime` type and time interval of the TTL-based tiered storage policy.
>?
>- After the TTL-based tiered storage policy is modified, all existing and new data will be stored according to the new policy by default.
>- If you don't want the change to the TTL-based tiered storage policy to take effect for existing data, run the `set materialize_ttl_after_modify=0;` statement first before modifying the policy. In this way, only new data will be stored according to the new policy.
>- After the TTL-based tiered storage policy is modified, data on the cold data disk will not be automatically moved to the hot data disk, but it can be manually moved.

You can modify the TTL-based tiered storage policy according to the following syntax:
```
 ALTER TABLE 
 MODIFY TTL 
 + INTERVAL 
 TO DISK 'cold_disk'; 
```
Parameter description
<table>
<thead>
<tr>
<th >Parameter</th>
<th >Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>table_name</td>
<td>Table name.</td>
</tr>
<tr>
<td>time_column</td>
<td>Column of `Date` or `Datetime` type after the change.</td>
</tr>
<tr>
<td>number</td>
<td>Time interval in days, weeks, months, or years after the change.</td>
</tr>
</tbody>
</table>

3. Move the data on the hot or cold data disk.

  - Check the location of the current part or partition before moving:
```
select partition,name,table,disk_name,database from system.parts where active=1
```

  - Find the part or partition to be moved by using the following syntax:
```
ALTER TABLE table_name MOVE PART｜PARTITION  partition_expr TO VOLUME ' volume_name';
```
  - Move data from the hot data disk to the cold data disk.
```
ALTER TABLE 
MOVE PARTITION <partition>
	 TO DISK 'cold_disk'; ALTER TABLE 
MOVE PARTITION <partition>
	TO VOLUME 'cold'; 
```
  - Move data from the cold data disk to the hot data disk.
```
ALTER TABLE 
ON CLUSTER default MOVE PARTITION  
TO DISK 'default'; ALTER TABLE 
ON CLUSTER default MOVE PARTITION 
TO VOLUME 'hot'; 
```

## Possible Problems During Use
1. After tiering, data will be first written to the hot data disk. If the data imported at a time exceeds the remaining available capacity of the hot data disk, an error may be reported, indicating that the disk has no remaining space.
2. Only the kernel on v21.6 or later supports the COS connection retry mechanism. If time-consuming operations such as join are performed on an earlier version, the following error may be reported. This is because it takes CDWCH more than a certain period of time to read files after connecting to COS. In this case, you can adjust the SQL statement or upgrade the version.
![](https://qcloudimg.tencent-cloud.cn/raw/bea6fb2cabe02f857f431d5405070fb2.png)

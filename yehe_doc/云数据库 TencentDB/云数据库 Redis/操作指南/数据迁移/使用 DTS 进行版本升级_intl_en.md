
## Overview
TencentDB for Redis 4.0 and 5.0 Memory Edition instances in [standard architecture](https://intl.cloud.tencent.com/document/product/239/31959) or [cluster architecture](https://intl.cloud.tencent.com/document/product/239/18336) feature more flexible specification configuration, higher performance, and better functionality. If you are using an earlier version of Redis, we recommend that you upgrade to Redis 4.0 or 5.0 for a better TencentDB service experience.

TencentDB for Redis instance version can now be upgraded through Data Transmission Service (DTS) with hot migration, which guarantees instance service continuity during the upgrade process and can update incremental data in real time.

| Term | Description | 
|---------|---------|
| Source instance | Source instance for version upgrade | 
| Target instance | Target instance for version upgrade | 

#### Supported versions
<table>
    <tr>
    <td rowspan=2 align=center>Source Instance Version</td>
    <td colspan=4 align=center>Target Instance Version</td>
    </tr>
    <tr>
    <td>4.0 Memory Edition (standard architecture)</td>
		<td>4.0 Memory Edition (cluster architecture)</td>
		<td>5.0 Memory Edition (standard architecture)</td>
		<td>5.0 Memory Edition (cluster architecture)</td>
    </tr>
    <tr>
    <td>2.8 Memory Edition (standard architecture)</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td>4.0 Memory Edition (standard architecture)</td>
    <td>N/A</td>
    <td>✓</td>
	  <td>✓</td>
		<td>✓</td>
    </tr>
		<tr>
    <td>4.0 Memory Edition (cluster architecture)</td>
    <td>N/A</td>
		<td>N/A</td>
    <td>✓</td>
		<td>✓</td>
    </tr>
		<tr>
    <td>5.0 Memory Edition (standard architecture)</td>
    <td>N/A</td>
		<td>N/A</td>
		<td>N/A</td>
    <td>✓</td>
    </tr>
</table>


## Prerequisites
- The source TencentDB for Redis instance should be running properly.
- You have purchased TencentDB for Redis 4.0 or 5.0 Memory Edition instances in standard architecture or cluster architecture.
>?If your existing data is less than 12 GB with incremental data of no more than 60 GB and QPS of no more than 40,000, or your business requires transactional support, TencentDB for Redis 4.0 or 5.0 Memory Edition (standard architecture) is recommended; otherwise, TencentDB for Redis 4.0 or 5.0 Memory Edition (cluster architecture) is your best choice.

## Directions
1. Use DTS to migrate data from a source TencentDB for Redis instance to a Redis 4.0 or 5.0 Memory Edition instance in standard architecture or cluster architecture. For more information, see [Migration with DTS](https://intl.cloud.tencent.com/document/product/239/31941).
2. After the data sync is completed and the data is verified by your business, you can select the time to disconnect the source Redis instance based on metrics such as business QPS and connect to the destination Redis instance. There are two switching methods:
**Log in to the console for switch:**
 1) Note down the old IP address of the source Redis instance and modify it.
 2) Change the network information of the target Redis instance to the VPC subnet of the source Redis instance, and change the IP address of the target instance to the old IP address of the source instance to complete the switchover on the business side. For more information on how to modify network information and IP addresses, see [Configuring Network](https://intl.cloud.tencent.com/document/product/239/31944).
**Log in to the instance for switch:** update the IP of the source Redis instance in the code to the IP of the target Redis instance.

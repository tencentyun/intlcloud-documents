## Operation Scenarios
TencentDB for Redis [4.0 Standard Edition](https://intl.cloud.tencent.com/document/product/239/31959) and [4.0 Cluster Edition](http://intl.cloud.tencent.com/document/product/239/18336) feature more flexible specification configuration, higher performance, and better functionality. If you are using a lower version of Redis, we recommend that you upgrade to Redis 4.0 for a better TencentDB service experience.

TencentDB for Redis instance version is upgraded through Data Transfer Service (DTS) in a hot migration manner, which guarantees instance service continuity during the upgrade process and can update incremental data in real time.

| Term | Description |
|---------|---------|
| Source instance | Source instance for version upgrade |
| Target instance | Target instance for version upgrade |

#### Supported Versions
<table>
    <tr>
    <td rowspan=2 align=center>Source Instance Version</td>
    <td colspan=2 align=center>Target Instance Version</td>
    </tr>
    <tr>
    <td>4.0 Standard Edition</td>
		<td>4.0 Cluster Edition</td>
    </tr>
    <tr>
    <td>2.8 Standard Edition</td>
    <td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td>4.0 Standard Edition</td>
    <td>-</td>
    <td>✓</td>
    </tr>
</table>

>Data migration among 4.0 Standard Edition instances can be performed through DTS.

## Prerequisites
- The source Redis instance should be running properly.
- You have purchased Redis 4.0 Standard Edition or Redis 4.0 Cluster Edition instances.
>If your existing data is less than 12 GB with incremental data of no more than 60 GB and QPS of no more than 40,000, or you business requires transactional support, Redis 4.0 Standard Edition is recommended; otherwise, Redis 4.0 Cluster Edition is your best choice.

## Directions
1. Use DTS to migrate data from a source TencentDB for Redis instance to a Redis 4.0 Standard Edition or Redis 4.0 Cluster Edition instance. For more information, see [Migration with DTS](http://intl.cloud.tencent.com/document/product/239/31941).
2. After the data sync is completed and the data is verified by your business, you can select the time to disconnect the source Redis instance based on metrics such as business QPS and connect to the destination Redis instance. There are two switching methods:
**Log in to the console for switch:**
 (1) Note down the the old IP address of the source Redis instance and modify it.
 (2) Change the network information of the target Redis instance to the VPC subnet of the source Redis instance, and change the IP address of the target instance to the old IP address of the source instance to complete the switchover on the business side. For more information on how to modify network information and IP addresses, see [Configure Network](http://intl.cloud.tencent.com/document/product/239/31944).
**Log in to the instance for switch:** Update the IP of the source Redis instance in the code to the IP of the target Redis instance.

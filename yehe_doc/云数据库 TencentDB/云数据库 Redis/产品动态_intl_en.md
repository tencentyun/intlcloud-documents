## April 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>DTS supported Redis 5.0</td>
<td>You can migrate data and upgrade instances to Redis 5.0 with Data Transmission Service (DTS).</td>
<td>2020-04</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31941" target="_blank">Migration with DTS</a><li><a href="https://intl.cloud.tencent.com/document/product/239/32546" target="_blank">Version Upgrade with DTS</a></td>
</tr>
</table>

## March 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Supported the service unavailability event alarm</td>
<td>Redis supported the service unavailability event alarm, in addition to supporting event alarms of instance master/slave switch, read-only replica failover, and read-only replica unavailability.</td>
<td>2020-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31947" target="_blank">Configuring Alarms</a></td>
</tr>
<tr>
<td>Supported adjusting bandwidth in the console</td>
<td>You can adjust instance network bandwidth on the instance details page in the Redis console. The bandwidth specifications for the cluster edition have been fully upgraded, with shard specifications upgraded to 384 Mbps.</td>
<td>2020-03</td>
<td>-</td>
</tr>
<tr>
<td>Supported monitoring view switch for Redis 2.8</td>
<td>To provide more accurate monitoring information, Tencent Cloud has updated the monitoring view of Redis 2.8 instance to the cluster view. If you use APIs to get monitoring data from Cloud Monitor, you need to change the view parameter from `redisuuid` to `cluster` in the code.</td>
<td>2020-03</td>
<td>-</td>
</tr>
</table>


## February 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Upgraded the default number of databases in an instance to 256</td>
<td>For Redis 2.8, 4.0, and 5.0 standard and cluster editions you purchased this month, the default number of databases in an instance has been upgraded from 16 to 256.</td>
<td>2020-02</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">Redis Standard Edition</a><li><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">Memory Edition (Cluster Architecture)</a></td>
</tr>
</table>

## January 2020
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Released Redis 5.0</td>
<td>Redis 5.0 standard and cluster editions have been released with all features of Redis 4.0 reserved, and support the latest STREAM data structure, new ZSET commands `ZPOPMIN` and `ZPOPMAX`, scaling without disconnection, 4 TB of storage capacity, and tens of millions of concurrent QPS.</td>
<td>2020-01</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">Redis Standard Edition</a><li><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">Memory Edition (Cluster Architecture)</a></td>
</tr>
</table>

## October 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Supported access management</td>
<td>You can create policies through access management which grant sub-accounts permissions to use the resources they need.</td>
<td>2019-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32845" target="_blank">Access Management</a></td>
</tr>
<tr>
<td>Supported account management in the console</td>
<td>TencentDB for Redis provides read/write permission control and routing policy control through the account mechanism, which helps meet the needs of business permission management in complex scenarios. Currently, only the TencentDB for Redis community edition (excluding Redis 2.8) supports account settings.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/34590" target="_blank">Managing Accounts</a></td>
</tr>
</table>

## September 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Released monitoring 2.0</td>
<td>Redis monitoring 2.0 has been released, adding more than 16 monitoring metrics, including network delay, response error and other monitoring metrics.</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/34589" target="_blank">Monitoring Feature</a></td>
</tr>
</table>

## August 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Supported password-free access</td>
<td>To enable password-free access, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application. After password-free access is enabled, we recommend that you limit access to servers using a security group.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32548" target="_blank">Password-free Access</a></td>
</tr>
<tr>
<td>Supported disabling high-risk commands online</td>
<td>TencentDB for Redis is able to disable some Redis commands that may cause an unstable service or accidentally delete data, including `flushall`, `flushdb`, `keys`, `hgetall`, `eval`, `evalsha`, and `script`.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32550" target="_blank">Disabling Commands</a></td>
</tr>

<tr>
<td>DTS supported cluster edition</td>
<td>You can migrate self-created Redis Cluster (3.0, 3.2, and 4.0) or Codis (2.8 and 3.2) databases to TencentDB for Redis with DTS.</td>
<td>2019-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941" target="_blank">Migration with DTS</a></td>
</tr>
</table>


## July 2019
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Supported version upgrade with DTS</td>
<td>TencentDB for Redis instance version is upgraded through Data Transfer Service (DTS) in a hot migration manner, which guarantees instance service continuity during the upgrade process and can update incremental data in real time.</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/32546" target="_blank">Version Upgrade with DTS</a></td>
</tr>
<tr>
<td>Released Redis 4.0 standard edition</td>
<td>Redis 4.0 standard edition supports 1-master 5-slave mode, read/write separation, scaling without disconnection, and high availability.</td>
<td>2019-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31959" target="_blank">Redis Standard Edition</a></td>
</tr>
</table>


## October 2018
<table>
<tr>
<th width=20%>Update</th>
<th width=50%>Description</th>
<th width=10%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
<tr>
<td>Released Redis 4.0 cluster edition</td>
<td>Redis 4.0 cluster edition has been released and supports 4 TB of storage capacity, tens of millions of concurrent access, scaling without storage capacity loss, and automatic read/write separation.</td>
<td>2018-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/18336" target="_blank">Memory Edition (Cluster Architecture)</a></td>
</tr>
</table>


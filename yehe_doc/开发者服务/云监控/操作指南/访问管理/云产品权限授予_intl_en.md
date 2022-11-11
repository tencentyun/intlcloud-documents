Cloud Monitor (CM) allows a root account to grant a sub-account access permissions via [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583). This document describes how to manage access permissions for a sub-account.

## Overview

By default, a root account is the resource owner and has full access to all resources in the account, while a sub-account has no access to any resources. The root account must grant a sub-account access permissions for the sub-account to access resources. You can use your root account to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) and grant a sub-account access permissions. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

CM policies are subject to the policies of other Tencent Cloud services. When granting CM permissions to a sub-account, you also need to grant the corresponding cloud service permissions so that the Cloud Monitor permissions can take effect.

>?
> - Permissions are used to allow or deny operations to access specific resources under certain conditions.
> - Policies are syntax rules used to define and describe one or more permissions.

## Common Permission Configurations

> ? Below takes CVM permission configuration as an example. For more information on how to grant permissions for other Tencent Cloud services, see the following scenarios and [CM-related Tencent Cloud service policies](#.E4.BA.91.E7.9B.91.E6.8E.A7.E7.9B.B8.E5.85.B3.E7.9A.84.E4.BA.91.E4.BA.A7.E5.93.81.E7.AD.96.E7.95.A5).

### Common permissions

#### Permission list

| Permission Type | Permission Name |
| ------------ | ------------------------------------------------------ |
| CM permission | `QcloudMonitorFullAccess` (full read/write permissions) and `QcloudMonitorReadOnlyAccess` (read-only permissions) |
| CVM permission | `QcloudCVMFullAccess` (full read/write permissions) or `QcloudCVMReadOnlyAccess` (read-only permissions) |

#### Features and permissions

>? You must authorize a role or grant the access permissions of all Tencent Cloud services to a sub-account so that the sub-account can normally access the **Monitor Overview** page, because the access permissions of multiple services are involved here.

<table>
	<tr>
	<th rowspan="2">Feature</th>
    <th colspan="2">Operation Permissions</th>
    <th colspan="2">Access Permissions</th>
	</tr>
	<tr>
	<td>QcloudMonitor<br>FullAccess</td>
	<td>QcloudMonitor<br>ReadOnlyAccess</td>
    <td>QcloudMonitor<br>FullAccess</td>
	<td>QcloudMonitor<br>ReadOnlyAccess</td>
	</tr>
	<tr>
	<td>Dashboard</td>
	<td>&#10003;</td>
	<td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	<tr>
	<td>Instance group</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	    <tr>
	<td>Integration center</td>
	<td>&#10003;</td>
   <td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	    <tr>
	<td>Resource consumption</td>
	<td>&#10003;</td>
   <td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
    <tr>
	<td>Alarm record</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
    <tr>
	<td>Alarm policy</td>
	<td>&#10003;</td>
   <td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	<tr>
	<td>Trigger condition template</td>
	<td>&#10003;</td>
	<td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	    <tr>
	<td>Notification template</td>
	<td>&#10003;</td>
   <td><b>×</b></td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	<tr>
	<td>Traffic monitoring</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
	<tr>
	<td>Tencent Cloud service monitoring</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	<td>&#10003;</td>
	</tr>
</table>

>? **A user with full read/write access permissions for particular Tencent Cloud services also has full read/write access to CM resources by default**. For example, if you have the full read/write access permission (`QcloudCVMFullAccess`) for CVM, you’ll have full read/write access to CM resources by default. You can go to [CAM Console > Policies](https://console.cloud.tencent.com/cam/policy) and click a policy name to check the access to what resources is allowed by this policy.
> <img src="https://qcloudimg.tencent-cloud.cn/raw/60758e89c5a4371b46b11705ef8eff6d.png" width="100%">


### CM-related Tencent Cloud service policies

> ? If you have been properly granted CM permissions, you can access Tencent Cloud service resources with the read-only permission for them. The following table lists permissions for some Tencent Cloud services. For more information, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

<table>
<tr>
	<th>Tencent Cloud Service</th>
	<th>Policy</th>
	<th>Permission Description</th>
	<th>Reference</th>
</tr>
<tr>
<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/213">Cloud Virtual Machine (CVM)</a></td>
	<td>QcloudCVMFullAccess</td>
	<td>Full access permissions for CVM, including monitoring permissions for CVM, CLB and VPC</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213/10312">Sample Console Configuration</a></td>
</tr>
<tr>
	<td>QcloudCVMReadOnlyAccess</td>
	<td>Read-only permissions for CVM resources</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236">TencentDB for MySQL</a></td>
	<td>QcloudCDBFullAccess</td>
	<td>Full access permissions for TencentDB for MySQL, including the access to TencentDB for MySQL, as well as the security group, monitoring, user group, COS, VPC and KMS permissions related to TencentDB for MySQL.</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236/14468">Console Examples</a></td>
</tr>
<tr>
	<td>QcloudCDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for MySQL resources</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/240">TencentDB for MongoDB</a></td>
	<td> QcloudMongoDBFullAccess</td>
	<td>Full access permissions for TencentDB for MongoDB</td>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/240/32838">Access Management</a></td>
</tr>
<tr>
	<td>QcloudMongoDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for MongoDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/239">TencentDB for Redis</a></td>
	<td> QcloudRedisFullAccess </td>
	<td>Full access permissions for TencentDB for Redis</td>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/239/32844">Access Management</a></td>
</tr>
<tr>
	<td>QcloudRedisReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for Redis</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016">TencentDB for TcaplusDB</a> </td>
	<td>QcloudTcaplusDBFullAccess</td>
	<td>Full access permissions for TencentDB for TcaplusDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016/35749">Overview</a></td>
</tr>
<tr>
	<td>QcloudTcaplusDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for TcaplusDB</td>
</tr>
<tr>
	<td>QcloudTBaseReadOnlyAccess</td>
	<td>Read-only permissions for TDSQL for PostgreSQL</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845">Elasticsearch Service</a></td>
	<td>QcloudElasticsearchServiceFullAccess</td>
	<td>Full access permissions for Elasticsearch Service</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845/19550">CAM-Based Access Control Configuration</a></td>
</tr>
<tr>
	<td>QcloudElasticsearchServiceReadOnlyAccess</td>
	<td>Read-only permissions for Elasticsearch Service</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/215">Virtual Private Cloud</a></td>
	<td>QcloudVPCFullAccess</td>
	<td>Full access permissions for VPC</td>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/215/31859">Access Management</a></td>
</tr>
<tr>
	<td>QcloudVPCReadOnlyAccess</td>
	<td>Read-only permissions for VPC</td>
</tr>
<tr>
	<td><a href="https://www.tencentcloud.com/document/product/216">Direct Connect (DC)</a></td>
	<td>QcloudDCFullAccess</td>
	<td>Full access permissions for DC</td>
	<td>-</td>
</tr>
<tr>
	<td><a href="https://www.tencentcloud.com/document/product/406">Cloud Message Queue (CMQ) </a></td>
	<td>QcloudCmqQueueFullAccess</td>
	<td>Full access permissions for CMQ, including permissions for queues and Cloud Monitor</td>
	<td >-</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/597">Message Queue CKafka</a></td>
	<td>QcloudCKafkaFullAccess</td>
	<td>Full access permissions for Message Queue CKafka</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</tr>
<tr>
	<td>QcloudCkafkaReadOnlyAccess</td>
	<td>Read-only permissions for Message Queue Ckafka</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/436">Cloud Object Storage (COS)</a></td>
	<td>QcloudCOSFullAccess</td>
	<td>Full access permissions for COS</td>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/436/12473">Access Control and Permission Management</a></td>
</tr>
<tr>
	<td>QcloudCOSReadOnlyAccess</td>
	<td>Read-only permissions for COS</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/214">Cloud Load Balancer (CLB)</a></td>
	<td>QcloudCLBFullAccess</td>
	<td>Full access permissions for CLB</td>
	<td rowspan="2"><a href="https://www.tencentcloud.com/document/product/214/9776">Cloud Access Management</a></td>
</tr>
<tr>
	<td>QcloudCLBReadOnlyAccess</td>
	<td>Read-only permissions for CLB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582">Cloud File Storage (CFS)</a></td>
	<td>QcloudCFSFullAccesss</td>
	<td>Full access permissions for CFS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582/14679">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCFSReadOnlyAccess</td>
	<td>Read-only permissions for CFS</td>
</tr>
</table>

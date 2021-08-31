Cloud Monitor (CM) allows a root account to grant a sub-account access permissions via [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583). This document describes how to manage access permissions for a sub-account.

## Feature Overview

By default, a root account is the resource owner and has full access to all resources in the account. A sub-account has no access to any resources. The root account must grant a sub-account access permissions for it to access resources. You can use your root account to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) and grant a sub-account access permissions. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

CM policies depend on the policies of other Tencent Cloud services. When you grant CM permissions to a sub-account, the corresponding cloud service permissions must also be granted for CM permissions to take effect.

> ?
> - Permissions: allow or deny operations to access specific resources under certain conditions.
> - Policies: syntax rules used to define and describe one or more permissions.


## Common Permission Configuration

> ? Below takes CVM permission configuration as an example. For more information on how to grant permissions for other Tencent Cloud services, see the following scenarios and [CM-related Tencent Cloud service policies](#.E4.BA.91.E7.9B.91.E6.8E.A7.E7.9B.B8.E5.85.B3.E7.9A.84.E4.BA.91.E4.BA.A7.E5.93.81.E7.AD.96.E7.95.A5).
> Enable the corresponding Tencent Cloud service permissions.

### Common permissions

#### Permission list

| Permission Type | Permission Name |
| ------------ | ------------------------------------------------------ |
| CM permission | QcloudMonitorFullAccess and QcloudMonitorReadOnlyAccess |
| CVM permission | QcloudCVMReadOnlyAccess or QcloudCVMFullAccess |

#### Features and permissions

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
	<td>Monitoring overview</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Dashboard</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Instance grouping</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>Alarm history</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>Alarm policies</td>
	<td>√</td>
        <td><b>×</b></td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Platform event subscription</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Custom messages</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Trigger condition templates</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>Product events</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Platform events</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Traffic monitoring</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Tencent Cloud service monitoring</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
</table>




### CM-related Tencent Cloud service policies

> ? Provided that CM permissions have been properly granted, Tencent Cloud service resources can be accessed after the read-only permission is granted. The following table lists permissions for some Tencent Cloud services. For more information on permissions for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

<table>
<tr>
	<th>Tencent Cloud Service</th>
	<th>Policy</th>
	<th>Permission Description</th>
	<th>Reference</th>
</tr>
<tr>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213">Cloud Virtual Machine (CVM)</a></td>
	<td>QcloudCVMFullAccess</td>
	<td>Full access permissions for CVMs, including monitoring permissions for CVM, CLB and VPC</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213/10312">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCVMReadOnlyAccess</td>
	<td>Read-only permissions for CVM resources</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236">TencentDB for MySQL</a></td>
	<td>QcloudCDBFullAccess</td>
	<td>Full access permissions for TencentDB for MySQL instances, including permissions for MySQL, related security groups, monitoring, user groups, COS, VPC and KMS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236/14468">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for MySQL resources</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240">TencentDB for MongoDB</a></td>
	<td> QcloudMongoDBFullAccess</td>
	<td>Full access permissions for TencentDB for MongoDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240/32839">Access Management</a></td>
</tr>
<tr>
	<td>QcloudMongoDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for MongoDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239">TencentDB for Redis</a></td>
	<td> QcloudRedisFullAccess </td>
	<td>Full access permissions for TencentDB for Redis</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239/32845">Access Management</a></td>
</tr>
<tr>
	<td>QcloudRedisReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for Redis</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016">Tencent Cloud TcaplusDB</a> </td>
	<td>QcloudTcaplusDBFullAccess</td>
	<td>Full access permissions for TencentDB for TcaplusDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016/35749">Access Management</a></td>
</tr>
<tr>
	<td>QcloudTcaplusDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for TcaplusDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845">Elasticsearch Service</a></td>
	<td>QcloudElasticsearchServiceFullAccess</td>
	<td>Full access permissions for Elasticsearch Service</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845/19550">Access Management</a></td>
</tr>
<tr>
	<td>QcloudElasticsearchServiceReadOnlyAccess</td>
	<td>Read-only permissions for Elasticsearch Service</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/215">VPC</a></td>
	<td>QcloudVPCFullAccess</td>
	<td>Full access permissions for VPC</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudVPCReadOnlyAccess</td>
	<td>Read-only permissions for VPC</td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect (DC)</a></td>
	<td>QcloudDCFullAccess</td>
	<td>Full access permissions for DC</td>
	<td>-</td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/406">Cloud Message Queue (CMQ)</a></td>
	<td>QcloudCmqQueueFullAccess</td>
	<td>Full access permissions for CMQ, including permissions for queues and Cloud Monitor</td>
	<td>-</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/597">Message Queue CKafka</a></td>
	<td>QcloudCKafkaFullAccess</td>
	<td>Full access permissions for Message Queue CKafka</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudCkafkaReadOnlyAccess</td>
	<td>Read-only permissions for Message Queue Ckafka</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/436">Cloud Object Storage (COS)</a></td>
	<td>QcloudCOSFullAccess</td>
	<td>Full access permissions for COS</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudCOSReadOnlyAccess</td>
	<td>Read-only permissions for COS</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer (CLB)</a></td>
	<td>QcloudCLBFullAccess</td>
	<td>Full access permissions for CLB</td>
	<td rowspan="2">Access Management</td>
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

Cloud Monitor allows you to control the permissions of sub-accounts by using a root account in [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583). You can refer to this document to learn how to manage sub-account access.

## Feature Overview

By default, a root account is the owner of resources and has access to all resources under it. A sub-account has no access to any resources. The root account needs to grant access permissions for a sub-account so that the sub-account can access relevant resources. You can log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) by using your root account and grant access permissions for a sub-account. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Cloud Monitor policies depend on the policies of other Tencent Cloud services. When you grant Cloud Monitor permissions to a sub-account, you must also grant the permissions of corresponding Tencent Cloud services to the sub-account so that the Cloud Monitor permissions can take effect.

> ?
> - Permissions are used to allow or deny certain operations or access to specific resources under specific conditions.
> - Policies are syntax rules that are used to define and describe one or more permissions.


## Common Permission Configuration

> ? This section takes permission configuration for CVMs as an example. For more information on how to grant permissions for other Tencent Cloud services, see the following scenario description and [Cloud Monitor-Related Tencent Cloud Service Policies](#.E4.BA.91.E7.9B.91.E6.8E.A7.E7.9B.B8.E5.85.B3.E7.9A.84.E4.BA.91.E4.BA.A7.E5.93.81.E7.AD.96.E7.95.A5).
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

> ? Provided that CM permissions have been properly granted, Tencent Cloud service resources can be accessed after the read-only permission is granted. The following table lists the permissions for some Tencent Cloud services. To learn about the permissions for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

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
	<td>Full access permissions for CVMs, including monitoring permissions for CVM, CLB, and VPC instances</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213/10312">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCVMReadOnlyAccess</td>
	<td>Read-only permission for CVM resources</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236">TencentDB for MySQL</a></td>
	<td>QcloudCDBFullAccess</td>
	<td>Full access permissions for TencentDB for MySQL instances, including permissions for MySQL and related security groups, monitoring, user groups, COS instances, VPC instances, and KMS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236/14468">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCDBReadOnlyAccess</td>
	<td>Read-only permission for resources related to TencentDB for MySQL</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240">TencentDB for MongoDB</a></td>
	<td> QcloudMongoDBFullAccess</td>
	<td>Full access permissions for TencentDB for MongoDB instances</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240/38703">Access Management</a></td>
</tr>
<tr>
	<td>QcloudMongoDBReadOnlyAccess</td>
	<td>Read-only permission for TencentDB for MongoDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239">TencentDB for Redis</a></td>
	<td> QcloudRedisFullAccess </td>
	<td>Full access permissions for TencentDB for Redis</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239/38687">Access Management</a></td>
</tr>
<tr>
	<td>QcloudRedisReadOnlyAccess</td>
	<td>Read-only permission for TencentDB for Redis</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016">Tencent Cloud TcaplusDB</a> </td>
	<td>QcloudTcaplusDBFullAccess</td>
	<td>Full access permissions for Tencent Cloud TcaplusDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016/35749">Access Management</a></td>
</tr>
<tr>
	<td>QcloudTcaplusDBReadOnlyAccess</td>
	<td>Read-only permissions for Tencent Cloud TcaplusDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845">Elasticsearch Service</a></td>
	<td>QcloudElasticsearchServiceFullAccess</td>
	<td>Full access permissions for Elasticsearch Service</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845/19550">Access Management</a></td>
</tr>
<tr>
	<td>QcloudElasticsearchServiceReadOnlyAccess</td>
	<td>Read-only permission for Elasticsearch Service</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/215">VPC</a></td>
	<td>QcloudVPCFullAccess</td>
	<td>Full access permissions for VPC</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudVPCReadOnlyAccess</td>
	<td>Read-only permission for VPC</td>
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
	<td>Read-only permission for Message Queue Ckafka</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/436">Cloud Object Storage (COS)</a></td>
	<td>QcloudCOSFullAccess</td>
	<td>Full access permissions for COS</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudCOSReadOnlyAccess</td>
	<td>Read-only permission for COS</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer (CLB)</a></td>
	<td>QcloudCLBFullAccess</td>
	<td>Full access permissions for CLB</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudCLBReadOnlyAccess</td>
	<td>Read-only permission for CLB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582">Cloud File Storage (CFS)</a></td>
	<td>QcloudCFSFullAccesss</td>
	<td>Full access permissions for CFS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582/14679">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCFSReadOnlyAccess</td>
	<td>Read-only permission for CFS</td>
</tr>
</table>

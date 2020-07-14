Cloud Monitor allows you to control the permissions of sub-accounts by using a root account in [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583). You can refer to this document to learn how to manage sub-account access permissions.

## Feature Overview

By default, a root account is the owner of resources and has access to all resources under it. A sub-account does not have access to any resources. The root account needs to grant access permission to a sub-account so that the sub-account can properly access relevant resources. You can log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) by using your root account and grant access permissions to a sub-account. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

>
> - Permissions are used to allow or deny access to specific resources under specific conditions.
> - Policies are the syntax rules used to define and describe one or more permissions.

## Policy Description

Cloud Monitor policies depend on the policies of other Tencent Cloud services. When you grant Cloud Monitor permissions to a sub-account, you must grant the permissions of corresponding Tencent Cloud services to the sub-account so that the Cloud Monitor permissions can take effect.

### Cloud Monitor policies

<table>
	<tr>
		<th width="15%">Policy</th>
		<th width="15%">Description</th>
		<th width="35%">Dependency</th>
		<th width="35%">Difference</th>
	</tr>
	<tr>
		<td>QcloudMonitorFullAccess</td>
		<td>Full read-write permissions for Cloud Monitor, including the permission to view user groups</td>
		<td>This policy depends on the policies of other Tencent Cloud services. For example, if you want to use a sub-account to create an alarm in the Cloud Monitor console, which involves access to CVM instances, the “QcloudCVMFullAccess” permission must be granted to the sub-account</td>
		<td rowspan="2">After the policy of a Tencent Cloud service is granted to a sub-account, the sub-account can properly use all features of Cloud Monitor if it is granted the “QcloudMonitorFullAccess” permission.<br>If the sub-account is granted only the “QcloudMonitorReadOnlyAccess” permission, the sub-account can properly use all features except for creating an alarm policy.</td>
	</tr>
	<tr>
		<td>QcloudMonitorReadOnlyAccess</td>
		<td>Read-only permission for Cloud Monitor</td>
		<td>This policy depends on the policies of other Tencent Cloud services. For example, if you want to use a sub-account to view monitoring charts in the Cloud Monitor console, the “QcloudCVMFullAccess” permission must be granted to the sub-account</td>
	</tr>
</table>

### Tencent Cloud service policies related to Cloud Monitor

> When you have access permissions for Cloud Monitor, you can properly access Tencent Cloud services after being granted the read-only permission to Tencent Cloud services. The following table lists the permissions for certain Tencent Cloud services. For more information, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

<table>
<tr>
	<th>Product</th>
	<th>Policy</th>
	<th>Permission</th>
	<th>Documentation</th>
</tr>
<tr>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213">Cloud Virtual Machine (CVM)</a></td>
	<td>QcloudCVMFullAccess</td>
	<td>Full read-write permissions for CVM, including monitoring permissions for CVM, CLB, and VPC</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213/10312">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCVMReadOnlyAccess</td>
	<td>Read-only permissions for resources related to CVM</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236">TencentDB for MySQL</a></td>
	<td> QcloudCDBFullAccess</td>
	<td>Full read-write permissions for TencentDB for MySQL, including permissions for MySQL and related security groups, monitoring, user groups, COS, VPC, and KMS permissions</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236/14468">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCDBReadOnlyAccess</td>
	<td>Read-only permissions for resources related to TencentDB for MySQL</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240">TencentDB for MongoDB</a></td>
	<td> QcloudMongoDBFullAccess</td>
	<td>Full read-write permissions for TencentDB for MongoDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240/32839">Access Management</a></td>
</tr>
<tr>
	<td>QcloudMongoDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for MongoDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239">TencentDB for Redis</a></td>
	<td> QcloudRedisFullAccess</td>
	<td>Full read-write permissions for TencentDB for Redis</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudRedisReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for Redis</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016">TencentDB for TcaplusDB</a> </td>
	<td>QcloudTcaplusDBFullAccess</td>
	<td>Full read-write permissions for TencentDB for TcaplusDB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016/35749">Access Management</a></td>
</tr>
<tr>
	<td>QcloudTcaplusDBReadOnlyAccess</td>
	<td>Read-only permissions for TencentDB for TcaplusDB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845">Elasticsearch Service</a></td>
	<td>QcloudElasticsearchServiceFullAccess</td>
	<td>Full read-write permissions for Elasticsearch Service</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845/19550">Access Management</a></td>
</tr>
<tr>
	<td>QcloudElasticsearchServiceReadOnlyAccess</td>
	<td>Read-only permissions for Elasticsearch Service</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/215">VPC</a></td>
	<td>QcloudVPCFullAccess</td>
	<td>Full read-write permissions for VPC</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudVPCReadOnlyAccess</td>
	<td>Read-only permissions for VPC</td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect (DC)</a></td>
	<td>QcloudDCFullAccess</td>
	<td>Full read-write permissions for DC</td>
	<td>-</td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/406">Cloud Message Queue (CMQ)</a></td>
	<td>QcloudCmqQueueFullAccess</td>
	<td>Full read-write permissions for CMQ, including permissions for queues and Cloud Monitor</td>
	<td >-</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/597">Message Queue CKafka</a></td>
	<td>QcloudCKafkaFullAccess</td>
	<td>Full read-write permissions for Message Queue CKafka</td>
	<td rowspan="2">Access Management</td>
</tr>
<tr>
	<td>QcloudCkafkaReadOnlyAccess</td>
	<td>Read-only permissions for Message Queue Ckafka</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/436">Cloud Object Storage (COS)</a></td>
	<td> QcloudCOSFullAccess </td>
	<td>Full read-write permissions for COS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/436/12470">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCOSReadOnlyAccess</td>
	<td>Read-only permissions for COS</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer (CLB)</a></td>
	<td>QcloudCLBFullAccess</td>
	<td>Full read-write permissions for CLB</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/214/9777">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCLBReadOnlyAccess</td>
	<td>Read-only permissions for CLB</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582">Cloud File Storage (CFS)</a></td>
	<td>QcloudCFSFullAccess</td>
	<td>Full read-write permissions for CFS</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582/14679">Access Management</a></td>
</tr>
<tr>
	<td>QcloudCFSReadOnlyAccess</td>
	<td>Read-only permissions for CFS</td>
</tr>
</table>
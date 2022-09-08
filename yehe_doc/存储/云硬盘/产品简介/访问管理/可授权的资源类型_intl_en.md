Resource-level permissions refer to the ability to specify which resources users are allowed to perform operations on. CBS supports resource-level permissions. That is, you can specify when users are allowed to perform some CBS operations that support resource-level permissions or which resources users are allowed to use.
The types of resources that can be authorized in Cloud Access Management (CAM) are as follows:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| [CBS APIs](#CBSCorrelation) |  ` qcs::cvm:$region::volume/* `|

[CBS APIs](#CBSCorrelation) describe CBS API operations that currently support resource-level permissions as well as resources and condition keys supported by each operation. **When configuring the resource path,** you need to replace variable parameters such as `$region` and `$account` with your actual parameters. You can also use the `*` wildcard in the path. For more information, see [Console Example](https://intl.cloud.tencent.com/document/product/213/10312).

<dx-alert infotype="notice" title="">
CBS API operations not listed in the table do not support resource-level permissions. You can still authorize users to perform these operations, but the resource element of the policy statement must be specified as `*`.
</dx-alert>

[](id:CBSCorrelation)
### CBS APIs
<table>
<thead>
<tr>
<th align="left">API Operation</th>
<th align="left">Resource Path</th>
<th align="left">Condition Key</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16313" target="_blank">Mount a cloud disk<br>AttachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16312" target="_blank">Create a cloud disk<br>CreateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/32170" target="_blank">Query the list of cloud disk operation logs<br>DescribeDiskOperationLogs</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16315" target="_blank">Query the list of cloud disks<br>DescribeDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16316" target="_blank">Unmount a cloud disk<br>DetachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/15659" target="_blank">Modify the attributes of cloud disks<br>ModifyDiskAttributes</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Modify the billing mode of a cloud disk<br>ModifyDisksChargeType</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Modify the renewal flag of a cloud disk<br>ModifyDisksRenewFlag</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Renew a cloud disk<br>RenewDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16310" target="_blank">Expand the capacity of a cloud disk<br>ResizeDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16321" target="_blank">Return a cloud disk<br>TerminateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
</tbody></table>







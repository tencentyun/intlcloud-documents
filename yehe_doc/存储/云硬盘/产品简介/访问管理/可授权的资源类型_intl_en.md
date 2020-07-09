Resource-level permissions specify which resources a user can manipulate. Cloud Block Storage (CBS) supports resource-level permission on some CBS operations that control which resources and when a user can manipulate.
The following table describes the types of resources that can be authorized in Cloud Access Management (CAM):

| Resource Type | Resource Description Method in the Authorization Policy |
| :-------- | -------------- |
| [CBS APIs](#CBSCorrelation) |  ` qcs::cvm:$region::volume/* `|

The [CBS APIs](#CBSCorrelation) describe the CBS API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. **When setting the resource path,** you need to replace the variable parameters such as `$region` and `$account` with your actual parameters. You can also use the `*` wildcard in the path. For related operation examples, see [Console Example](https://intl.cloud.tencent.com/document/product/213/10312).
>! CBS API operations not listed in the table do not support resource-level permission. You can still authorize a user to perform these operations, but you must specify `*` as the resource element in the policy statement.
>

<span id="CBSCorrelation"></span>
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
<td align="left">Change the billing mode of an elastic cloud disk<br>ModifyDisksChargeType</a></td>
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







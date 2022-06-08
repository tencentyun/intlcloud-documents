ENI supports resource-level permission control, which means you can specify when a user is allowed for an operation, and what resource can a user get access to.

Cloud Access Management (CAM) allows you to grant access permissions to the following resources.

| Resource Type | Resource Description Method in Authorization Policies |
| :-------- | -------------- |
| [ENI APIs](#eniCorrelation) | `qcs::vpc:$region:$account:eni/$networkInterfaceId` |

[ENI APIs](#eniCorrelation) describes ENI API operations that currently support resource-level permissions as well as resources and condition keys supported by each operation. **When configuring the resource path,** you need to replace variable parameters such as `$region` and `$account` with your actual parameters. You can also use the `*` wildcard in the path. For more information, see [CAM Examples](https://intl.cloud.tencent.com/document/product/576/44375).


<dx-alert infotype="notice" title="">
ENI API operations not listed in the table do not support resource-level permissions. You can still authorize users to perform these operations, but the resource element of the policy statement must be specified as `*`.
</dx-alert>



[](id:eniCorrelation)
### ENI APIs
<table>
<thead>
<tr>
<th align="left">API Operation</th>
<th align="left">Resource Path</th>
<th align="left">Condition Key</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15813" target="_blank">Requesting a private IP for an ENI<br>AssignPrivateIpAddresses</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15819" target="_blank">Binding an ENI to a CVM<br>AttachNetworkInterface</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td rowspan="3"align="left"><a href="https://intl.cloud.tencent.com/document/product/215/37318" target="_blank">Creating an ENI and binding it to a CVM<br>CreateAndAttachNetworkInterface</a></td>
<td align="left"><br>VPC resource<br><code>qcs::vpc:$region:$account:vpc/*</code><br><code>qcs::vpc:$region:$account:vpc/$vpcId</code></td>
<td align="left">vpc:region</td>
</tr>
<tr>
<td align="left"><br>CVM resource<br><code>qcs::cvm:$region:$account:instance/*</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code></td>
<td align="left">cvm:region</td>
</tr>
<tr>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td rowspan="3"align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15818" target="_blank">Creating an ENI<br>CreateNetworkInterface</a></td>
<td align="left"><br>VPC resource<br><code>qcs::vpc:$region:$account:vpc/*</code><br><code>qcs::vpc:$region:$account:vpc/$vpcId</code></td>
<td align="left">vpc:region</td>
</tr>
<tr>
<td align="left"><br>Subnet resource<br><code>qcs::vpc:$region:$account:subnet/*</code><br><code>qcs::vpc:$region:$account:subnet/$subnetId</code></td>
<td align="left">vpc:vpc<br>vpc:region</td>
</tr>
<tr>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15822" target="_blank">Deleting an ENI<br>DeleteNetworkInterface</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td rowspan="2"align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15816" target="_blank">Unbinding an ENI from a CVM<br>DetachNetworkInterface</a></td>
<td align="left"><br>CVM resource<br><code>qcs::cvm:$region:$account:instance/*</code><br><code>qcs::cvm:$region:$account:instance/$instanceId</code></td>
<td align="left">cvm:region</td>
</tr>
<tr>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td rowspan="2"align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15821" target="_blank">Migrating an ENI<br>MigrateNetworkInterface</a></td>
<td align="left"><br>CVM Resource<br><code>qcs::cvm:$region:$account:instance/*</code><br><code>qcs::cvm:$region:$account:instance/$instanceId(permission is required before and after the migration)</code></td>
<td align="left">cvm:region</td>
</tr>
<tr>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15820" target="_blank">Migrating a private IP of an ENI<br>MigratePrivateIpAddress</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15815" target="_blank">Modifying an ENI<br>ModifyNetworkInterfaceAttribute</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15823" target="_blank">Modifying the private IP Information of an ENI<br>ModifyPrivateIpAddressesAttribute</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/215/15814" target="_blank">Returning a private IP of an ENI<br>UnassignPrivateIpAddresses</a></td>
<td align="left"><br>ENI resource<br><code>qcs::vpc:$region:$account:eni/*</code><br><code>qcs::vpc:$region:$account:eni/$networkInterfaceId</code></td>
<td align="left">vpc:vpc<br>vpc:subnet<br>vpc:region</td>
</tr>
</tbody></table>

With Cloud Access Management (CAM), you can grant resource-level permissions for users.
In CAM, the types of Lighthouse resources that can be authorized are as follows:
<table>
<thead>
<tr>
<th align="left">Resource Type</th>
<th>Resource Description Method in Authorization Policy</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Instance</td>
<td><code>qcs::lighthouse:$region:$account:instance/*</code></td>
</tr>
<tr>
<td align="left">Image</td>
<td><code>qcs::lighthouse:$region:$account:blueprint/*</code></td>
</tr>
<tr>
<td align="left">Snapshot</td>
<td><code>qcs::lighthouse:$region:$account:snapshot/*</code></td>
</tr>
<tr>
<td align="left">Key</td>
<td><code>qcs::lighthouse:$region:$account:keypair/*</code></td>
</tr>
</tbody></table>

The table below lists the API operations of Lighthouse that currently support resource-level permissions, as well as their resources and condition keys. When setting the resource path, you need to replace the variable parameters such as `$region` and `$account` with your actual parameter values. You can also use the `*` wildcard in the path.
For relevant concepts such as `region`, `action`, `account`, and `resource` in CAM policies, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
>!Lighthouse API operations not listed here do not support resource-level permissions. You can still authorize a user to perform such an API operation, but you must specify `*` as the resource element of the policy statement.
>

### Instance
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">ModifyInstancesBundle</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">RenewInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">IsolateInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ModifyInstancesAttribute</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ModifyInstancesRenewFlag</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">RebootInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ResetInstance</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ResetInstancesPassword</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">StartInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">StopInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">TerminateInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeInstancesDeniedActions</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeInstancesReturnable</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeInstancesTrafficPackages</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceVncUrl</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeResetInstanceBlueprints</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>

### Snapshot
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">CreateInstanceSnapshot</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code><br>
<code>qcs::lighthouse:$region:$account:snapshot/*</code></td>
</tr>
<tr>
<td align="left">DeleteSnapshots</td>
<td align="left"><code>qcs::lighthouse:$region:$account:snapshot/$snapshotId</code></td>
</tr>
<tr>
<td align="left">ApplyInstanceSnapshot</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code><br>
<code>qcs::lighthouse:$region:$account:snapshot/$snapshotId</code></td>
</tr>
<tr>
<td align="left">DescribeSnapshotsDeniedActions</td>
<td align="left"><code>qcs::lighthouse:$region:$account:snapshot/$snapshotId</code></td>
</tr>
<tr>
<td align="left">ModifySnapshotAttribute</td>
<td align="left"><code>qcs::lighthouse:$region:$account:snapshot/$snapshotId</code></td>
</tr>
</tbody></table>

### Firewall
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">CreateFirewallRules</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DeleteFirewallRules</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DescribeFirewallRules</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ModifyFirewallRules</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ModifyFirewallRuleDescription</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>


### Key
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">DeleteKeyPairs</td>
<td align="left"><code>qcs::lighthouse:$region:$account:keypair/$keypairId</code></td>
</tr>
<tr>
<td align="left">AssociateInstancesKeyPairs</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code><br>
<code>qcs::lighthouse:$region:$account:keypair/$keypairId</code></td>
</tr>
<tr>
<td align="left">DescribeInstanceLoginKeyPairAttribute</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">DisassociateInstancesKeyPairs</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code><br>
<code>qcs::lighthouse:$region:$account:keypair/$keypairId</code></td>
</tr>
<tr>
<td align="left">ModifyInstancesLoginKeyPairAttribute</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>

### Image
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">CreateBlueprint</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code><br>
<code>qcs::lighthouse:$region:$account:blueprint/*</code></td>
</tr>
<tr>
<td align="left">DeleteBlueprints</td>
<td align="left"><code>qcs::lighthouse:$region:$account:blueprint/$blueprintId</code></td>
</tr>
<tr>
<td align="left">DescribeBlueprintInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
<tr>
<td align="left">ModifyBlueprintAttribute</td>
<td align="left"><code>qcs::lighthouse:$region:$account:blueprint/$blueprintId</code></td>
</tr>
</tbody></table>

### Bundle
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody><tr>
<td align="left">DescribeModifyInstanceBundles</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>

### Billing
<table>
<thead>
<tr>
<th align="left" width="40%">API</th>
<th align="left">Resource</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">InquirePriceRenewInstances</td>
<td align="left"><code>qcs::lighthouse:$region:$account:instance/$instanceId</code></td>
</tr>
</tbody></table>


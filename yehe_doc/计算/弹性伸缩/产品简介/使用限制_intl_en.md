Auto Scaling is now available in all regions except edge server regions. The following table details the use limits of this feature:
<table>
<tr>
<th>Limit Type</th>
<th>Description</th>
</tr>
<tr>
<td>One user in one region</td>
<td>
<ul class="params">
<li>Up to 20 launch configurations can be created.</li>
<li>Up to 20 scaling groups can be created.</li>
<li>The maximum number of CVM instances that can be created depends on your CVM quota. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/2664">Purchase Limits for Pay-as-You-Go CVM Instances</a>.</li>
</ul>
</td>
</tr>
<tr>
<td>A scaling group</td>
<td>
<ul class="params">
<li>Only one launch configuration can be created.</li>
<li>Up to 2,000 CVM instances can be scaled.</li>
<li>Up to 100 scaling policies and up to 10 scheduled tasks can be created.</li>
<li>Up to 5 notifications can be created.</li>
<li>Up to 10 lifecycle hooks can be created.</li>
</ul>
</td>
</tr>
<tr>
<td>Others</td>
<td>
<ul class="params">
<li>The number of CVMs in all scaling groups cannot exceed the maximum number of IP addresses that the VPC subnet can provide.</li>
<li>Currently, Auto Scaling does not support scaling up, which means it cannot automatically scale the CPU, memory, and bandwidth of CVM instances.</li>
<li>Auto Scaling and launch configurations are region-specific services. Therefore, you can only launch or terminate CVM instances in the same region.</li>
<li>A scaling group and its associated CLB instances (in the case of a cross-region CLB instance, its backend VPC) must be in the same network environment (the same VPC instance or the basic network in the same region).</li>
</ul>
</td>
</tr>
</table>

<style>
	.params{margin-bottom:0px !important;}
</style>

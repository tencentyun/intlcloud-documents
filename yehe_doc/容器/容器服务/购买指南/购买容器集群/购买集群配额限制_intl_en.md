
Each user is assigned a fixed quota for TKE clusters in each region.

### TKE quota limits

The following describes the number of container clusters each user can purchase. If you need more clusters, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS).
> Since October 21, 2019, the maximum number of nodes supported in a cluster has been increased to 5,000.
>


<table>
	<tr>
	<th>Quota Item</th>
	<th>Default Value</th>
	<th>Where to Check</th>
	<th>Support Quota Increase</th>
	</tr>
	<tr>
	<td>Clusters in a single region</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2">Bottom-right section of the TKE overview page</a></td>
	<td rowspan=5>Yes</td>
	</tr>
	<tr>
	<td>Nodes in a single cluster</td>
	<td>5,000</td>
	</tr>
	<tr>
	<td>Image namespaces in a single region</td>
	<td>10</td>
	</tr>
	<tr>
	<td>Images in a single region</td>
	<td>500</td>
	</tr>
	<tr>
	<td>Image tags for a single image</td>
	<td>100</td>
	</tr>
</table>



### CVM quota limits

For CVM instances that you purchase for Tencent Cloud TKE, CVM purchase limits apply. For more information, see [CVM Instance Purchase Limits](https://intl.cloud.tencent.com/document/product/213/2664). See the following table for the maximum number of CVMs that a user can purchase by default. If you need a higher quota for any item, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&level3_id=156&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%B4%AD%E4%B9%B0%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=1&scene_code=12701&step=2).

<table >
<thead>
<tr>
<th width="20%">Quota Item</th>
<th width="20%">Default Value</th>
<th width="20%">Support Quota Increase</th>
</tr>
</thead>
<tbody><tr>
<td>Pay-as-you-go CVMs in a single availability zone
</td>
<td >30 or 60
</td> 
<td>Yes</tr>
</thead>
</tbody></table>





### Cluster configuration limits
>Cluster configuration limits the size of clusters and cannot be modified currently.
>

| Configuration Item | IP Address Range | Affected Item | Where to Check | Support Modification |
| ----- | ----- | ---- | --------- | ---------- |
| VPC network - Subnet | Custom | Number of nodes that can be added |[VPC subnet list page for the cluster - Available IP addresses](https://console.cloud.tencent.com/vpc/subnet) | <ul class="params"><li>No</li><li>Yes, and you can create new subnets</li></ul> |
| CIDR block of the container IP range | Custom | <ul class="params"><li>Maximum nodes per cluster</li><li>Maximum services per cluster</li><li>Maximum pods per node</li></ul> | Basic information page for the cluster - Container IP address range | No |

<style>
	.params{margin-bottom:0px !important;}
</style>


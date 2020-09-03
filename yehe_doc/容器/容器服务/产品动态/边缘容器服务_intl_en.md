## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The application market, Helm Chart, and assembly line support TKE Edge.</td><td>TKE Edge supports the creation of apps, use of the application market to create apps, and assembly line operations.</td><td>2020-07-06</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30682">Application Overview</a></li></ul></td>
</tr>
<tr>
    <td>Users can customize the node initialization script.</td><td><ul class="params"><li>Node initialization operations include mounting a data disk and creating directories.</li><li>The script is run only once during node initialization.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
<tr>
    <td>Users can obtain metrics on cluster pods via the apiserver.</td><td><ul class="params"><li>For pods in a cluster, users can obtain the metrics of all pods (assuming that such metrics exist) by requesting tem from the api-server.</li><li>In such use cases, a monitoring component should be deployed in the cluster.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
</table>

## June 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE Edge supports GPU.</td><td>Currently, TKE Edge supports the NVIDIA Tesla (T4, P40, M40, P4, and V100) GPU models.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>The TKE Edge image acceleration feature is launched for beta testing.</td><td>The launch time of big-image pods is shortened to 70% of the original launch time, and the public traffic consumption for pulling images is reduced to 1/n (n: the number of nodes in the same LAN) of the original traffic consumption.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports custom parameters.</td><td><ul class="params"><li>Supports custom node initialization scripts.</li><li>Supports custom container directories.</li><li>Supports custom node max-pod.</li></ul></td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>TKE Edge supports Kubernetes v1.18.2.</td><td>Supports the creation of Kubernetes v1.18.2 clusters.</td><td>2020-06-01</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating Edge Clusters</a></td>
</tr>
</table>

## March 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>TKE Edge is launched.</td><td>TKE Edge is a container system that manages edge cloud resources from the central cloud. You can use it to manage distributed nodes in the same cluster across multiple regions. TKE Edge is fully compatible with native Kubernetes, supports one-click app delivery, and provides edge autonomy and distributed health checks.</td><td>2020-03-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35390">Tencent Kubernetes Engine for Edge</a></td>
</tr>
</table>


<style>
	.params{margin:0px !important}
</style>

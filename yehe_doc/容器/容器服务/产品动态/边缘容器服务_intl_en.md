## October 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>ECK supports multi-architecture hybrid management.</td><td>Users can manage the nodes in both ARM and X86 CPU architectures within a cluster at the same time.</td><td>2020-10-28</td><td>-</td>
</tr>
<tr>
    <td>ECK supports edge Pod HPA.</td><td>The feature of edge Pod HPA is launched, and the native Kubernetes HPA feature can also take effect at the edge.</td><td>2020-10-23</td><td>-</td>
</tr>
<tr>
    <td>The feature of using script to add node is upgraded.</td><td>Users can use the same script to add self-owned nodes to the cluster multiple times (the script validity is 1 hour), which is convenient for adding self-owned nodes in batches.</td><td>2020-10-22</td><td>-</a></td>
</tr>
</table>


## September 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Users can enable edge health feature on the console.</td><td>The "Enable Edge Health" switch is added to the basic information page of the edge cluster. Users can enable or disable this feature based on actual usage.</td><td>2020-09-28</td><td>-</a></td>
</tr>
<tr>
    <td>ECK supports ECM security groups.</td><td>When purchasing ECM resources on the ECK console, users can select the node security group for security management.</td><td>2020-09-24</td><td>-</td>
</tr>
<tr>
    <td>The permission convergence of edge node is launched.</td><td>This feature is automatically enabled without user operation, and can effectively prevent malicious users from disrupting the normal operation of the system through edge nodes.</td><td>2020-09-15</td><td>-</td>
</tr>
</table>

## August 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>Edge cluster is available in Beijing region.</td><td>User can create edge clusters in Beijing region.</td><td>2020-08-28</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a></td>
</tr><tr>
    <td>The node installation script is optimized.</td><td>The node installation script can automatically obtain the default ENI.</td><td>2020-08-12</td><td>-</td>
</tr>
<tr>
    <td>The Pod access mode is added.</td><td>Pod can access Apiserver in incluster mode.</td><td>2020-08-05</td><td>-</td>
</tr>
</table>

## July 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>The application market, Helm Chart, and assembly line support ECK.</td><td>ECK supports creation of apps, use of the application market to create apps, and assembly line operations.</td><td>2020-07-06</td><td><ul class="params"><li><a href="https://intl.cloud.tencent.com/document/product/457/37706">Application Market</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30682">Application Overview</a></li></ul></td>
</tr>
<tr>
    <td>Users can customize the node initialization script.</td><td><ul class="params"><li>Node initialization operations include mounting a data disk, creating directories, and so on.</li><li>The script is run only once during node initialization.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
<tr>
    <td>Users can obtain the metrics of cluster pods via the apiserver.</td><td><ul class="params"><li>For users’ pods in a cluster, users can obtain the metrics of all pods (assuming that such metrics exist) by requesting the api-server.</li><li>In such use cases, a monitoring component should be deployed in the cluster.</li></ul></td><td>2020-07-01</td><td>-</td>
</tr>
</table>

## June 2020
<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>ECK supports GPU.</td><td>Currently, ECK supports the NVIDIA Tesla (T4, P40, M40, P4, and V100) GPU models.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>The ECK image acceleration feature is launched for beta testing.</td><td>The launch time of big-image pods is shortened to 70% of the original launch time, and the public traffic consumption for pulling images is reduced to 1/n (n: the number of nodes in the same LAN) of the original traffic consumption.</td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>ECK supports custom parameters.</td><td><ul class="params"><li>Supports custom node initialization scripts.</li><li>Supports custom container directories.</li><li>Supports custom node max-pod.</li></ul></td><td>2020-06-30</td><td>-</td>
</tr>
<tr>
    <td>ECK supports Kubernetes v1.18.2.</td><td>Supports the creation of Kubernetes v1.18.2 clusters.</td><td>2020-06-01</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating Edge Clusters</a></td>
</tr>
</table>

## March 2020

<table>
<tr><th style="width:20%">Update</th><th style="width:50%">Description</th> 
<th style="width:15%">Date</th><th style="width:15%">Related Documents</th> </tr>
<tr>
    <td>ECK is launched.</td><td>ECK is a container system that manages edge cloud resources from the central cloud. You can use it to manage distributed nodes in the same cluster across multiple regions. ECK is fully compatible with native Kubernetes, supports one-click app delivery, and provides edge autonomy and distributed health checks.</td><td>2020-03-25</td><td><a href="https://intl.cloud.tencent.com/document/product/457/35390">Edge Cloud Kubernetes Engine</a></td>
</tr>
</table>


<style>
	.params{margin:0px !important}
</style>

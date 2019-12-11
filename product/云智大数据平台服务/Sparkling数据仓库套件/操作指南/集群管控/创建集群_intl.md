[//]: # (chinagitpath:XXXXX)

This section describes how to create a data warehouse cluster. Currently, the beta version only supports cluster creation in Guangzhou, Shanghai and Beijing.

## Steps

1. Go to [Cluster Management](https://console.qcloud.com/sparkling) and click **Clusters** in the left pane to enter the cluster management page.
2. Select the region in which to create the cluster in the upper left corner of the page. Currently, we support  **Guangzhou**, **Shanghai** and **Beijing**.
3. Click **Create a cluster** in the upper right corner of the page to enter the cluster creation page.
4. Enter the cluster configuration parameters.
   ![](https://main.qcloudimg.com/raw/8b9be82b96c78045d07542b61f73583c.png)

<table border="1">
<tr>
<th>Name</th>
<th>Meaning</th>
<th>Note</th>
</tr>
<tr>
<td>Storage cluster name</td>
<td>Name of the cluster</td>
<td>-</td>
</tr>
<tr>
<td>Region</td>
<td>Actual working region of the cluster	</td>
<td>The beta version only supports Guangzhou, Shanghai and Beijing regions.
</td>
</tr>
<tr>
<td>Availability zone	</td>
<td>Select an availability zone in the region	</td>
<td>You can check whether there are available models in the availability zone in [Master node].  
<ul style="margin-bottom: 0px;">
<li>Available: "Select a model" is displayed. </li>
<li>Unavailable: "No models available in this availability zone" is displayed. </li>
</td>
</tr>
<tr>
<td>Select a network	</td>
<td>Specify a VPC connected to Sparkling	</td>
<td>You can create a VPC in the console for query and planning. <b>Once selected, the VPC and subnet cannot be changed. Subsequently added compute clusters can only be deployed within the same VPC and subnet. <b>
</td>
</tr>
<tr>
<td>Select a subnet group	</td>
<td>Specify a subnet connected to Sparkling	</td>
<td>You can create a subnet in the console for query and planning.
</td>
</tr>
<tr>
<td>Running version</td>	
<td>Sparkling's internal component version</td>	
<td>The beta version only supports 0.1.0 (Spark 2.3.2, Hadoop 2.7.3, Hive 2.1.0).
</td>
</tr>
<tr>
<td>Master node</td>
<td>D1</td>
<td>The beta version supports selecting a Big Data D1 model with four types of configuration. Please select the memory and CPU core quantity of the master node as needed. </td>
</tr>
</table>

5. Select the cluster node type and quantity.
 ![](https://main.qcloudimg.com/raw/2ee505672eaac11805c75efc95a1d598.png)

| Name | Meaning | Note |
| ------------ | ------------------ | ------------------------------------------------------------ |
| Core compute node | Responsible for the cluster's storage tasks | The beta version supports selecting a Big Data D1 model with four types of configuration. You can select the memory and CPU core quantity of the node as needed. |
| Elastic compute node | Responsible for the cluster's computation tasks | The beta version supports selecting a MEM Optimized model with multiple types of configuration. You can select the memory and CPU core quantity of the node as needed. |
| Minimum node quantity | Minimum number of nodes required | - |
| Maximum node quantity | Maximum number of nodes required | - |

6. Click **OK** to create the cluster.
   It takes time to create a cluster. The initial status is **Creating**. Please wait a while. The status will be updated to **Normal** after successful creation.
7. Click **Clusters** in the left panel to enter the cluster management page. In the upper left corner, select **Guangzhou**, **Shanghai** or **Beijing** to view the list of clusters in the selected region.


## Operation Scenario
A Sparkling cluster is the core Sparkling Data Warehouse Suite component. The size of the Sparkling cluster determines the upper limit of the storage capacity and computing power that Sparkling can provide. You can customize the cluster based on your business needs.
This documents describes how to quickly create a Sparkling cluster in the Sparkling console.

## Prerequisites
1. You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and [verified your identity](https://intl.cloud.tencent.com/document/product/378/3629).
2. You have filled out the application form on the [Sparkling Data Warehouse Suite](https://intl.cloud.tencent.com/login) page and clicked **Submit Application** to complete the online application.

> After receiving your application, we will review your service requirements. Our Sparkling team will contact you to confirm your preliminary needs and discuss your usage scenarios as well as other business issues. After the review is completed, we will approve your beta qualification.

## Creating a Cluster
1. Go to [Cluster Management](https://intl.cloud.tencent.com/login) and click **Clusters** in the left pane to enter the cluster management page.
2. Select the region in which to create the cluster in the upper left corner of the page. Currently, **Guangzhou**, **Shanghai**, and **Beijing** are supported.
3. Click **Create a Cluster** in the upper right corner of the page to enter the cluster creation page.
4. Enter the cluster configuration parameters.
   ![](https://main.qcloudimg.com/raw/d0dacfc2104c11134fa809031969dcec.png)

<table border="1">
<tr>
<th>Name</th>
<th>Meaning</th>
<th>Note</th>
</tr>
<tr>
<td>Storage Cluster Name</td>
<td>Name of the cluster</td>
<td>-</td>
</tr>
<tr>
<td>Region</td>
<td>Actual working region of the cluster	</td>
<td>The current version only supports the Guangzhou, Shanghai, and Beijing regions. <br>The current region defaults to the region selected on the cluster management page. If you need to change it, please select a new region in the upper left corner of the cluster management page.
</td>
</tr>
<tr>
<td>Availability Zone	</td>
<td>Select an availability zone in the region	</td>
<td>You can check whether there are available models in the availability zone in **Master Node**.  
<ul style="margin-bottom: 0px;">
<li>Available: "Select a model" is displayed. </li>
<li>Unavailable: "This availability zone has no available models." is displayed. </li>
</td>
</tr>
<tr>
<td>Network	</td>
<td>Specify a VPC to connect to Sparkling	</td>
<td>You can create a VPC in the console for query and planning. <b>Once selected, the VPC and subnet cannot be changed. Subsequently added compute clusters can only be deployed in the same VPC and subnet. <b>
</td>
</tr>
<tr>
<td>Subnet Group	</td>
<td>Specify a subnet connected to Sparkling	</td>
<td>You can create a subnet in the console for query and planning.
</td>
</tr>
<tr>
<td>Running Version</td>	
<td>Sparkling's internal component version</td>	
<td>The current version only supports 0.1.0 (Spark 2.3.2, Hadoop 2.7.3, Hive 2.1.0).
</td>
</tr>
<tr>
<td>Master Node</td>
<td>D1</td>
<td>The current version supports selecting a Big Data D1 model with four types of configuration. Please select the memory and CPU core quantity of the master node as needed. </td>
</tr>
</table>

5. Select the cluster node type and quantity.
 ![](https://main.qcloudimg.com/raw/21edf2ec770c9ca45d971399efa7498b.png)

| Name | Meaning | Note |
| ------------ | ------------------ | ------------------------------------------------------------ |
| Core Compute Node | Responsible for the cluster's storage tasks | The current version supports selecting a Big Data D1 model with four types of configuration. You can select the memory and CPU core quantity of the node as needed. |
| Elastic Compute Node | Responsible for the cluster's computation tasks | The current version supports selecting a MEM Optimized model with various types of configuration. You can select the memory and CPU core quantity of the node as needed. |
| Min Node Quantity | Minimum number of nodes required | - |
| Max Node Quantity | Maximum number of nodes required | - |

6. Click **OK** to create the cluster.
   It takes time to create a cluster. The initial status is **Creating**. Please wait a while. The status will be updated to **Normal** after successful creation.
7. Click **Clusters** in the left pane to enter the cluster management page. In the upper left corner, select **Guangzhou**, **Shanghai** or **Beijing** to view the list of clusters in the selected region.




 












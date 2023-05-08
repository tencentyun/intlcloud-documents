## Billing Mode
EMR offers one billing mode for clusters: pay-as-you-go. The cost of a cluster is the sum of the costs of all nodes in the cluster and of associated cloud products. Elastic nodes (task nodes) can be billed on a spot instance basis.
A pay-as-you-go cluster can have pay-as-you-go and spot instance nodes.
The following table lists the differences between these two billing modes:

<table>
<thead>
<tr>
<th>Billing Mode</th>
<th>Pay-As-You-Go</th>
<th>Spot Instance</th>
</tr>
</thead>
<tbody><tr>
<td>Payment method</td>
<td>Postpaid; <a href="https://intl.cloud.tencent.com/document/product/555/12039">amount freezing</a> upon purchase, billed hourly</td>
<td>Postpaid; <a href="https://intl.cloud.tencent.com/document/product/555/12039">amount freezing</a> upon purchase, billed hourly</td>
</tr>
<tr>
<td>Billing unit</td>
<td>USD/second</td>
<td>USD/second</td>
</tr>
<tr>
<td>Unit price</td>
<td>Relatively higher</td>
<td>The price fluctuates. In most cases, the price is about 10-20% of the price of a pay-as-you-go instance with the same specifications.</td>
</tr>
<tr>
<td>Minimum use time</td>
<td>Charged by second and billed by hour. Purchase and release at any time.</td>
<td>Charged by second and billed by hour. Purchase and release at any time. May be repossessed by the system.</td>
</tr>
<tr>
<td>Configuration change</td>
<td>No limit. Change (node CPU and memory only) at any time.</td>
<td>Not supported</td>
</tr>
<tr>
<td>Use case</td>
<td>Suitable for a cluster to exist for a short period or periodically.</td>
<td>Suitable for a cluster using elastic compute resources to get more computing power.</td>
</tr>
<tr>
<td>Billing mode change</td>
<td>Not supported</a></td>
<td>Not supported</td>
</tr>
</tbody></table>
**The pay-as-you-go mode offers 3-tiered pricing, except for model S5 and new models launched after November 2019. A longer usage period means a bigger discount.**

- Tier 1: 0 &lt;T1 ≤ 96
- Tier 2: 96 &lt;T2 ≤ 360
- Tier 3: T3 > 360
For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/213/2176).

You can view node specifications and pricing and estimate your resource costs on the [Pricing | Elastic MapReduce](https://www.tencentcloud.com/pricing/emr) page.
EMR bills only show the costs of nodes, namely, the costs of CPU, memory, system disk, and local data disk. The bills of associated cloud products are available in their respective consoles. For EMR bill details, see [Viewing Bills](https://intl.cloud.tencent.com/document/product/1026/48586) or [Cost Allocation by Tag](https://intl.cloud.tencent.com/document/product/1026/48586).
>! 
>- **Select the shutdown mode with caution when shutting down a pay-as-you-go EMR cluster node in the CVM console, because EMR nodes do not support the "no charges when shut down" mode.**
>- **The prices of a model given on the Pricing | Elastic MapReduce page cover only the configuration of its CPU, memory, and local data disk**, excluding the costs of images, cloud system disks, cloud data disks, and associated cloud products.
>- For the pricing of different types of disks, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413). For charges of associated cloud products, see "Billable Items > Charges of associated cloud products" below.
>- The prices are subject to changes as appropriate. Please visit our official website for the latest prices.

## Billable Items
The cost of a cluster is the sum of the costs of all nodes in the cluster and of associated cloud products. Cloud products such as Elastic IP, CDB, CBS, CHDFS, COS, and Virtual Private Cloud (VPC) may be used when you use EMR. You will be charged for such products in their respective billing mode. For details, see their respective billing document.
<table>
<thead>
<tr>
<th>Cost Category</th>
<th>Billable Item</th>
<th>Resource Use in EMR</th>
<th>Billing Description</th>
<th>Pricing</th>
</tr>
</thead>
<tbody><tr>
<td>Costs of EMR nodes</td>
<td>Node cost</td>
<td>You can select the model specifications as needed. The nodes are subject to separate pricing by EMR. The price of a node covers its resources such as CPU, memory, system disk, and local data disk. Two billing modes are available: pay-as-you-go and spot instance.</td>
<td>The EMR cost is only the costs of all nodes.</td>
<td><a href="https://buy.cloud.tencent.com/price/emr"><strong>Pricing of Elastic MapReduce</strong></a></td>
</tr>
<tr>
<td rowspan=5>Costs of associated cloud products</td>
<td>Elastic IP (EIP)</td>
<td>Public network access is enabled for the Master.1 node in a cluster by default so that you can access the WebUI pages of various Hadoop components from outside the cluster. Traffic fees are incurred for data interactions when you visit these pages, but a little traffic is generated in most cases. Therefore, the bill-by-traffic mode is used by default, which costs less than the bill-by-bandwidth mode.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/17156">Elastic IP Billing</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/17156">Elastic IP Billing</a></td>
</tr>
<tr>
<td>TencentDB for MySQL (CDB)</td>
<td>If you plan to deploy one or more components among Hive (local), Hue, Ranger, Oozie, Druid, and Superset in an EMR cluster, you need to purchase a CDB instance for storing metadata.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/18335">TencentDB for MySQL Billing Overview</a></td>
<td><a href="https://buy.cloud.tencent.com/price/cdb/overview?regionId=1&amp;zoneId=100006&amp;engineVersion=8.0&amp;cdbType=Z3&amp;memory=8000&amp;cpu=4&amp;volume=200&amp;goodsNum=1">TencentDB for MySQL Pricing</a></td>
</tr>
<tr>
<td>Cloud Block Storage (CBS)</td>
<td>If you plan to deploy cloud disks as the data disks in a node, you need to purchase at least one cloud disk. The cost of the cloud disk will be paid together with the EMR node purchased, with the corresponding CBS order generated. The cloud disk will be subject to the same billing mode as the node.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/32415">CBS Billing Overview</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/2413">CBS Price Overview</a></td>
</tr>
<tr>
<td>Cloud Object Storage (COS)</td>
<td>If you use COS to separate the compute and storage resources of a cluster, you will be charged for data storage and requests when the cluster requests to pull data stored in COS for computing. Meanwhile, result data storage, backup, or other operations in the computing will also generate new data in COS.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/16871">COS Billing Overview</a></td>
<td><a href="https://buy.cloud.tencent.com/price/cos">COS Pricing</a></td>
</tr>
<tr>
<td>Cloud HDFS (CHDFS)</td>
<td>If you use CHDFS to separate the compute and storage resources of a cluster, you will be charged for data storage and requests when the cluster requests to pull data stored in CHDFS for computing. Meanwhile, result data storage, backup, or other operations in the computing will also generate new data in CHDFS.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1106/41955">CHDFS Purchase Guide</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1106/41955">CHDFS Purchase Guide</a></td>
</tr>
</tbody></table>

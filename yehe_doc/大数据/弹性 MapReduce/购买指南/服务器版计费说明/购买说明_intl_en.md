## Pay-As-You-Go
- You are charged by usage duration of a cluster. This billing mode requires identity verification and will freeze an amount of 2-hour usage fee when the cluster is purchased (vouchers cannot be used here). After this cluster is terminated, the frozen amount will be refunded. Before creating a cluster, check your Tencent Cloud account balance. If your balance is less than the service cost, top up your account first.
- When you purchase an EMR cluster, the price will be listed as an hourly fee. However, you will be billed by the actual seconds of usage and the charge will be rounded to two decimal places. Billing starts from the second the cluster is created and stops the second the cluster is terminated.
- When you purchase a pay-as-you-go cluster, the fee for 2-hour usage under the current configuration will be frozen in your account balance as a deposit. You will then be billed by the hour for your usage over the past hour. When you change the node configuration, the frozen amount will be unfrozen and a new 2-hour deposit will be frozen based on the unit price of the new configuration. Your deposit will be released back to your account when the cluster is terminated.
- For information about what you can do when your account balance is insufficient, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/1026/34537).
- For information about the use and limits of Tencent Cloud vouchers, see [Promo Vouchers](https://intl.cloud.tencent.com/document/product/555/7428).

## Spot Instance
- Similar to pay-as-you-go instances, spot instances are charged by second and billed by hour. The prices of spot instances fluctuate according to market demand, which provide you with a substantial discount (about 80-90% off the prices of pay-as-you-go instances with the same specifications). However, spot instances may be repossessed automatically by the system as a result of inventory shortages or higher bids from other users.
- For more information about spot instance policies, use cases, and limitations, see [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816).

>! Spot instances only support auto scaling to replace compute nodes. The system may repossess spot instances due to higher bids from other users. Therefore, please use them with caution.
>

## Billing Example
### Pay-as-you-go
Assuming you create a Hadoop cluster in Guangzhou Zone 7, with a high-availability cluster of EMR 3.5.0 for the "default scenario". Services deployed include hdfs-3.2.2, yarn-3.2.2, zookeeper-3.6.3, openLDAP-2.4.44, knox-1.6.1, and hive-3.1.3 (with the cluster default mode selected for the Hive metadata storage mode). The pay-as-you-go mode is adopted, with a discount of 15% for EMR, 10% for CDB, and 5% for CBS.
>? The above discounts are provided as an example only. Actual discounts may differ.

EMR cluster fees are shown below:
<table>
<thead>
<tr>
<th>Node Type</th>
<th>Model Specification</th>
<th>System Disk</th>
<th>Data Disk</th>
<th>Model Specification Fee</th>
<th>System Disk Fee</th>
<th>Data Disk Fee</th>
<th>Number of Nodes</th>
</tr>
</thead>
<tbody><tr>
<td>Master</td>
<td>Standard SA2: 4-core CPU, 16 GB memory</td>
<td>SSD 50 GB × 1</td>
<td>SSD 200 GB × 1</td>
<td>0.77</td>
<td>0.0025 × 50 GB × 1</td>
<td>0.0025 × 200 GB × 1</td>
<td>2</td>
</tr>
<tr>
<td>Core</td>
<td>Standard SA2: 4-core CPU, 8 GB memory</td>
<td>SSD 50 GB × 1</td>
<td>SSD 200 GB × 1</td>
<td>0.52</td>
<td>0.0025 × 50 GB × 1</td>
<td>0.0025 × 200 GB × 1</td>
<td>3</td>
</tr>
<tr>
<td>Common</td>
<td>Standard SA2: 2-core CPU, 4 GB memory</td>
<td>SSD 50 GB × 1</td>
<td>SSD 200 GB × 1</td>
<td>0.26</td>
<td>0.0025 × 50 GB × 1</td>
<td>0.0025 × 200 GB × 1</td>
<td>3</td>
</tr>
<tr>
<td>MetaDB</td>
<td colspan=5>High-IO TencentDB - memory: 4,000 MB, hard disk size: 100 GB, 1 instance</td>
<td>USD 0.48/instance</td>
<td>1</td>
</tr>
</tbody></table>

Master node fee = ((0.77 + 0.125) × 0.85 + 200 × 0.0025 × 0.95) × 2 = 2.4715 (USD/hour)
Core node fee = ((0.52 + 0.125) × 0.85 + 200 × 0.0025 × 0.95) × 3 = 3.06975 (USD/hour)
Common node fee = ((0.26 + 0.125) × 0.85 + 200 × 0.0025 × 0.95) × 3 = 2.40675 (USD/hour)
MetaDB node fee = 0.48 × 0.9 = 0.432 (USD/hour)
Total fee = 2.4715 + 3.06975 + 1035.324 + 2.40675 = 8.38 (USD/hour)

>! 
>- The prices provided in this example are for reference only. Refer to the purchase page for actual fees.
>- For information about model specifications and pricing, see [Pricing | Elastic MapReduce](https://buy.cloud.tencent.com/price/emr).
>- The above example only involves the following associated products: CBS and CDB.
>- EMR bills only show the costs of nodes, namely, the costs of CPU, memory, system disk, and local data disk. **The bills of associated cloud products are available in their respective consoles**. For EMR bill details, see [Viewing Bills](https://intl.cloud.tencent.com/document/product/1026/39955) or [Cost Allocation by Tag](https://intl.cloud.tencent.com/document/product/1026/48586).


## Purchase
### Evaluating your business
Before purchasing a cluster, you need to evaluate your business according to the actual situation to ensure that the created cluster meets your actual needs. For more information, see [Business Evaluation](https://intl.cloud.tencent.com/document/product/1026/31098).
### Purchasing EMR clusters
Before using EMR services, you need to register a Tencent Cloud account and go to the [EMR purchase page](https://buy.cloud.tencent.com/emr) to purchase an EMR cluster. For more information, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).

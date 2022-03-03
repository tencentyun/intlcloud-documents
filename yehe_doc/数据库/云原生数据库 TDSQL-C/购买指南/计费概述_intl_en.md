## TDSQL-C for MySQL
TDSQL-C for MySQL offers the following three billing modes:

| Billing Mode | Payment Mode | Use Case |
|---------|---------|---------|
| Monthly subscription | Prepaid. You need to pay the fees when creating an instance. | It is suitable for businesses with stable long-term needs as it is cheaper than pay-as-you-go billing. Moreover, the longer duration the service is purchased for, the cheaper it is. |
| Pay-as-You-Go | Postpaid. You can apply for resources for on-demand use and will be charged based on the actual usage of resources upon settlement. | It is suitable for businesses that may fluctuate greatly and instantaneously. In this mode, instances can be released immediately after use to reduce costs. |
| [Serverless](https://intl.cloud.tencent.com/document/product/1098/40618) | Postpaid. You can first set the maximum and minimum computing power values as needed and will be charged based on the actual usage of computing and storage resources upon settlement. | It is suitable for business scenarios with low frequency and uncertain loads such as development and testing. |

### Billing description
**Total monthly subscription/pay-as-you-go fees = computing node fees + storage space fees = computing node price + storage space price * storage space**

**Total serverless fees = computing node fees + storage space fees = serverless computing power price * number of CCUs + storage space price * storage space**

TDSQL-C adopts a computing-storage separation architecture. It is sold by cluster, and the computing nodes and storage space of each cluster are billed separately:
- Computing node fees are charged using the corresponding billing mode of the specifications you purchase.
- Storage space fees are charged by hour according to the storage space you actually use, which can be viewed on the cluster details page.

### [Product specifications](id:cpgg)

<table>
<thead><tr>
<th rowspan=2 >Compute Node Specification<br>(CPU and Memory)</th>
<th colspan = "2" style="text-align:center" width="50%">Supported Max Storage Space (GB)</th>
<th rowspan=2 >Max IOPS</th>
<th rowspan=2 >I/O Bandwidth</th>
<tr>
<th>MySQL 5.7 (Kernel Minor Version < 2.0.15)<br>MySQL 8.0 (Kernel Minor Version < 3.1.2)</th><th>MySQL 5.7 (Kernel Minor Version ≥ 2.0.15)<br>MySQL 8.0 (Kernel Minor Version ≥ 3.1.2)</th>
</thead><tbody>
<td>1 core, 1 GB</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>1 core, 2 GB</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>2 cores, 4 GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2 cores, 8 GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2 cores, 16 GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>4 cores, 8 GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4 cores, 16 GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4 cores, 32 GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>8 cores, 16 GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8 cores, 32 GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8 cores, 64 GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>16 cores, 64 GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16 cores, 96 GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16 cores, 128 GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>32 cores, 128 GB</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>32 cores, 256 GB</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>64 cores, 256 GB</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>64 cores, 512 GB</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>88 cores, 710 GB</td>
<td>50000</td><td>400000</td><td>780000</td><td>98 Gbps</td></tr>
<tr>
</tbody></table>	

>?If you need other computing node specifications or larger storage space, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Computing node pricing

| Computing Node Specifications | Pay-as-You-Go Price (USD/Hour) | Monthly Subscription Price (USD/Month) |
| ------- | ---------------- |---------------- |
| 2-core 4 GB   |  0.1          |  48  |
| 4-core 8 GB   |  0.2            |  652.8  |
| 8-core 32 GB  |  0.57647059            |  276.70588235  |
| 16-core 64 GB |  1.15294118            |  553.41176471  |
| 16-core 128 GB | 1.85882353          | 892.23529412 |
| 32-core 256 GB |  3.71764706         | 1,784.4705882 |


### Serverless computing power pricing

| Billable Unit | CCU Price (USD/Unit/Second) |
|:--:|:--:|
| Serverless instance | 0.00001397    |

>?
>- CynosDB Compute Unit (CCU) is the computing and billing unit for the Serverless Edition. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater value between the number of CPU cores used by the database and 1/2 of the memory size.
>- You can refer to [product specifications](#cpgg) to select the corresponding maximum and minimum CCU values. The storage space upper limit is the same as the maximum storage space corresponding to the [common computing node specifications](#cpgg).


### Storage space pricing

| Billable Unit | Pay-as-You-Go Price (USD/GB/Hour) |
|:--:|:--:|
| TDSQL-C cluster | 0.00071324    |


#### Pay-as-You-Go billing
You purchased a 2-core 4 GB TDSQL-C cluster that contains 1 instance in Beijing Zone 3, and used 10 GB of storage space every day.

Daily computing node fees = 0.1 USD/hour * 24 hours = 2.4 USD
Daily storage space fees = 0.00071324 USD/GB/hour * 10 GB * 24 hours = 0.1711776 USD
Total daily fees = computing node fees + storage space fees = 2.4 USD + 0.1711776 USD = 2.5711776 USD

#### Serverless billing
You purchased a serverless database with a minimum computing specification of 0.25 CCU/s and a maximum computing specification of 2 CCU/s in Beijing Zone 3, and used 10 GB of storage space and a total of 20,000 CCUs for 6 hours every day.

Daily computing node fees = 20,000 * 0.00001397 USD/unit/second = 0.2794 USD
Daily storage space fees = 0.00071324 USD/GB/hour * 10 GB * 24 hours = 0.1711776 USD
Total daily fees = computing node fees + storage space fees = 0.2794 USD + 0.1711776 USD = 0.4505776 USD

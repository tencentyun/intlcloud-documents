## Billing Mode
TencentDB for TcaplusDB supports the following two billing modes:

| Instance Type | Billing Mode | Use Case |
|----|----|----|
|Standard Cluster Edition|Pay-as-You-Go|This billing mode is suitable for testing, auditing, and development environment. You will be charged according to the daily peak traffic. If no request is made to access the database, you only pay the fees of the minimum reserved resources.|
|Self-deployed Cluster Edition|Pay-as-You-Go|This billing mode is suitable for the production environment. You will be daily charged according to the quantity of access layers and storage layers. You can reduce costs by auto scaling. For example, you can expand cluster capacity before campaigns based on the estimated business peaks, and reduce cluster capacity after campaigns.|

## Settlement Cycle
Fees incurred on the current day are billed the next day.

## Billing Rules for Standard Cluster Edition

The Standard Cluster Edition adopts the pay-as-you-go billing mode. Daily fees are calculated based on the peak database read/write requests and the peak disk capacity used on a day.

**Daily fees = Fees of the peak disk capacity used on a day + Fees of the peak RCUs on a day + Fees of the peak WCUs on a day**

**Concepts**
-**Capacity**: the names of both primary key column and attribute column are counted into the size of each data row.
- **Read CU**: one 4 KB single-row read operation per second is counted as one reserved [read capacity unit (RCU)](https://intl.cloud.tencent.com/document/product/1016/36557).
- **Write CU**: one 4 KB single-row write operation per second is counted as one reserved [write capacity unit (WCU)](https://intl.cloud.tencent.com/document/product/1016/36557).
- **CU calculation rule**: a CU is counted separately at the end of each request and response process. CUs are accumulated and calculated based on the request or response (whichever is greater). Data smaller than 4 KB is rounded up to the nearest 4 KB, and data larger than 4 KB is calculated in multiples of 4 KB. For example, if a 9 KB response is returned for a 1 KB request within one second, because the size of the response is larger than that of the request, the number of CUs will be calculated based on the value of the response. 9 KB is about two 4 KB sets, and the remaining 1 KB is counted as 4 KB, so the total number of CUs will be 2 + 1 = 3.
- **CU statistics rule**: the daily fees are calculated based on the daily access peak to the database. If the database reads reach the highest value at 12:00:00 on a day, the RCUs at this moment will be used to calculate the fees of this day. Similarly, if the database writes reach the highest value at 15:01:00 on a day, the WCUs at this moment will be used to calculate the fees of this day.

### Pricing

| Region | Capacity (USD/GB/day) | RCU (USD/CU/day) |  WCU (USD/CU/day)  |
|---------|---------|---------|---------|
| Chinese mainland | 0.0052 | 0.0019 |  0.0048 |
|   Silicon Valley (Western US)  |0.006289|0.002| 0.0055 |
|Virginia (Eastern US)|0.006289|0.002|0.0055|
|Frankfurt (German)| 0.006 | 0.0022 | 0.0057 |
|  Singapore | 0.0061 |0.0025 | 0.0061 |
|   Hong Kong (China)  | 0.0055 |0.0019 | 0.0055 |
|   Japan  | 0.0055 |0.0019 |0.0055 |
|  Seoul  |0.006289|0.002546|0.00599|

>?
> - Fees are incurred once a cluster is created. The minimum daily consumption of a cluster is 1 GB of disk capacity, 80 RCUs, and 26 WCUs. Even if no tables are created, fees are incurred.
>  - At least 1 GB of disk capacity is reserved for a standard cluster.
>  -  At least 80 RCUs are reserved for a standard cluster.
>  -  At least 26 WCUs are reserved for a standard cluster.
>-  The Standard Cluster Edition supports up to 100,000 QPS. Requests beyond this range will be limited. If your business needs more than 100,000 QPS, we recommend that you use the Self-deployed Cluster Edition which provides higher and more stable performance.
### Billing sample
Assume that you create a cluster in the Shanghai region. On a day, the peak read requests are 80 per second, the peak write requests are 26 per second, and the peak of used disk capacity is 0.5 GB.
The daily fees are calculated as follows:

| Capacity (GB) | Read Requests (RCU) |  Write Requests (WCU)  | Fees |
|---------|---------|---------|-------|
| 1 | 80 |  26 | 1 GB × 0.0052 USD/GB/day + 80 RCUs × 0.0019 USD/RCU/day + 26 WCUs × 0.0048 USD/WCU/day = 0.282 USD/day|

Assume that with the business promotion, applications interact more with the cluster, resulting in higher read/write accesses per second. If the daily peak reads reach 1,000 RCU/s, the daily peak writes 300 WCU/s, and the daily peak data size 1.5 GB, then the daily fees are calculated as follows:

| Capacity (GB) | Read Requests (RCU) |  Write Requests (WCU)  | Fees |
|---------|---------|---------|-------|
| 1.5 | 1,000 |  300 | 1.5 GB × 0.0052 USD/GB/day + 1,000 RCUs × 0.0019 USD/RCU/day + 300 WCUs × 0.0048 USD/WCU/day = 3.3478 USD |


## Billing Rules for Self-deployed Cluster Edition
The Self-deployed Cluster Edition adopts the pay-as-you-go billing mode. Daily fees are calculated based on the actually used resources at the storage layers and access layers on a day.

**Daily fees = Daily unit price of access layer × Access layer quantity + Daily unit price of storage layer (which varies with instance type) × Storage layer quantity**

### Pricing
| Region| Access Layer (USD/layer/day) | One-Primary-One-Secondary T1 Standard Instance at Storage Layer (USD/instance/day) |
|---------|---------|---------|
| Chinese mainland| 0.51 | 65.22 |
|   Virginia (Eastern US)  |1.52| 220.58 |
|   Silicon Valley (Western US)  |1.57| 224.49 |
|Frankfurt (German)| 1.57 | 224.49 |
|  Singapore |1.89 | 224.49 |
|   Hong Kong (China)  | 1.89 |226.38 |
|   Japan  | 1.76 | 226.38 |
|Seoul | 1.76 |222.03 |

### Billing sample
Assume that you create a self-deployed cluster in the Shanghai region. The cluster has four access layers and two storage layers (i.e., two one-primary-one-secondary T1 standard instances).
The daily fees are calculated as follows:

Daily access layer fees = 0.5 × 4 = 2 USD/day
Daily storage layer fees = 64.28471429 × 2 = 128.56942858 USD/day

Total daily fees = 2 + 128.56942858 = 130.56942858 USD/day

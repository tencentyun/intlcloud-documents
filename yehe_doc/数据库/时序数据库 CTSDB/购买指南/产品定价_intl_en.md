## Purchasable Regions 
CTSDB is purchasable in multiple regions around the world. For more information, please see [Regions and AZs](https://intl.cloud.tencent.com/document/product/1100/40937). CTSDB supports separate billing for memory and disks to provide you with more flexible options.

## Price Calculation

**Instance price formula: instance price = memory fees + storage space fees**
- Memory specification fees = total memory specification * memory unit price
- Storage space fees = total storage space * storage unit price
- Total memory specification = memory size per node * number of nodes
- Total storage space = storage space per node * number of nodes

### Node memory pricing
Tiered pricing is added for the pay-as-you-go billing mode. The longer the service is used, the cheaper it is. For more information, please see the price list below:

|CPU<br>(Cores) | Memory<br>(GB) | Applicable Scenario |Writes<br>(Data Points/Second) | Tier 1 for Pay-as-You-Go Billing (0,96 Hours]<br>(USD/GB/Hour) | Tier 2 for Pay-as-You-Go Billing (96,360 Hours]<br>(USD/GB/Hour) | Tier 3 for Pay-as-You-Go Billing (Above 360 Hours)<br> (USD/GB/Hour)|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1   |2   | Test environment | 12500    | 0.02737  | 0.02053  | 0.01368  |
|1   |4   | Production environment | 25000    | 0.02737 | 0.02053 | 0.01368  |
|2   |9   | Production environment | 50000    | 0.02737 | 0.02053 | 0.01368  |
|4   |20 | Production environment | 100000 | 0.02463 | 0.01847  | 0.01232  |
|8   |40 | Production environment | 200000  | 0.02326  | 0.01745 | 0.01163  |
|16 |80 | Production environment | 400000  | 0.02190 | 0.01642 | 0.01095  |
|28 |128 | Production environment | 800000  | 0.02053 | 0.01540  | 0.01026  |

### Node storage space pricing

| Database Type | Pay-as-You-Go Price<br>(USD/GB/Hour) |
|:--:|:--:|
| CTSDB instance | 0.00007353|

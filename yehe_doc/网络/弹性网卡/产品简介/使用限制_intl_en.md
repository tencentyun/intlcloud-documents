The maximum number of ENIs that can be bound to a CVM and the maximum number of private IPs allowed for a single ENI vary with CPU and memory configurations. You can check the details below. For use limits of other VPC products, please [see here](https://intl.cloud.tencent.com/document/product/215/38959).
>- The number of private IPs bound to a single ENI indicates the maximum number allowed. The EIP quota is not provided based on this upper limit but based on EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).
>- The number of ENIs indicates the number of ENIs that can be bound to a CVM. However, CVM instances in the same VPC can bind up to 1,000 ENIs.
>

| CVM configuration | Number of ENIs | Number of private IPs bound to a single ENI |
| -------------------- | :---- | :-------- |
| CPU: 1 core<br/>Memory: 1 GB    | 2     | 2         |
| CPU: 1 core<br/>Memory: >1 GB   | 2     | 6       |
| CPU: 2 cores            | 2     | 10      |
| CPU: 4 cores<br/>Memory: ≤16 GB | 4     | 10      |
| CPU: 4 cores<br/>Memory: >16 GB | 4     | 20      |
| CPU: 8-12 cores         | 6     | 20      |
| CPU: >12 cores | 8 | 30 |

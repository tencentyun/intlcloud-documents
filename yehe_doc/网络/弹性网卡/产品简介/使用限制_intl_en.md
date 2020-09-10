The max number of ENIs that can be bound to a CVM and the max number of private IPs allowed for a single ENI vary according to the CPU and memory specification. You can check th details below. 
>
>- **Number of private IPs per ENI** indicates the max possible number of IPs that can be bound to an ENI. It’s not the available EIP quota. For the EIP quota of your account, please refer to EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).
>- Number of ENIs indicates the number of ENIs that can be bound to the CVM. However, a CVM can have up to 50 ENIs in the same VPC.

| CVM Specification               | Number of ENIs | Number of private IPs per ENI |
| -------------------- | :---- | :-------- |
| CPU: 1 core<br/>Memory: 1G    | 2     | 2         |
| CPU: 1 core  </br>Memory: > 1G   | 2     | 6       |
| CPU: 2 cores            | 2     | 10      |
| CPU: 4 cores  </br>Memory: ≤ 16G | 4     | 10      |
| CPU: 4 cores   </br>Memory: > 16G | 4     | 20      |
| CPU: 8 cores - 12 cores         | 6     | 20      |
| CPU: >12 cores | 8 | 30 |

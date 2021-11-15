To optimize user experience, TencentDB for MongoDB plans to modify the statistical method of the monitoring metric "Capacity Utilization" in November, 2020.

- The current statistical method calculates the average value of capacity utilization of multiple nodes, while the new method will calculate the minimum value of capacity utilization of multiple nodes.
- The minimum value also decides whether TencentDB for MongoDB should lock an instance due to the instance capacity being fully utilized.
- During the modification, it is normal if the capacity utilization of your disk is temporarily reduced.


| Region | Modification Time |
|---------|---------|
| Chongqing, Moscow | November 2, 2020 |
| Tokyo, Virginia, Beijing | November 4, 2020 |
| Mumbai, Nanjing, Singapore | November 9, 2020 |
| Hong Kong (China), Silicon Valley, Tianjin | November 12, 2020 |
| Shanghai, Toronto, Seoul | November 16, 2020 |
| Guangzhou, Frankfurt, Bangkok, Shenzhen | November 19, 2020 |
| Chengdu, Taipei (China) | November 23, 2020  |


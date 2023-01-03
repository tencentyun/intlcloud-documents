
This document describes the specification of TDMQ for Pulsar pro cluster, including TPS, bandwidth, and topic quantity.


## Pro cluster specification

| No. | Cluster Specification Code | Maximum Messaging TPS |	 Peak Bandwidth (MB/s) | Maximum Topics per Cluster | Minimum Storage (GB) |
| :--- | :-------- | :-------- |:-------- |:-------- |:-------- |
| 1	| PULSAR.P1.MINI2  | 2000 | 45 | 1000 | 200 |
| 2 | PULSAR.P1.SMALL4 | 4000 | 90	| 1000 | 200 |
| 3	| PULSAR.P1.SMALL6	| 6000 | 120| 1000 | 300 |
| 4	| PULSAR.P1.SMALL10	| 10000 | 180 | 2000 | 400 |
| 5	| PULSAR.P1.MEDIUM15 | 15000 | 300 | 2000 | 500 |
| 6	| PULSAR.P1.MEDIUM20 | 20000 | 480 | 2000 | 600 |
| 7	| PULSAR.P1.MEDIUM40 | 40000 | 720 | 2000 | 800 |
| 8	| PULSAR.P1.MEDIUM60 | 60000 | 1080 | 2000 | 800 |
| 9	| PULSAR.P1.MEDIUM100 | 100000 | 1920 | 3000 | 2666 |
| 10 | PULSAR.P1.LARGE150 | 150000 | 2400 | 3000 | 3333 |
| 11 | PULSAR.P1.LARGE200 | 200000 | 3600 | 3000 | 4000 |
| 12 | PULSAR.P1.LARGE400 | 400000 | 4200 | 3000 | 5000 |
| 13 | PULSAR.P1.LARGE600 | 600000 | 4800 | 3000 | 6000 |
| 14 | PULSAR.P1.LARGE1000 | 1000000 | 6000 | 3000 | 8334 |

### Notes

The upper limit of messaging TPS is calculated based on the general message type and message size of 4 KB. The values for advanced messages and large messages need to be multiplied accordingly. The peak bandwidth indicates the maximum inbound and outbound bandwidth. For specific calculation methods, see [Pro Cluster Billing](https://www.tencentcloud.com/document/product/1110/52235).


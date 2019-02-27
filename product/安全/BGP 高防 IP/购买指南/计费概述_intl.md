[//]: # (chinagitpath:XXXXX)

## Billing Method
Anti-DDoS Advanced is billed based on "base protection bandwidth (prepaid) + elastic protection bandwidth (postpaid) + forwarding bandwidth (prepaid)".

| Billing Item | Billing Method | Payment Method | Payment Description |
| ----------- | --------------- | ----------- | ----------- |
| Base protection bandwidth | Monthly subscription | Prepaid | Provides base protection bandwidth. The prepaid fee is based on the base protection bandwidth and the purchased usage period. If you upgrade the base defense, extra fees will be charged. The defense can only be upgraded, but cannot be degraded. |
| Elastic protection bandwidth | Pay as you go| Postpaid | If elastic defense is triggered, the fee is charged based on the elastic protection bandwidth range corresponding to the maximum attack traffic of the day, and the bill is generated the next day. No fee occurs if elastic defense is not triggered. |
| Forwarding traffic | Monthly subscription| Prepaid | Business traffic forwarded back to the real server after traffic cleansing. |

## Base Defense
Base defense is prepaid by month. See the following table for the latest prices:

| DDoS Defense | CC Defense | Mainland China BGP (USD/Month) | Outside Mainland China BGP (USD/Month) |
| -------------- | ------------ | ------------------ | ------------------ |
| 10Gbps         | 20,000QPS    | -                  | 2,500             |
| 20Gbps         | 40,000QPS    | 2,400              | 4,800             |
| 30Gbps         | 70,000QPS    | 3,500             | 7,000             |
| 40Gbps         | 100,000QPS   | -                  | 8,200             |
| 50Gbps         | 150,000QPS   | 9,500             | 10,500             |
| 60Gbps         | 200,000QPS   | -                  | 12,000             |
| 80Gbps         | 250,000QPS   | -                  | 15,000             |
| 100Gbps        | 300,000QPS   | 28,000             | 16,500             |

>?
>- Query Per Second (QPS) here is used to measure the number of CC attack requests per second that an Anti-DDoS Advanced instance can defend against.
>- Tencent Cloud provides up to TB-level protection capability. Contact your sales rep if necessary.

## Elastic Protection
You can enable elastic protection manually according to your actual needs.
- When elastic protection is not enabled, the maximum protection bandwidth is the base protection bandwidth and no extra fee is generated.
- When elastic protection is enabled, the elastic protection bandwidth is the maximum protection bandwidth of an instance.
 - When elastic protection is not triggered, no fee is generated.
 - When elastic protection is triggered (the attack traffic is larger than the base protection bandwidth and less than or equal to the elastic protection bandwidth), the fee is charged based on the largest attack traffic of the day, and the bill is generated the next day.

The prices of elastic protection are as follows:

| DDoS Protection Bandwidth       | Mainland China (USD/day) | Outside Mainland China  (USD/Day) |
| -------------------- | ------------------- | ------------------- |
| 10 Gbps < Attack traffic peak ≤ 20 Gbps   | -                   | 320             |
| 20 Gbps < Attack traffic peak ≤ 30 Gbps   | 260              | 400              |
| 30 Gbps < Attack traffic peak ≤ 40 Gbps   | 450               | 700               |
| 40 Gbps < Attack traffic peak ≤ 50 Gbps   | 600               | 800               |
| 50 Gbps < Attack traffic peak ≤ 60 Gbps   | 800               | 1,200               |
| 60 Gbps < Attack traffic peak ≤ 70 Gbps   | 1,200               | 1,800              |
| 70 Gbps < Attack traffic peak ≤ 80 Gbps   | 1,500               | 2,200              |
| 80 Gbps < Attack traffic peak ≤ 90 Gbps   | 1,700               | 2,500              |
| 90 Gbps < Attack traffic peak ≤ 100 Gbps  | 1,900              | 2,700              |
| 100 Gbps < Attack traffic peak ≤ 120 Gbps | 2,100              | 2,900              |
| 120 Gbps < Attack traffic peak ≤ 150 Gbps | 2,300              | 3,200              |
| 150 Gbps < Attack traffic peak ≤ 200 Gbps | 2,700              | 4,000              |
| 200 Gbps < Attack traffic peak ≤ 250 Gbps | 3,200              | 4,800              |
| 250 Gbps < Attack traffic peak ≤ 300 Gbps | 3,800              | 5,600              |
| 300 Gbps < Attack traffic peak ≤ 400 Gbps | -                   | 6,600              |

## Forwarding Traffic
Forwarding traffic refers to the normal traffic that is forwarded back to the real server after being cleansed in Tencent Cloud Anti-DDoS cleansing center.
Forwarding traffic is billed by bandwidth. For non-Tencent Cloud users in Mainland China, 100 Mbps forwarding bandwidth will be given free of cost after they purchase the base protection package. See the following table for the latest prices:

| Bandwidth	| Price (USD/Month) |
|-|-|
|50Mbps|750|
|100Mbps	|1,500|
|150Mbps	|2,250|
|200Mbps|3,000|
|500Mbps	|7,500|
|1Gbps|15,000|
|2Gbps	|30,000|



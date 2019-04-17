[//]: # (chinagitpath:XXXXX)

## Billing Model
Anti-DDoS Advanced uses a combination billing model that utilizes monthly subscription and pay-as-you-go. Base Protection Bandwidth and Forwarding Traffic is billed by monthly subscription. Elastic Protection Bandwidth is pay-as-you-go with a daily billing cycle. 

| Billing Item | Billing Method | Payment Method | Payment Description |
| ----------- | --------------- | ----------- | ----------- |
| Base Protection Bandwidth | Monthly Subscription | Frozen Fees | Bandwidth for base protection. The fee is calculated based on base protection bandwidth limit and the service plan period. Fees for the first month will be frozen in your account upon purchase and deducted on the 1st day of the next month. If you increase the bandwidth, extra fees will apply. Please note that you can only upgrade or keep your current service plan. Downgrade is not supported. |
| Elastic Protection Bandwidth | Pay-as-you-go| Postpaid | Once elastic protection is enabled, you will be charged a fee based the day's  what range of elastic protection bandwidth the maximum attack traffic falls of that day, and receive the bill next day. No fee occurs if the elastic defense is not triggered. |
| Forwarding Traffic | Monthly Subscription| Frozen Fees | Bandwidth of cleaned traffic forwarded back to the real server. |

## Base Protection
Base protection is prepaid by month. See the following table for the latest prices:

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
>- Query Per Second (QPS) measures how many  CC attack requests an Anti-DDoS Advanced instance can defend against in one second.
>- Tencent Cloud provides up to TB-level protection capability. Contact your sales rep if necessary.

## Elastic Protection
You can manually enable elastic protection based on your needs.
- When elastic protection is deactivated, you have the maximum protection bandwidth equal to the base protection bandwidth with no extra charge.
- When elastic protection is activated, the elastic protection bandwidth is the maximum protection bandwidth of the instance.
 - When elastic protection is not triggered, no fee is generated.
 - When elastic protection is triggered ( the attack traffic exceeds the base protection bandwidth limit while the traffic amount is still no greater than the elastic protection bandwidth), the fee is charged based on the largest attack traffic of the day, and the bill is generated the next day.

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
Forwarding traffic refers to the normal traffic that is forwarded back to the real server after being cleansed by Tencent Cloud Anti-DDoS  Advanced IP.
Forwarding traffic is billed by bandwidth. For non-Tencent Cloud users in Mainland China,  they will have 100 Mbps forwarding bandwidth for free after they purchase the base protection service package. See the following table for the latest prices:

| Bandwidth    | Price (USD/Month) |
|-|-|
|50Mbps|750|
|100Mbps    |1,500|
|150Mbps    |2,250|
|200Mbps|3,000|
|500Mbps    |7,500|
|1Gbps|15,000|
|2Gbps    |30,000|

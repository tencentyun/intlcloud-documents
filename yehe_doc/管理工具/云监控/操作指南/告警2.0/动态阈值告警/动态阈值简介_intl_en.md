## What is dynamic threshold alarm?

CM dynamic threshold alarm relies on the Tencent Cloud Intelligent Anomaly Detection (IAD) solution for time series data. CM adopts leading machine learning technologies to learn historical change patterns of metrics for different services. Then CM will intelligently detect metric exceptions and send you alarm notifications with no need for manually setting thresholds.

Dynamic thresholds can be used to detect exceptions in basic and business time series data in various uses cases of monitoring and OPS.

Dynamic thresholds support built-in product monitoring metrics and custom ones. 
- Common built-in monitoring metrics include CPU, memory, network bandwidth, inbound traffic, and outbound traffic.
- Common custom monitoring metrics include latency, user volume, and traffic.


## What are the advantages of dynamic thresholds over static ones?

When you use static thresholds, CM will send alarm notifications only when manually set trigger conditions are met. Static thresholds are only suitable for metrics that fluctuate within a certain range, e.g., CPU/memory/disk utilization. However, static thresholds are not effective for network traffic, latency, and other metrics that fluctuate widely or have no obvious upper and lower boundaries.

Advantages of dynamic thresholds:

- Low labor cost: setting static thresholds relies on experienced developers or OPS personnel. You can save such labor costs by using dynamic thresholds.
- Low maintenance cost: upper and lower boundaries of dynamic thresholds are adaptively adjusted according to historical change patterns of metrics. There is no need for regular maintenance by IT staff.
- More accurate alarming: CM provides multiple built-in detection models to monitor various metrics. CM will detect and learn the trends, cycles, and other aspects of metrics to increase alarm accuracy.

## Limits

- Alarm policy: a user can configure up to 20 alarm policies and create up to 20 alarm objects for each policy.
- Time granularity: currently, only granularity of 1 minute is supported for dynamic thresholds. Other granularities will be supported in the future.
- Data amount: to ensure effective detection by dynamic thresholds, the data amount reported on one metric shall be no less than three days. Otherwise, an alarm will not be triggered.


## How to use dynamic thresholds?
For use instructions, please see [How to Use Dynamic Thresholds](https://intl.cloud.tencent.com/document/product/248/39022) or [Dynamic Alarm Threshold](https://intl.cloud.tencent.com/document/product/248/39443).

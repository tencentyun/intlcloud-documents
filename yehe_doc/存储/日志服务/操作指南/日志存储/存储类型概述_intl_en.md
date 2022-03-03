According to users' different requirements for log search latency and log processing capabilities, CLS provides two storage types: **real-time storage** and **IA storage**.

>!
>   - As an upgraded version of the offline storage solution, IA storage will completely replace it.
>   - Currently, the IA storage solution is in beta testing and available only in Beijing, Guangzhou, Shanghai, and Hong Kong (China). If the solution is unavailable in the region of your log topic, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) for application.
>   - For IA storage in the beta phase, the fees for log write traffic and storage of log topics are exempted. (The beta phase is scheduled to end at 23:59:59 on March 31, 2022.)
>   

## Real-Time Storage

Real-time storage is suitable for users who require statistical analysis and provides log search within seconds, real-time statistical analysis, real-time monitoring, streaming consumption, and other application capabilities.

#### Use Cases

- OPS monitoring and troubleshooting: implements real-time diagnosis of online problems by leveraging the capability of log search within seconds to quickly search the log content scattered on multiple machines for fault cause locating and recovery; calculates quality metrics based on logs in real time and reports alarms when quality metrics exceed thresholds, facilitating development and OPS personnel to discover and rectify faults in the first place.
- Streaming processing: collects the tracking log data of petabyte scale scattered on multiple machines and streams the data to the user-built big data processing cluster in real time for subsequent data lake computing, for example, for the model data calculation business of a recommendation system.



## IA Storage

IA storage is suitable for infrequently accessed logs that do not require statistical analysis, such as archived audit logs. It provides the full-text log search capability, meeting users' requirements for backtracking and archiving historical logs. The overall usage costs of IA storage are 80% lower than those of **real-time storage**. For more information, please see [IA Storage](https://intl.cloud.tencent.com/document/product/614/42004).

#### Use Cases

- Historical logs: the explosive growth of log data makes it expensive to store and analyze logs on a large scale over months or even years. This can cause users to delete valuable data and miss out on important insights that long-term data can yield. **IA storage** can meet the needs of users to conduct large-scale statistical analysis and backtracking of historical data with low costs.
- Non-critical business logs: during troubleshooting, researchers need to pay more attention to ERROR and WARN logs and monitor them and generate alarms when necessary. Non-critical business logs, such as INFO logs, are only archived and need to be searched and analyzed in specific scenarios. Common users do not have specific requirements on the search latency of these logs. Using **IA storage** to store non-critical business logs can significantly reduce user costs and meet users' demands for infrequent search.
- Audit logs: logs for operation and security audits are collected to **IA storage**, and access behaviors, such as operation records of an account or an object, are analyzed via CLS's infrequently accessed log search capability to determine whether there are illegal operations. In addition, logs can be stored for more than 180 days to meet compliance audit requirements.



## Feature Comparison

| Feature       | IA Storage             | Real-Time Storage |
| ------------ | ------------------- | -------- |
| Index creation     | ✓ (supports only full-text indexes) | ✓        |
| Context search   | ✓                   | ✓        |
| Quick analysis     | ×                   | ✓        |
| Full-text search     | ✓ (responds in 2 seconds for searches in 100 million records)                   | ✓ (responds in 0.5 second for searches in 100 million records)        |
| Key-value search     | ×                   | ✓       |
| Log download     | ✓                   | ✓       |
| SQL analysis      | ×                   | ✓        |
| Dashboard       | ×                   | ✓       |
| Alarm monitoring     | ×                   | ✓        |
| Shipping to COS    | ✓                   | ✓        |
| Shipping to CKafka | ✓                   | ✓        |
| Shipping to ES     | ✓                   | ✓       |
| Shipping to SCF    | ✓                   | ✓        |
| Log consumption     | ✓                   | ✓        |
| Data processing     | ✓                   | ✓        |


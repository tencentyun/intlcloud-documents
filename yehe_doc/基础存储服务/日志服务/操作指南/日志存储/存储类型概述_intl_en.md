According to users' different requirements for log search latency and log processing capabilities, CLS provides two storage classes: **STANDARD** and **STANDARD_IA**.

>! Currently, STANDARD_IA log storage is available only in Beijing, Guangzhou, Shanghai, Hong Kong (China), Nanjing, Singapore, Silicon Valley, and Frankfurt regions. If it is not supported in the region of your log topic, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) for application.
> 

## STANDARD

STANDARD storage is suitable for users who require statistical analysis and provides log search within seconds, real-time statistical analysis, real-time monitoring, streaming consumption, and other application capabilities.

### Use cases

- Ops monitoring and troubleshooting: Implements real-time diagnosis of online problems by leveraging the capability of log search within seconds to quickly search the log content scattered on multiple machines for fault cause locating and recovery; calculates quality metrics based on logs in real time and reports alarms when quality metrics exceed thresholds, facilitating development and Ops personnel to discover and rectify faults in the first place.
- Streaming processing: Collects the tracking log data of petabyte scale scattered on multiple machines and streams the data to the user-built big data processing cluster in real time for subsequent data lake computing, for example, for the model data calculation business of a recommendation system.



## STANDARD_IA

STANDARD_IA is suitable for infrequently accessed logs that do not require statistical analysis, such as archived audit logs. It provides the full-text log search capability, meeting users' requirements for backtracking and archiving historical logs. The overall usage costs of STANDARD_IA storage are 80% lower than those of **STANDARD storage**. For more information, see [IA Storage](https://intl.cloud.tencent.com/document/product/614/42004).

### Use cases

- Historical logs: The explosive growth of log data makes it expensive to store and analyze logs on a large scale over months or even years. This can cause users to delete valuable data and miss out on important insights that long-term data can yield. **STANDARD_IA** can meet the needs of users to conduct large-scale statistical analysis and backtracking of historical data with low costs.
- Non-critical business logs: During troubleshooting, developers need to pay more attention to ERROR and WARN logs and monitor them and generate alarms when necessary. Non-critical business logs, such as INFO logs, are only archived and need to be searched and analyzed in specific scenarios. Common users do not have specific requirements on the search latency of these logs. Using **STANDARD_IA** to store non-critical business logs can significantly reduce user costs and meet users' demands for infrequent search.
- Audit logs: Logs for operation and security audits are collected to **STANDARD_IA**, and access behaviors, such as operation records of an account or an object, are analyzed via CLS's infrequently accessed log search capability to determine whether there are illegal operations. In addition, logs can be stored for more than 180 days to meet compliance audit requirements.



## Feature Comparison

| Feature       | STANDARD_IA            | STANDARD |
| ------------ | ------------------- | -------- |
| Index creation     | ✓ (supports only full-text indexes) | ✓        |
| Context search   | ✓                   | ✓        |
| Quick analysis     | ×                   | ✓        |
| Full-text search     | ✓ (responds in 2 seconds for searches in 100 million records)                   | ✓ (responds in 0.5 second for searches in 100 million records)        |
| Key-value search     | ×                   | ✓       |
| Log download     | ✓                   | ✓       |
| SQL analysis      | ×                   | ✓        |
| Dashboard       | ×                   | ✓       |
| Monitoring alarm     | ×                   | ✓        |
| Shipping to COS    | ✓                   | ✓        |
| Shipping to CKafka | ✓                   | ✓        |
| Shipping to ES     | ✓                   | ✓       |
| Shipping to SCF    | ✓                   | ✓        |
| Log consumption     | ✓                   | ✓        |
| Data processing     | ✓                   | ✓        |


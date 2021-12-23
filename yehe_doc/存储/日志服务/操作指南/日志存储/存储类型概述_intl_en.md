According to users' different requirements for log search latency and log processing capabilities, CLS provides two storage types: **real-time storage** and **offline storage**.

>!
> - Currently, the offline log storage solution is in beta testing, and supports only the Beijing, Guangzhou, and Chongqing regions. If the solution is not supported in the region of your log topic, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) for application.
> - For offline storage in the beta phase, the fees for log write traffic and storage of log topics are exempted.
> 

## Real-time Storage

Real-time storage is suitable for users who require real-time log processing and provides log search within seconds, real-time statistical analysis, real-time monitoring, streaming consumption and other application capabilities.

**Use cases**

- OPS monitoring and troubleshooting: implements real-time diagnosis of online problems by leveraging the capability of log search within seconds to quickly search the log content scattered on multiple machines for fault cause locating and recovery; calculates quality metrics based on logs in real time and reports alarms when quality metrics exceed thresholds, facilitating development and OPS personnel to discover and rectify faults in the first place.
- Streaming processing: collects the tracking log data of petabyte scale scattered on multiple machines and streams the data to the user-built big data processing cluster in real time for subsequent data lake computing, for example, for the model data calculation business of a recommendation system.

## Offline Storage

Offline storage is suitable for infrequently accessed logs that do not require real-time search, such as archived audit logs. It provides the minute-level offline log search capability, meeting users' requirements for backtracking and archiving historical logs. The overall usage costs of offline storage are 80% lower than those of **real-time storage**. For more information, please see [Offline Storage](https://intl.cloud.tencent.com/document/product/614/42004).

**Use cases**

- Historical logs: the explosive growth of log data makes it expensive to store and analyze logs on a large scale over months or even years. This can cause users to delete valuable data and miss out on important insights that long-term data can yield. **Offline storage** can meet the needs of users to conduct large-scale statistical analysis and backtracking of historical data with low costs.
- Non-critical business logs: during troubleshooting, researchers need to pay more attention to ERROR and WARN logs and monitor them and generate alarms when necessary. Non-critical business logs, such as INFO logs, are only archived and need to be searched and analyzed in specific scenarios. Common users do not have specific requirements on the search latency of these logs. Using **offline storage** to store non-critical business logs can significantly reduce user costs and meet users' demands for infrequent search.
- Audit logs: logs for operation and security audits are collected to **offline storage**, and access behaviors, such as operation records of an account or an object, are analyzed via the CLS offline search capability to determine whether there are illegal operations. In addition, logs can be stored for more than 180 days to meet compliance audit requirements.

## Feature Comparison

| Feature             | Real-time Storage                                       | Offline Storage                |
| ---------------- | ---------------------------------------------- | ----------------------- |
| **Log search**     | √ (Returns results in real time.)                                | √ (Returns results in minutes offline.)       |
| **SQL aggregate analysis**  | √ (Returns results in real time.)                                | ×                       |
| **Context search**     | √ (Returns results in real time.)                                | √ (Returns results in minutes offline.)       |
| **Visual dashboard** | √                                              | ×                       |
| **Real-time alarm**     | √                                              | ×                       |
| **Log shipping**     | Allows logs to be shipped to CKafka, SCF, and COS in real time. | Allows logs to be shipped only to COS. |
| **Real-time consumption**     | Supports Kafka consumption.                              | ×                       |






















This document describes key terms and concepts for Cloud Monitor.

### Metric

Metric is the fundamental concept in Cloud Monitor. It represents a time-ordered set of data points sent to Cloud Monitor. You can retrieve statistics of those data points as an ordered set of time-series data. A metric can be regarded as a variable to monitor, and metric data represents the value of that variable over time. For example, CPU utilization of a CVM instance is a metric, and capacity utilization of a TencentDB instance is another metric.

Metric data can come from any products, applications, or services. For example, a metric can be the CPU utilization of a CVM instance or the process latency of a user service. Metrics are uniquely defined by a name, a namespace, and one or more dimensions. Each data point has a timestamp, and an optional unit of measure. When a request is made for metric data stored in Cloud Monitor, the returned data stream will be identified by namespace, metric name, and dimension.

### Namespace

A namespace is a container for metrics. Metrics in different namespaces are isolated from each other, so that metrics from different applications will not be mistakenly aggregated.

### Dimension

A dimension is a key-value pair that uniquely identifies a monitored object. A metric is meaningful only after the dimension value is determined. Dimensions are useful for the design of aggregate structure for statistics. For example, two dimension values of server IP and `proc_name` (process name) can identify monitored object A (IP=1.1.1.1&proc_name=test).
You need to specify appropriate dimensions when you input the metric data of a Tencent Cloud product into Cloud Monitor (dimensions are preset for metrics preset by the system). An error may occur if an undefined dimension is used for retrieval.

### Timestamp

Each metric data point in Cloud Monitor must have a timestamp, which indicates the time when the raw data is collected. The timestamp used in a request must be a `dateTime` object and contain the complete date, hours, minutes, and seconds, such as 2000-01-31 23:59:59. We recommend you provide timestamps based on Beijing time (GMT+8).

### Unit

A unit refers to the unit of measure for raw metric data, and an application can derive useful semantic information based on the unit. For example, the unit of CVM's public network outbound bandwidth is Mbps, because network bandwidth is often measured in Mbps for the current network speed. Some common units supported by Cloud Monitor are as listed below:


| Unit | Description |
|---------|---------|
| Second | Time unit |
| Byte | Data size. 1 byte = 8 bits | 
| bit | The smallest unit of data size | 
|% | Percentage | 
| - | Quantity | 
| Bps | Bytes per second | 
| bps | Bits per second | 

### Period

A period refers to the length of time associated with a specific Cloud Monitor statistic. Each timestamp data represents an aggregation of all data collected in a specified period. Although periods are defined in seconds, the minimum granularity of period is one minute. Therefore, the period value you specified should be a multiple of 60. For example, to specify a 6-minute period, you should use the value `360`.

When calling a Cloud Monitor API, you can specify the period through the `period` parameter. When the `GetMonitorData` API is called to get monitoring data, the values of `period`, `startTime`, and `endTime` parameters will determine the amount of data to be returned. For example, calling an API with default parameter values that return the statistics for every 5 minutes of the previous hour, you will retrieve a total of 12 data points. If you want to aggregate statistics once every 10 minutes, set `period` to 600. For statistics aggregated over the entire hour, set it to 3,600.

Period is also an important component for alarms. When creating an alarm trigger, you need to compare the metric with the threshold value you specified. You can specify how many consecutive periods must be met by the monitoring data before an alarm is triggered.

### Alarm

Alarm management is a feature in Tencent Cloud's monitoring and alarm services. It triggers an alarm if Tencent Cloud resources have an exception. You can view alarm information, customize alarm thresholds, and subscribe to alarms. Checks will be performed at set intervals according to your custom thresholds. Once an alarm is trigger, you will receive a notification.

### Alarm policy type
Alarm policy type identifies policy category and corresponds to specific Tencent Cloud products. For example, if you choose the CVM policy, you can customize metric alarms for CPU utilization, disk utilization, and more.

### Alarm policy

An alarm policy is a set of alarm triggers. It is related to project and alarm policy type. Up to 15 alarm policies can be created in each alarm policy type for each project.

An alarm policy includes the following components: alarm trigger, alarm object, and alarm recipient group. After an alarm policy is successfully configured, alarm notifications will be sent to users through SMS, email, and other channels as specified when an alarm is triggered.

### Alarm policy group

An alarm policy group is a set of alarm rules. An alarm policy is related to project and alarm policy type. Up to 15 alarm policy groups can be created in each alarm policy type for each project.

### Alarm recipient group

An alarm recipient group can include one or more users. Alarm notifications are sent through "alarm recipient group". For each alarm policy, notifications will be sent to users in the configured alarm recipient group when the alarm threshold is met. You can go to "Account Center" > "Message Subscription" to add user information and alarm receipt methods.

### Alarm receipt method

This refers to the way users will be notified when an exception occurs, including text message and email.

### Alarm rule

This refers to the action performed when the monitoring data of a metric meets the configured alarm trigger.

### Alarm trigger

An alarm trigger is a semantic condition consisting of metric, comparison, threshold, statistical period, and duration.

### Custom monitoring

Custom monitoring provides flexible and simple custom metric reporting, monitoring, and alarm services, covering diverse monitoring scenarios in addition to standard monitoring metrics. It offers a simple entry for you to self-report monitoring data, while real-time alarms keep you informed on business status.




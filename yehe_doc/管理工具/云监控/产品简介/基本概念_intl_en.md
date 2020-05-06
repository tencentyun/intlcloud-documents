This document describes key terms and concepts for Cloud Monitor.

### Metric

Metric is a fundamental concept in Cloud Monitor. A metric represents a time-ordered set of data points sent to Cloud Monitor. You can retrieve the statistics of those data points in time series. A metric can be seen as a variable to monitor, and the data points represent the values of that variable over time. For example, the CPU utilization of a CVM instance is a metric, and the capacity utilization of a TencentDB instance is another metric.

Metric data can come from any product, application, or service. For example, a metric can be the CPU utilization of a CVM instance or the process latency of a user service. The metric is uniquely defined by a name, a namespace, and one or more dimensions. Each data point has a timestamp and an optional unit of measure. When a request is made for metric data stored in Cloud Monitor, the returned data stream will be identified by namespace, metric name, and dimension.

### Namespace

A namespace is a container for metrics. Metrics in different namespaces are isolated from each other, so metrics from different applications will not be mistakenly aggregated.

### Dimension

A dimension is a key-value pair that uniquely identifies a monitored object. A metric is meaningful only after the dimension value is determined. Dimensions are useful for designing the aggregate structure for statistics. For example, two dimension values of server IP and `proc_name` (process name) can identify monitored object A (IP=1.1.1.1&proc_name=test).
You need to specify the appropriate dimensions when you input the metric data of a Tencent Cloud product into Cloud Monitor (dimensions are preset for metrics preset by the system). An error may occur if an undefined dimension is used for retrieval.

### Timestamp

Each metric data point in Cloud Monitor must have a timestamp, which indicates the time when the raw data is collected. The timestamp used in a request must be a `dateTime` object and contain the complete date, hour, minute, and second, such as 2000-01-31 23:59:59. We recommend you provide timestamps based on Beijing time (GMT+8).

### Unit

A unit refers to the unit of measure for raw metric data, and an application can derive useful semantic information based on the unit. For example, the unit of CVM's outbound bandwidth is Mbps, because network bandwidth often measures current network speed in Mbps. Common units supported by Cloud Monitor are listed below:

| Unit | Description |
| ---- | --------------------------------- |
| Second | Time unit |
| Byte | Data size. 1 byte = 8 bits |
| bit | The smallest unit of data |
|% | Percentage |
| Number of times | Quantity |
| Bps | Bytes per second |
| bps | Bits per second |

### Time granularity

A time granularity refers to a statistical period in Cloud Monitor. Timestamp data represents the result of aggregating all data collected in the specified time granularity. Time granularity is defined in seconds. Cloud Monitor currently supports time granularities of 10 seconds, 60 seconds, and 300 seconds.
When calling a Cloud Monitor API, you can specify the time granularity through the `period` parameter. When the [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881) API is called to get monitoring data, the values of `period`, `startTime`, and `endTime` parameters determine the amount of data to be returned. For example, calling this API with the default values of all parameters will return the statistics for every 300 seconds in the last hour, i.e., a total of 12 data points.
Time granularities are also important for alarms. When creating an alarm trigger condition, you need to set the time granularity and period for the alarm rule. Different granularities and periods indicate different alarm judgment durations.

### Alarm

Alarm management is a feature in Tencent Cloud's monitoring and alarm services. It triggers an alarm if Tencent Cloud resources have an exception, while allowing you to view alarm information, customize alarm thresholds, and subscribe to alarms. Checks will be performed at set intervals according to your custom thresholds. Once an alarm is triggered, you will receive a notification.

### Alarm policy type

Alarm policy type identifies the policy category and corresponds to specific Tencent Cloud products. For example, if you choose the CVM policy, you can customize metric alarms for CPU utilization, disk utilization, and more.

### Alarm policy

An alarm policy is a set of alarm trigger conditions, and is related to the project and alarm policy type. Up to 15 alarm policies can be created in each alarm policy type for each project.

An alarm policy includes the following components: alarm trigger condition, alarm object, and alarm recipient group. After an alarm policy is successfully configured, alarm notifications will be sent to users through SMS, email, and other channels as configured when an alarm is triggered.

### Alarm recipient group

An alarm recipient group can include one or more users. Alarm notifications are sent through "alarm recipient group." For each alarm policy, notifications will be sent to users in the configured alarm recipient group when the alarm threshold is met. You can go to "Account Center" > "Message Subscription" to add user information and alarm receipt methods.

### Alarm receipt method

This refers to the way users will be notified when an exception occurs, such as via SMS and email.

### Alarm rule

This refers to the action performed when the monitoring data of a metric meets the configured alarm trigger condition.

### Alarm trigger condition

An alarm trigger is a semantic condition consisting of metric, comparison relationship, threshold, statistical period, and duration.

### Custom monitoring

Custom monitoring provides flexible and simple custom metric reporting, monitoring, and alarm services, covering diverse monitoring scenarios other than standard monitoring metrics. It offers a simple entry for you to self-report monitoring data, with real-time alarms to keep you informed of the status of your businesses.


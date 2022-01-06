
### AppID

An `AppID` of a Tencent Cloud account is the application ID that has a unique correspondence with the account ID, which will be used by some Tencent Cloud services.

### Data Granularity

A data granularity refers to a statistical period in Cloud Monitor. Timestamp data represents the result of aggregating all data collected in the specified data granularity. Data granularity is defined in seconds. Cloud Monitor currently supports data granularities of 10 seconds, 60 seconds, and 300 seconds.
When calling a Cloud Monitor API, you can specify the data granularity through the `period` parameter. When the `GetMonitorData` API is called to get monitoring data, the values of `period`, `startTime`, and `endTime` parameters determine the amount of data to be returned. For example, calling this API with the default values of all parameters will return the statistics for every 300 seconds in the last hour, i.e., a total of 12 data points.
Data granularities are also important for alarms. When creating an alarm trigger condition, you need to set the data granularity and period for the alarm rule. Different granularities and periods indicate different alarm judgment durations.

### Statistical Method

#### Time dimension
Time dimension is a statistical method used when Cloud Monitor metric data is aggregated from fine to rough granularities. Generally, it can be `Sum`, `Max`, `Min`, `Avg`, or `Last`.
For example, a metric has data of the following granularities: 10 seconds, 60 seconds, and 300 seconds. The time dimension statistical method determines how to calculate 1 piece of data of the 60-second granularity by using 6 pieces of data of the 10-second granularity, and how to calculate 1 piece of data of the 300-second granularity by using 5 pieces of data of the 60-second granularity.
A metric supports a maximum of 5 levels of calculation: 10 seconds, 1 minute, 5 minutes, 1 hour, and 1 day. Each level of calculation uses the same statistic method.
#### Object dimension
Object dimension refers to a statistical method used to aggregate the specific monitoring metric data of multiple instances into total data. Statistical methods of this type generally include `Sum`, `Max`, `Min`, and `Avg`.
When you want to calculate the total data of a metric of all servers in a cluster, the object dimension statistical method determines how to aggregate the data of all servers in the cluster. For example, to calculate the average CPU utilization of the cluster, the aggregation method is `Avg`; to calculate the total bandwidth of the cluster, the aggregation method is `Sum`.

### Dimension

A dimension is a key-value pair that uniquely identifies a monitored object. A metric is meaningful only after the dimension value is determined. Dimensions are useful for designing the aggregate structure for statistics. For example, two dimension values of server IP and `proc_name` (process name) can identify monitored object A (IP=1.1.1.1&proc_name=test).
When you input metric data of a cloud service into Cloud Monitor, you need to specify appropriate dimensions (dimensions are preset for metrics that are preconfigured by the system). An error occurs if an undefined dimension is used for retrieval.

### Metric

Metric is a fundamental concept in Cloud Monitor. A metric represents a time-ordered set of data points sent to Cloud Monitor. You can retrieve the statistics of those data points in time series. A metric can be seen as a variable to monitor, and the data points represent the values of that variable over time. For example, the CPU utilization of a CVM instance is a metric, and the capacity utilization of a TencentDB instance is another metric.

Metric data can come from any product, application, or service. For example, a metric can be the CPU utilization of a CVM instance or the process latency of a user service. The metric is uniquely defined by a name, a namespace, and one or more dimensions. Each data point has a timestamp and an optional unit of measure. When a request is made for metric data stored in Cloud Monitor, the returned data stream will be identified by namespace, metric name, and dimension.


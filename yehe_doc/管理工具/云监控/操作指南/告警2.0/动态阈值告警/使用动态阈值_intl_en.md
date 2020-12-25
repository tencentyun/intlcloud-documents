This document describes how to use dynamic thresholds and their use cases.

## Creating a Dynamic Threshold Alarm Policy

1. Log in to CM console and go to [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist).
2. Go to the **Alarm Policy** page and click **Create**.
3. In the **Alarm Rule Configuration** section, select **Manual Configuration**, and select **Dynamic** as the threshold type. After you finish all configurations, click **Save**.
![](https://main.qcloudimg.com/raw/6eb6ad792dd9dbc6cd9b8151c32359c4.png)
 - **Sensitivity**
The alarm threshold sensitivity is a configuration based on users' perception and is used to control the relative deviation of a metric value for exception detection. The following sensitivity levels are available:
	 - High (default): dynamic thresholds closely follow the trends and patterns of the original metrics. A small deviation will trigger an alarm and thus many alarms will be generated.
	 - Medium: dynamic thresholds follow the original patterns less closely. Fewer alarms will be generated.
	 - Low: dynamic thresholds loosely follow the original patterns, resulting in larger deviations. Only a large deviation will trigger an alarm and thus far less alarms will be generated.
 - **Condition setting**
You can set the same alarm rule for different metrics and can set the alarm trigger condition as a metric going beyond the upper or lower boundary of the dynamic threshold zone. Options include:
	- Outside the dynamic threshold zone. This option is suitable for metrics with smooth curves which you hope not to rise or fall sharply.
	- Above the upper boundary of the dynamic threshold zone. For example, this option is suitable for CPU usage.
	- Below the lower boundary of the dynamic threshold zone. For example, this option is suitable for business success times/rate.


**Chart elements:**

- Blue line: the actual metric curve detected in a period of time.
- Gray zone: the allowed fluctuation range of a metric value. No alarm will be triggered if the metric value is within this zone.
- Blue dot: click the chart by the left mouse button, stay at a point on the blue line, and then you will see a blue dot with the metric value displayed.
- Red line: curve of a period when the metric value is outside the gray zone. The alarm will only be triggered for once and it will not be resolved during this period.

## Use Cases of Dynamic Thresholds

**Use case 1: metrics fluctuate periodically** 
When metrics fluctuate periodically, obvious exceptions cannot be detected if you set static thresholds with large deviations; yet setting static thresholds with small deviations will cause many time periods to be wrongly detected as exceptional. Using dynamic thresholds ensures detection accuracy and avoids repeated alarm notifications. 
![](https://main.qcloudimg.com/raw/7c06b74e495c0000e8e9bc0fefc29695.png)

**Use case 2: metric curves with ascending/descending sections**
If you set static thresholds for metric curves with reasonably ascending/descending sections, such sections will be detected as exceptional. Yet if you use dynamic thresholds, the allowed range will be adjusted adaptively, and exceptions will be reported only when there is a large metric value change.
![](https://main.qcloudimg.com/raw/e56837283ba565fa10668bf76726247f.png)

**Use case 3: metric curves with sudden increase or decrease**
It's hard to set appropriate static thresholds for metric curves with sudden increases or decreases. If such curves do not go beyond a static threshold, the sudden increases or decreases will not be detected as exceptional. Nonetheless, if you use dynamic thresholds, such sudden increases and decreases will be automatically captured, and exceptions will be reported only when there is a large metric value change.

You can set different sensitivity levels to capture changes of different extents for triggering alarms. 
![](https://main.qcloudimg.com/raw/b4623fcf4ad14a61e71da53aca558133.png)



**You are advised to use dynamic thresholds for the following metrics:**

| Use Case | Metric | Description |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Percentage | Success rate, failure rate, packet loss rate, traffic hit rate, outbound traffic utilization, query rejection rate, and bandwidth utilization | Such metrics range between 0 and 100%. Users will only concern if such metrics reach certain levels. For example, users will only care when the disk utilization exceeds 95%. It is suitable to use static thresholds or both static and dynamic ones for such metrics. |
| Network traffic | Network inbound bandwidth, network outbound bandwidth, network inbound packets, and network outbound packets | Such metrics usually change over time with no certain range and may also fluctuate widely. It is suitable to use dynamic thresholds for such metrics. |
| Latency | Number of latencies, latency interval, and latency duration | Such metrics fluctuate mildly yet their ranges are uncertain. It is suitable to use dynamic thresholds for such metrics.  |
| Others | Slow queries, threads of TencentDB, Redis connections, TCP connections, QPS hard disks, IO wait time, temporary tables, full table scans, and unconsumed messages in Kafka | It is suitable to use dynamic thresholds for such metrics.  |



Tencent Cloud Monitor collects and displays data for the CLB instance and the real server, helping you obtain CLB statistics, verify whether the system is running normally, and create alarms. For more information about Tencent Cloud Monitor, see the [Basic Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248) documentation.

Tencent Cloud provides the Cloud Monitor feature for all users by default and does not require manual activation. You can use Cloud Monitor to collect the monitoring data of your CLB instances and view the data using the following methods.

## CLB Console Method
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb), click the monitoring icon next to the CLB instance ID, and then browse the performance data of the instance in the floating window.
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. Click the ID/Name of the CLB instance to access its details page. Click **Monitoring** to view its monitoring data.
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## Cloud Monitor Console Method
Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) to view CLB monitoring data. Click **[Cloud Load Balancer](https://console.cloud.tencent.com/monitor/clb)** on the left sidebar, and then click the ID/name of the CLB instance to access its monitoring details page. You can view the monitoring data of the CLB instance and expand its drop-down list to view the listener and real server monitoring information.

## API Method
Use the `GetMonitorData` API to get the monitoring data of all products. For more information, see [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881), [Public Network CLB Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/10997), [Private Network CLB](https://intl.cloud.tencent.com/document/product/248/39529).

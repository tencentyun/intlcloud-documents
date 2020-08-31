Tencent Cloud Monitor collects and displays data for CLB instance and real server, which helps you obtain CLB statistics, test the system running, and create alarms. For more information, see the [Basic Cloud Monitor](https://intl.cloud.tencent.com/doc/product/248) documentation.

Tencent Cloud provides the Cloud Monitor feature for all users by default without manual activation. You can use Cloud Monitor to collect monitoring data of your CLB instances and view the data in the following ways:

## CLB Console
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), click the monitoring icon near the CLB instance ID, and then browse the performance data of the instance in the floating window.
![](https://main.qcloudimg.com/raw/6580c81d6fd1eee2234fcb5262a976bb.png)
2. Click the ID/Name of the CLB instance to enter its details page. Select the **Monitoring** tab to view the monitoring data of the instance.
![](https://main.qcloudimg.com/raw/3eb231b336c9325ae16bfe2937e41b39.png)

## Cloud Monitor Console
Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) to view CLB monitoring data. Click **Cloud Product Monitoring** -> [**Cloud Load Balancer**](https://console.cloud.tencent.com/monitor/clb) on the left sidebar, and then click the ID/Name of the CLB instance to enter the monitoring details page. You can view monitoring data of the CLB instance, and expand it to view the listener and real server monitoring information.

## API
Use the `GetMonitorData` API to get the monitoring data of all products. For more information, see [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881), [Public Network CLB Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/10997), [Private Network CLB Monitoring Metrics (at the CLB Dimension)](https://intl.cloud.tencent.com/document/product/248/34639), [Private Network CLB Monitoring Metrics (at the Real Server Dimension)](https://intl.cloud.tencent.com/document/product/248/11001) and [CLB Layer-7 Data Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/11004).

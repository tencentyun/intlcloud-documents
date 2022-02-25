## Background
You should enable Grafana (Prometheus) monitoring during cluster purchase to configure the monitoring and alarming feature as needed. After a cluster is created, the cluster details page in the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch) will display a Grafana address, where prom-xxxxxx is the name of the Prometheus instance you purchased.
![](https://main.qcloudimg.com/raw/50a27fa5bd90cce730d235c0b3f87f1b.png)

## Configuring Alarm
1. To configure ClickHouse cluster alarms, go to [Prometheus Monitoring](https://console.cloud.tencent.com/monitor/prometheus) in the CM console, select the Prometheus monitoring instance corresponding to your ClickHouse cluster by region and instance name, and click **Instance ID/Name** to enter the details page.
![](https://main.qcloudimg.com/raw/506a8f0b8629f64321c918364dd9d163.png)
2. On the instance details page, select **Alarm Policy > Create**, select preconfigured basic policies (including the number of connections, CPU, memory, and data disk), and apply them to all nodes of the cluster.
 ![](https://main.qcloudimg.com/raw/ff6f3455368a6c7296513ea9b329f951.png)
The following shows the configuration of an alarm that will be triggered when the used capacity of a data node exceeds 85%:
![](https://main.qcloudimg.com/raw/b4bd4c07484703cd055c6aed099e77d7.png)
3. Configure (or create) a notification template to notify relevant users when the threshold is exceeded. An alarm policy will take effect immediately after it is saved.

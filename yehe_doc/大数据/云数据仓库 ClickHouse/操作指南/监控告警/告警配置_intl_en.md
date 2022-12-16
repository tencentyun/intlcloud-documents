## Background
You should enable Grafana (Prometheus) monitoring during cluster purchase to configure the monitoring and alarming feature as needed. After a cluster is created, the cluster details page in the [CDW console](https://console.cloud.tencent.com/cdwch) will display a Grafana address, where prom-xxxxxx is the name of the Prometheus instance you purchased.

## Configuring an Alarm Policy
1. To configure ClickHouse cluster alarms, go to [Prometheus Monitoring](https://console.cloud.tencent.com/monitor/prometheus) in the CM console, select the Prometheus monitoring instance corresponding to your ClickHouse cluster by region and instance name, and click **Instance ID/Name** to enter the details page.
2. On the instance details page, select **Alarm Policy > Create**, select preconfigured basic policies (including the number of connections, CPU, memory, and data disk), and apply them to all nodes of the cluster.
3. Configure (or create) a notification template to notify relevant users when the threshold is exceeded. An alarm policy will take effect immediately after it is saved.
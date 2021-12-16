You can easily view the running status of Prometheus scrape tasks to check whether the monitoring data is normally scraped by the Prometheus agent in real time.

## Preparations

- The Prometheus agent has been installed in the TKE cluster. For more information, please see Agent Management.
- Click a **Cluster ID** in the [TKE](https://console.cloud.tencent.com/tke2/cluster?rid=4) cluster list to enter the **Integrate with TKE** page.

## Description

- If the status of a scrape task is not found, the Prometheus agent has not correctly obtained the configuration of the corresponding scrape task. Please check whether the configuration is correct.
- The **red** value indicates the number of scrape tasks that failed under this task. You can expand them to view the specific failure causes.

## Directions

1. Click **Targets** on the **Integrate with TKE** page to view all scrape tasks of the current Prometheus agent and the failure causes as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5cc288ad1c66638622b6cf8cbcfb4f16.png)
![](https://main.qcloudimg.com/raw/d58451f7782b17c172d38adcf0957893.png)
2. You can also view the more detailed monitoring status of scrape tasks through the Grafana service provided by TMP. To do so, open Grafana to view the preset **Prometheus** dashboard as shown below:
![](https://main.qcloudimg.com/raw/ce5c3c3d0a183fe0490a2f48f54cac37.png)

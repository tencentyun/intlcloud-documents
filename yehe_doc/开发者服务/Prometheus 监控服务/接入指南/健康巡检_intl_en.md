## Overview

Health check detects the service connectivity on a regular basis to monitor the service health, helping you stay up to date with the service health in real time and promptly discover exceptions to improve the SLA.

## Directions

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Enter the instance details page and click **Integration Center**.
4. Select **Health Check** in **Integration Center** to configure the detection of the corresponding service.

### Detection description

![](https://qcloudimg.tencent-cloud.cn/raw/9e0666c08a6b1c3240150ad4c58abeb4.png)

| Parameter                       | Description                                                         |
| -------------------------- | ------------------------------------------------------------ |
| Name              | Unique detection task name, which corresponds to the detection group on the Grafana monitoring dashboard |
| Detection Method                  | Currently, the following detection methods are supported: <ul style="margin:0;list-style-type:disc;"><li>http_get</li><li>http_post</li><li>tcp</li><li>ssh</li><li>ping</li></ul> |
| Detection Target | Address of the service to be detected |
| Label   | Label with business meaning, which will be automatically added to Prometheus labels |


### Viewing monitoring information

You can clearly view the following status on the monitoring dashboard:
1. Service access latency and health status.
2. Latency in each processing phase of service access.
3. Expiration time of certificate in case of HTTPS
4. Status of various detection types.
   

![](https://qcloudimg.tencent-cloud.cn/raw/9f8f8e8e3ff5780423c253a25e8e4713.png)

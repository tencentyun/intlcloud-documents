## Overview

When using Consul, you need to monitor its running status to know whether it runs normally and troubleshoot its faults. TMP provides an exporter to monitor Consul and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to use TMP to monitor Consul.

## Directions

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Enter the instance details page and click **Integration Center**.
4. Select `Consul` in the Integration Center and click **Install** for integration.

### Configuration description

![](https://qcloudimg.tencent-cloud.cn/raw/d76a4da9bc29bbfca6b8c7b23e9998b5.png)

| Item                       | Description                                                         |
| -------------------------- | ------------------------------------------------------------ |
| Name              | Unique integration name |
| Address                  | Address and port of the Consul instance to be collected |
| Label   | Label with business meaning, which will be automatically added to Prometheus labels |

### Viewing monitoring information

You can clearly view the following monitoring metrics on the monitoring dashboard:
1. Status of Consul cluster nodes.
2. Status of services registered in Consul.


![](https://qcloudimg.tencent-cloud.cn/raw/83b448f34e45abbc0636780702642c00.png)
![](https://qcloudimg.tencent-cloud.cn/raw/b12321e5b2747d1e310c4fd24b3d98f5.png)

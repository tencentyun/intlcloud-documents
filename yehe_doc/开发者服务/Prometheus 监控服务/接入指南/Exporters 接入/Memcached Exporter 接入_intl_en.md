## Overview

When using Memcached, you need to monitor its running status to know whether it runs normally and troubleshoot its faults. TMP provides an exporter to monitor Memcached and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to use TMP to monitor Memcached.

## Directions

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Enter the instance details page and click **Integration Center**.
4. Select `Memcached` in the Integration Center and click **Install** for integration.

### Configuration description

![](https://qcloudimg.tencent-cloud.cn/raw/8d3218bd0419ff314f585d19338e35db.png)

| Item                       | Description                                                         |
| -------------------------- | ------------------------------------------------------------ |
| Name              | Unique integration name |
| Address                  | Address and port of the Memcached instance to be collected |
| Label   | Label with business meaning, which will be automatically added to Prometheus labels |

### Viewing monitoring information

You can clearly view the following monitoring metrics on the monitoring dashboard:
1. Memory utilization. The used memory and total memory are also displayed.
2. Current hit rate of `Get` commands. The hit and miss rates of `Get` commands during the service operation are also displayed.
3. Old data eviction rate and expired data reclaim rate of Memcached. The total numbers of evictions and reclaims during the service operation are also displayed.
4. Total amount of data stored in Memcached.
5. Number of bytes read from and written by the network.
6. Current number of open connections.
7. Ratio of `Get` and `Set` commands during the service operation.
8. Current generation rate of each command.

![](https://qcloudimg.tencent-cloud.cn/raw/83b448f34e45abbc0636780702642c00.png)

![](https://qcloudimg.tencent-cloud.cn/raw/b12321e5b2747d1e310c4fd24b3d98f5.png)

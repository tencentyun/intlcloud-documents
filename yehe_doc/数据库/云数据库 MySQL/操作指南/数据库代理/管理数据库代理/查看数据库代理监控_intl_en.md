This document describes how to view database proxy node monitoring data in the TencentDB for MySQL console.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Supported Monitoring Metrics

| Metric Name | Unit | Description |
|---------|---------|---------|
| Current connections | Count | Current node connections |
| Requests | Count/sec | Node access requests|
| Read requests | Count/sec | Read operation requests |
| Write requests | Count/sec | Write operation requests |
| CPU utilization | % | CPU utilization |
| Memory utilization | % | Memory utilization |
| Memory usage | MB | Used memory |

## Directions
- **Option 1:**
1. Log in to the [TencentDB for MySQL console] (https://console.cloud.tencent.com/cdb). In the instance list, click the ID or **Manage** in the **Operation** column of the source instance with proxy enabled to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Performance Monitoring** page, and click a proxy node name to view its monitoring data. You can switch between different nodes by clicking their names.
>?The default granularity of monitoring within four hours is 5 seconds.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pMhC112_7.png)

- **Option 2:**

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID or **Manage** in the **Operation** column of the source instance with proxy enabled to enter the instance management page.
2. On the instance management page, select the **Database Proxy** > **Overview**, and click icon ![] (https://qcloudimg.tencent-cloud.cn/raw/f3f75f219f501d9b6836b3f542e49ed4.png) after the target node ID in the **Proxy Node** column, then you can view the performance monitoring data of the node.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QtfL186_9.png)
The displayed page after redirection is as follows.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2HR2348_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1673407877191.png)

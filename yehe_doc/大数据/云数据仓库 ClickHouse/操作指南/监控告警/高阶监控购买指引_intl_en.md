## Purchase Method
You can purchase the advanced monitoring feature in the following two ways:
1. Enable Grafana monitoring when creating a cluster to enjoy the monitoring service with over 300 metrics.
![](https://main.qcloudimg.com/raw/cff694ed8a48d746d55360c137329c42.png)
2. Purchase Prometheus monitoring for a previously purchased cluster. From the cluster list in the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), select the **ID/Name** of the target cluster and select **Operation > More > Create Grafana Monitoring**.
 ![](https://main.qcloudimg.com/raw/c628b01c73b2ae0e2e1e3a6c5c8eb1cb.png)
 - Enter a password containing 6–20 characters, including special characters (@$!%\*#?&), letters, and digits.
 - Select a Prometheus service according to your cluster size. We recommend you select a Prometheus cluster based on the peak monitoring TPS and the maximum monitoring data volume. **The basic edition contains a single instance suitable for small-sized businesses, while the cluster edition has multiple distributed instances and features high performance and availability**.
![](https://main.qcloudimg.com/raw/eb2f95c579a248f4a8912ceb871e418b.png)

## User Guide
### Monitoring page entry
You can use advanced monitoring of the ClickHouse cluster in the following two ways:
- Go to the advanced monitoring page from the ClickHouse cluster details page.
![](https://main.qcloudimg.com/raw/bb6722dc3e66f7964f81ff1974fc1af3.png)
- View ClickHouse cluster monitoring in the [CM console](https://console.cloud.tencent.com/monitor/prometheus).
  ![](https://main.qcloudimg.com/raw/6a7166de12457ed6c187b6f891545b7a.png)

Click **Grafana Address** to access the Grafana page of the Prometheus monitoring service, where the default account is `admin` and the password is the one set on the purchase page.

### Getting started with Grafana
When you access the Grafana page for the first time, enter the admin account and password.
 ![](https://main.qcloudimg.com/raw/402606f5b42bbd77304eec84860851fb.png)
On the **Welcome to Grafana** page, click ![](https://main.qcloudimg.com/raw/5e04977fa7f4cb100f2dab5486f4bbc7.png) > **Manage** on the left sidebar to access the preconfigured ClickHouse monitoring dashboard. Later, you can view it directly on the **Home** page.
![](https://main.qcloudimg.com/raw/c99c33f472032dbce4ab40014bacd62b.png)
The **Big Data** folder contains preconfigured templates with the following four dashboards:
- ClickHouse cluster: displays ClickHouse cluster metrics.
- Single-Node server: details the metrics of the single-node server where a ClickHouse cluster resides.
- Multi-Node server: details the metrics of the multi-node server where a ClickHouse cluster resides and horizontally compares key metrics.
- Node overview: displays a general view of the server where a ClickHouse cluster resides.

![](https://main.qcloudimg.com/raw/623df61b0217413435bddfc33817f5d6.png)


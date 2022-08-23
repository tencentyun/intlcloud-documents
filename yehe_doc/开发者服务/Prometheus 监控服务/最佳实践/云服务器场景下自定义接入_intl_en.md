This document describes how to integrate CVM with TMP.

## Purchasing a TMP Instance
>?The purchased TMP instance must be in the same VPC as the monitored CVM instance for network connectivity.

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and click **Create** to purchase a TMP instance. 
![](https://qcloudimg.tencent-cloud.cn/raw/721c025fa3a82df239b240d1d2546471.png)
2. On the purchase page, select the target instance specification and network. Make sure that the TMP and CVM instances have the same VPC IP range so that data can be collected. Select the instance specification based on your reported data volume.
![](https://qcloudimg.tencent-cloud.cn/raw/11d449cab6ebcb10501a63c9cff0c421.png)
3. Click **Buy Now** and make the payment.



## Integrating CVM Basic Metrics
1. Download and install Node Exporter.
Download and install Node Exporter (used to collect basic metric data) in the target CVM instance. Click [here](https://prometheus.io/download/#node_exporter) or run the following command for download:
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz && tar -xvf node_exporter-1.3.1.linux-amd64.tar.gz
```
The file directory is as follows: 
![](https://qcloudimg.tencent-cloud.cn/raw/215bcb6ce3c069bd73eda5a9b1f8bdee.jfif)
2. Run Node Exporter to collect basic monitoring data.
 1. Go to the target folder and run Node Exporter.
```
cd node_exporter-1.3.1.linux-amd64
./node_exporter
```
If the following result is displayed, basic monitoring data has been collected successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/fb9bb9fcfb6f0e1a47ec2942e7215299.png)
 2. Run the following command to expose the basic monitoring data to port 9100:
```
curl 127.0.0.1:9100/metrics
```
You can see the following metric monitoring data that is exposed after the command is executed.
![](https://qcloudimg.tencent-cloud.cn/raw/4295420750699bf57711deb515319131.jfif)
3. Add a scrape task.
Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus), select **Integration Center** > **CVM**, and configure the information in **Task Configuration** as prompted.
Below is a sample configuration of a scrape task:
```
job_name: example-job-name
metrics_path: /metrics
cvm_sd_configs:
- region: ap-guangzhou
  ports:
  - 9100
  filters:         
  - name: tag: Sample tag key
    values: 
    - Sample tag value
relabel_configs: 
- source_labels: [__meta_cvm_instance_state]
  regex: RUNNING
  action: keep
- regex: __meta_cvm_tag_(.*)
  replacement: $1
  action: labelmap
- source_labels: [__meta_cvm_region]
  target_label: region
  action: replace
```


4. Check whether data is reported successfully.
Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and click the Grafana icon to enter Grafana.
Search for `{job="cvm_node_exporter"}` in **Explore** to see whether there is data, and if so, data is reported successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/5df4efbf12becadade7f2de2e64f220c.png)
5. Configure the dashboard page: Every product has some existing JSON files that can be directly imported into the dashboard.  
 1. **Download a dashboard file**: Go to the [**Dashboard** ](https://grafana.com/grafana/dashboards/) page, search for `node_exporter`, and select the latest dashboard for download.
![](https://qcloudimg.tencent-cloud.cn/raw/2198a3ab1f6243ce17addc73856614bb.png)
ii. **Import a JSON file into the dashboard**: Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus), select **Basic Info** > **Grafana Address** to enter Grafana. In the Grafana console, select **Create** > **Import** and upload the dashboard file in **Upload JSON file**.
![](https://qcloudimg.tencent-cloud.cn/raw/a5c4a39697314f2cfcf107a8972fbacc.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3c9a7028eabc4a898e020837c74752d3.png)


## Integrating CVM Metrics at the Business Layer
Prometheus provides four metric types for different monitoring scenarios: Counter, Gauge, Histogram, and Summary. The Prometheus community provides SDKs for multiple programing languages, which are basically similar in usage and mainly differ in the syntax. The following uses Go as an example to describe how to report custom monitoring metrics. For detailed directions of other metric types, see [Custom Monitoring](https://intl.cloud.tencent.com/document/product/1116/43215).

#### Counter
A metric in Counter type increases monotonically and will be reset after service restart. You can use counters to monitor the numbers of requests, exceptions, user logins, orders, etc.
1. You can use a counter to monitor the number of orders as follows:
```
package order

import (
    "github.com/prometheus/client_golang/prometheus"
    "github.com/prometheus/client_golang/prometheus/promauto"
)

// Define the counter object to be monitored
var (
    opsProcessed = promauto.NewCounterVec(prometheus.CounterOpts{
        Name: "order_service_processed_orders_total",
        Help: "The total number of processed orders",
    }, []string{"status"}) // Processing status
)

// Process the order
func makeOrder() {
    opsProcessed.WithLabelValues("success").Inc() // Success
    // opsProcessed.WithLabelValues("fail").Inc() // Failure

    // Order placement business logic
}
```
For example, you can use the `rate()` function to get the order increase rate:
```
rate(order_service_processed_orders_total[5m])
```
2. Expose Prometheus metrics:
Use `promhttp.Handler()` to expose the metric tracking data to the HTTP service.
``` go
package main

import (
	"net/http"

	"github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
        // Business code

        // Expose Prometheus metrics in the HTTP service
        http.Handle("/metrics", promhttp.Handler())

        // Business code
}

```

3. Collect data:
After the tracking of custom metrics for your business is completed and the application is released, you can use Prometheus to collect the monitoring metric data. After the collection is completed, wait a few minutes and then you can view the business metric monitoring data in Grafana integrated in TMP.
![img](https://main.qcloudimg.com/raw/fc6bf3f5cfbab1bbd931d418b9dddef2.png)


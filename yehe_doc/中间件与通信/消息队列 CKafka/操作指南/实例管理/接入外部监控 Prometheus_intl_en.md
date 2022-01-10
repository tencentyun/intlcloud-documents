## Overview

By default, a CKafka Pro Edition instance allows connection with external monitoring services for instance monitoring through the provided access point, including monitoring metrics of open-source Kafka such as **unsynced replicas and incoming message rate**.

**CKafka Pro Edition** instances currently provide Prometheus to scrape the metric information of broker nodes, including basic monitoring metrics such as CPU, memory usage, and system load, as well as the metrics exposed by the broker's JMX.


## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of the target instance to enter its basic information page.
3. Click **Get Monitoring Target** in the top-right corner of the **Prometheus Monitoring** module and select the VPC and subnet.
![](https://qcloudimg.tencent-cloud.cn/raw/38ced4a030cd8e901e5c5f89b7da92fc.png)
4. Click **Submit** to get the set of monitoring targets.
![](https://qcloudimg.tencent-cloud.cn/raw/971340b51689204493944646283efc21.png)
5. Download [Prometheus](https://prometheus.io/download/) and configure the monitoring scrape address.

   1. Enter the directory of the Prometheus package and run the following command to decompress it.
   ```bash
   tar -vxf prometheus-2.30.3.linux-amd64.tar.gz
   ```
   2. Modify the `prometheus.yml` configuration file by adding the `jmx_exporter` and `node_exporter` scrape tasks.
   ```yaml
   scrape_configs:
     # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
     - job_name: "prometheus"
       # metrics_path defaults to '/metrics'
       # scheme defaults to 'http'.
       static_configs:
         - targets: ["localhost:9090"]
   
     - job_name: "broker-jmx-exporter"
       scrape_interval: 5s
       metrics_path: '/metrics'
       static_configs:
         - targets: ['10.x.x.0:60001','10.x.x.0:60003','10.x.x.0:60005']
           labels:
              application: 'broker-jmx'
     - job_name: "broker-node-exporter"
       scrape_interval: 10s
       metrics_path: '/metrics'
       static_configs:
          - targets: ['10.x.x.0:60002','10.x.x.0:60004','10.x.x.0:60006']
            labels:
              application: 'broker-node'
   ```
   Here, `broker-jmx` is the tag configured for the `jmx` metric of the broker scraped by Prometheus, `Targets` contains the information of the mapped port, `broker-node-exporter` is the tag configured for the basic metrics of the node of the scraped broker, and `scrape_interval` is the frequency of scraping metric data.
   3. Start Prometheus.
   ```bash
   ./prometheus --config.file=prometheus.yml --web.enable-lifecycle
   ```
   4. Open the UI provided by Prometheus to check whether the connected targets are normal by entering `http://localhost:9090` in the browser for example.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/3d7fcddaa58fb897aaa597e3f6a6588f.png)
   5. Check and ensure that all targets are in `UP` status.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e54ab826f80668233e3cd3e90b1927f4.png)
	If the targets are in `DOWN` status, check whether the network is accessible or check the `Error` option at the end of the status bar for the cause.

6. Query the monitoring metric data.
   Click **Graph**, enter a metric name such as `node_memory_MemAvailable_bytes`, and click **Execute** to view the monitoring data.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/118a8acfadc562a83f0ebc621eaf79fe.png)

This document describes how to install Node Exporter to expose CVM basic metrics to TMP.

## Directions

### Step 1. Download and install Node Exporter
Download and install Node Exporter (used to collect basic metric data) in the target CVM instance. Click [here](https://prometheus.io/download/#node_exporter) or run the following command for download:
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz && tar -xvf node_exporter-1.3.1.linux-amd64.tar.gz
```
The file directory is as follows: 
![](https://qcloudimg.tencent-cloud.cn/raw/215bcb6ce3c069bd73eda5a9b1f8bdee.jfif)

### Step 2. Run Node Exporter to collect basic monitoring data
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

### Step 3. Configure the collection
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

### Step 4. Check whether data is reported successfully
Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and click the Grafana icon to enter Grafana.
Search for `job="cvm_node_exporter"}` in **Explore** to see whether there is data, and if so, data is reported successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/5df4efbf12becadade7f2de2e64f220c.png)
	 

#### Step 5. Configure the dashboard 	 
Every product has some existing JSON files that can be directly imported into the dashboard.  
1. **Download a dashboard file**: Go to the [**Dashboard** ](https://grafana.com/grafana/dashboards/) page, search for `node_exporter`, and select the latest dashboard for download.
![](https://qcloudimg.tencent-cloud.cn/raw/2198a3ab1f6243ce17addc73856614bb.png)
2. **Import a JSON file into the dashboard**: Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus), select **Basic Info** > **Grafana Address** to enter Grafana. In the Grafana console, select **Create** > **Import** and upload the dashboard file in **Upload JSON file**.
![](https://qcloudimg.tencent-cloud.cn/raw/a5c4a39697314f2cfcf107a8972fbacc.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3c9a7028eabc4a898e020837c74752d3.png)

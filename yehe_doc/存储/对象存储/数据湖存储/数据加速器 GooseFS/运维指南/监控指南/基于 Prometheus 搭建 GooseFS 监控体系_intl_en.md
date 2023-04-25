GooseFS allows you to output metrics to different monitoring systems, including Prometheus. Prometheus is an open-source monitoring framework that Tencent Cloud Observability Platform has integrated with. This document introduces GooseFS metrics and how to report them to the self-built/in-cloud Prometheus.

## Preparations

Before setting up the Prometheus monitoring system, you need to:

- Configure a GooseFS cluster.
- Download the Prometheus installation package (official or Tencent Cloud version).
- Download and configure [Grafana](https://grafana.com/docs/grafana/latest/installation/#install-grafana/).

## Enabling GooseFS Metric Report

1. Edit the GooseFS configuration file `conf/goosefs-site.properties` by adding the configuration items below. Then, use `goosefs copyDir conf/` to copy all worker nodes and use `./bin/goosefs-start.sh all` to restart the cluster.
```plaintext
goosefs.user.metrics.collection.enabled=true
goosefs.user.metrics.heartbeat.interval=10s
```
2. You can run the following command to view the Prometheus master metrics (port: 9201) and worker metrics (port: 9204):
```plaintext
curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/prometheus/
# HELP Master_CreateFileOps Generated from Dropwizard metric import (metric=Master.CreateFileOps, type=com.codahale.metrics.Counter)
...

curl <WORKER_IP>:<WOKER_PORT>/metrics/prometheus/
# HELP pools_Code_Cache_max Generated from Dropwizard metric import (metric=pools.Code-Cache.max, type=com.codahale.metrics.jvm.MemoryUsageGaugeSet$$Lambda$51/137460818)
...
```

## Reporting Metrics to Self-Built Prometheus

1. Download the Prometheus installation package, decompress it, and modify `promethus.yml` as follows:
<pre class="rno-code-pre"><code class="language-plaintext">
# prometheus.yml
global:
	scrape_interval:     10s
	evaluation_interval: 10s
scrape_configs:
	- job_name: 'goosefs masters'
		metrics_path: /metrics/prometheus
		file_sd_configs:
		- refresh_interval: 1m
		files:
		- "targets/cluster/masters/*.yml"
	- job_name: 'goosefs workers'
		metrics_path: /metrics/prometheus
		file_sd_configs:
		- refresh_interval: 1m
		files:
		- "targets/cluster/workers/*.yml"
</code></pre>
2. Create `targets/cluster/masters/masters.yml` and add the IP and port of the master:
<pre class="rno-code-pre"><code class="language-plaintext">
 - targets:
	- "&lt;TARGERTS_MASTER_IP>:&lt;TARGERTS_MASTER_PORT>"
</code></pre>
3. Create `targets/cluster/workers/workers.yml` and add the IP and port of the worker:
<pre class="rno-code-pre"><code class="language-plaintext">
 - targets:
	- "&lt;TARGERTS_WORKER_IP>:&lt;TARGERTS_WORKER_PORT>"
</code></pre>
4. Start Prometheus. `--web.listen-address` specifies the Prometheus listen address. The default port number is 9090.
<pre class="rno-code-pre"><code class="language-plaintext">
nohup ./prometheus --config.file=prometheus.yml --web.listen-address="&lt;LISTEN_IP>:&lt;LISTEN_PORT>" > prometheus.log 2>&1 &
</code></pre>
5. View the GUI:
``` plaintext
http://<PROMETHEUS_BI_IP>:<PROMETHEUS_BI_PORT>
```
6. View the target instance:
``` plaintext
http://<PROMETHEUS_BI_IP>:<PROMETHEUS_BI_PORT>/targets
```

## Reporting Metrics to Tencent Cloud Prometheus

1. Install the Prometheus agent on the master as instructed in the installation guide.
<pre class="rno-code-pre"><code class="language-plaintext">
wget https://rig-1258344699.cos.ap-guangzhou.myqcloud.com/prometheus-agent/agent_install && chmod +x agent_install && ./agent_install prom-12kqy0mw agent-grt164ii ap-guangzhou &lt;secret_id> &lt;secret_key>
</code></pre>
2. Configure jobs for the master and worker:

**Method 1:**
<pre class="rno-code-pre"><code class="language-plaintext">
 job_name: goosefs-masters
 honor_timestamps: true
 metrics_path: /metrics/prometheus
 scheme: http
 file_sd_configs:
 - files:
	- /usr/local/services/prometheus/targets/cluster/masters/*.yml
	refresh_interval: 1m
job_name: goosefs-workers
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
file_sd_configs:
 - files:
	- /usr/local/services/prometheus/targets/cluster/workers/*.yml
	refresh_interval: 1m
</code></pre>

>! Do not use spaces in the value of `job_name`. However, the value of `job_name` in single-machine Prometheus can contain spaces.
>

**Method 2:**
<pre class="rno-code-pre"><code class="language-plaintext">
job_name: goosefs masters
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
static_configs:
- targets:
 - "&lt;TARGERTS_MASTER_IP>:&lt;TARGERTS_MASTER_PORT>"
 refresh_interval: 1m
 
job_name: goosefs workers
honor_timestamps: true
metrics_path: /metrics/prometheus
scheme: http
static_configs:
- targets:
 - "&lt;TARGERTS_WORKER_IP>:&lt;TARGERTS_WORKER_PORT>"
 refresh_interval: 1m
</code></pre>

>! If you use method 2 to configure jobs, you don’t need to create the `masters.yml` and `workers.yml` files under `targets/cluster/masters/`.
> 

## Using Grafana to View Metrics

1. Start Grafana.
```plaintext
nohup ./bin/grafana-server web > grafana.log 2>&1 &
```
2. Open the login page `http://&lt;GRAFANA_IP&gt;:&lt;GRAFANA_PORT&gt;`. By default, Grafana will be listening on port 3000, and both the “username” and “password” are “admin”. You can change the password after your initial login.
3. Create a Prometheus data source.
```plaintext
<PROMETHEUS_IP>:<PROMETHEUS_PORT>
```
4. Import Grafana dashboards for GooseFS. Select JSON import ([Download JSON](https://cos-data-lake-release-1253960454.file.myqcloud.com/goosefs/grafana/goosefs-grafana-dashboard.json)) and use it for the data source created above.
>! You need to set the password when purchasing the in-cloud Prometheus. The configuration of the in-cloud Grafana monitoring GUI is similar to that mentioned above. Note that the configuration of `job_name` should be consistent.
>
5. You can export a modified dashboard.

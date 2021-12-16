## Overview

NGINX exposes certain monitoring metrics through the `stub_status` page. NGINX Prometheus Exporter collects the metrics of a single NGINX instance, converts them into monitoring data that can be used by Prometheus, and exposes the data to the Prometheus service for collection over the HTTP protocol. You can use the exporter to report the key monitoring metrics, which can be used for exception alerting and displayed on the dashboard.



## Directions

### Using Docker container to run exporter

Method 1. Use [nginx-prometheus-exporter](https://hub.docker.com/r/nginx/nginx-prometheus-exporter) to quickly deploy the exporter in a Docker container. Run the following Docker command:
```bash
$ docker run -p 9113:9113 nginx/nginx-prometheus-exporter:0.8.0 -nginx.scrape-uri http://<nginx>:8080/stub_status
```

Method 2. Use the [nginx-prometheus-exporter](https://hub.docker.com/r/nginx/nginx-prometheus-exporter) image to deploy the service in [TKE](https://intl.cloud.tencent.com/zh/document/product/457) and collect the monitoring data through TMP's self-discovery CRD PodMonitor or ServiceMonitor.

### Using binary program to run exporter

#### Downloading and installing explorer

1. Download [NGINX Prometheus Exporter](https://github.com/nginxinc/nginx-prometheus-exporter/releases) from the community for your runtime environment.
2. Install NGINX Prometheus Exporter.

#### Enabling `NGINX stub_status` feature

1. The [stub_status](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html) module of open-source NGINX provides a simple page to display the status data. Run the following command to check whether this module is enabled in NGINX:
```bash
nginx -V 2>&1 | grep -o with-http_stub_status_module
```
	- If `with-http_stub_status_module` is output on the terminal, the `stub_status` module in NGINX is enabled.
	- If no result is output, you can use the `--with-http_stub_status_module` parameter to configure and compile NGINX again from the source code. Below is the sample code:
```
./configure \
… \
--with-http_stub_status_module
make
sudo make install
```
2. After confirming that the `stub_status` module is enabled, modify the NGINX configuration file to specify the URL of the `stub_status` page as follows:
```
server {
    location /nginx_status {
        stub_status;

        access_log off;
        allow 127.0.0.1;
        deny all;
    }
}
```
3. Check NGINX and load it again to make the configuration take effect.
```bash
nginx -t
nginx -s reload
```
4. After completing the above steps, you can view the NGINX metrics through the configured URL.
```plaintext
Active connections: 45
server accepts handled requests
1056958 1156958 4491319
Reading: 0 Writing: 25 Waiting : 7
```



#### Running NGINX Prometheus Exporter

Run the following command to start NGINX Prometheus Exporter:
```bash
$ nginx-prometheus-exporter -nginx.scrape-uri http://<nginx>:8080/nginx_status
```

#### Reported metrics

- `nginxexporter_build_info`, which is the exporter compilation information.
- All [stub_status](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html) metrics.
- `nginx_up`, which displays the last scrape status. `1` indicates success, while `0` indicates failure.


#### Configuring Prometheus scrape job

1. After NGINX Prometheus Exporter runs normally, run the following command to add a job to the Prometheus scrape task.
```bash
...
     - job_name: 'nginx_exporter'
       static_configs:
         - targets: ['your_exporter:port']                    
```
2. Generally, the exporter and NGINX do not run together, so the `instance` of the reported data cannot describe the real instance. To facilitate data search and observation, you can modify the `instance` label and replace it with the real IP to make the label more intuitive as follows:
```bash
...
  - job_name: 'mysqld_exporter'
    static_configs:
    - targets: ['your_exporter:port']
    relabel_configs:
     - source_labels: [__address__]
       regex: '.*'
       target_label: instance
       replacement: '10.0.0.1:80'
```


### Enabling database monitoring dashboard


 TMP provides a preconfigured NGINX exporter dashboard in Grafana. You can view the NGINX monitoring data in the following steps.
1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. Click <img src="https://main.qcloudimg.com/raw/978c842f0c093a31df8d5240dd01016d.png" width="2%"/> on the right of the corresponding instance ID to view the data.
![Nginx Exporter dashboard](https://main.qcloudimg.com/raw/80ff106c4553812d083cd21c211ea950.png)
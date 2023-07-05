

## TKE Nginx-ingress Monitoring Introduction

Nginx Controller now provides monitoring data of the addon running status. You can enable Nginx-ingress monitoring capabilities by configuring Nginx-ingress monitoring.

## Prerequisites

- The cluster has associated with cloud native monitoring PROM instance. For more information, see [Associating with cluster](https://intl.cloud.tencent.com/document/product/457/38825).
- Cloud native monitoring PROM instance needs to be on the same network plane as Nginx.

## Collection Metrics

TKE Nginx-ingress automatically configures the following collection metrics:
- **Nginx status**
 - nginx_ingress_controller_connections_total
 - nginx_ingress_controller_requests_total
 - nginx_ingress_controller_connections
- **Processes**
 - nginx_ingress_controller_num_procs
 - nginx_ingress_controller_cpu_seconds_total
 - nginx_ingress_controller_read_bytes_total
 - nginx_ingress_controller_write_bytes_total
 - nginx_ingress_controller_resident_memory_bytes
 - nginx_ingress_controller_virtual_memory_bytes
 - nginx_ingress_controller_oldest_start_time_seconds
- **Sockets**
 - nginx_ingress_controller_request_duration_seconds
 - nginx_ingress_controller_request_size
 - nginx_ingress_controller_response_duration_seconds
 - nginx_ingress_controller_response_size
 - nginx_ingress_controller_bytes_sent
 - nginx_ingress_controller_ingress_upstream_latency_seconds

You can also configure monitoring collection metrics based on your business needs. For metric details, see [Official Document](https://kubernetes.github.io/ingress-nginx/user-guide/monitoring/).




## Grafana Dashboard of Nginx-ingress Monitoring

After TKE Nginx-ingress has enabled the monitoring feature, it will associate with the cloud native monitoring PROM instance. Cloud native monitoring PROM instance provides a Grafana dashboard. You can directly go to the corresponding Grafana dashboard on the Nginx-ingress addon page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/fea3e7005e93a63b98e37243638ab2af.png)

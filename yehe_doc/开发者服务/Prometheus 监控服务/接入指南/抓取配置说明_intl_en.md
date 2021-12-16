## Overview
Prometheus mainly uses PULL to scrape the monitoring APIs exposed by the target service; therefore, you need to configure the corresponding scrape task to request the monitoring data and write it into the storage provided by Prometheus. Currently, Prometheus provides the configurations of the following tasks:
- Native job configuration: the native scrape job configuration of Prometheus is provided.
- PodMonitor: it collects the corresponding monitoring data in Pods based on Prometheus Operator in the K8s ecosystem.
- ServiceMonitor: it collects the monitoring data in the corresponding Endpoints of Services based on Prometheus Operator in the K8s ecosystem.

>? Configuration items in `[]` are optional.

## Native job configuration

The relevant configuration items are as detailed below:

```yaml

# Scrape task name. `label(job=job_name)` will be added to the corresponding metrics to be scraped at the same time
job_name: <job_name>

# Scrape task interval
[ scrape_interval: <duration> | default = <global_config.scrape_interval> ]

# Scrape request timeout period
[ scrape_timeout: <duration> | default = <global_config.scrape_timeout> ]

# Scrape task request URI path
[ metrics_path: <path> | default = /metrics ]

# Solve the conflict between the scraped label and the label added to Prometheus on the backend
# true: retain the scraped label and ignore the label conflicting with Prometheus on the backend
# false: add `exported_<original-label>` before the scraped label to add the label on the Prometheus backend
[ honor_labels: <boolean> | default = false ]

# Whether to use the time generated on the scrape target
# true: use the time on the target
# false: directly ignore the time on the target
[ honor_timestamps: <boolean> | default = true ]

# Scrape protocol: HTTP or HTTPS
[ scheme: <scheme> | default = http ]

# URL parameter of the scrape request
params:
  [ <string>: [<string>, ...] ]

# Use `basic_auth` to set `Authorization` in the scrape request header. `password` and `password_file` are mutually exclusive, and the value in `password_file` will be used preferably 
basic_auth:
  [ username: <string> ]
  [ password: <secret> ]
  [ password_file: <string> ]

# Use `bearer_token` to set `Authorization` in the scrape request header. `bearer_token` and `bearer_token_file` are mutually exclusive, and the value in `bearer_token` will be used preferably 
[ bearer_token: <secret> ]

# Use `bearer_token` to set `Authorization` in the scrape request header. `bearer_token` and `bearer_token_file` are mutually exclusive, and the value in `bearer_token` will be used preferably 
[ bearer_token_file: <filename> ]

# Specify whether the scrape connection passes through a TLS secure channel and configure the corresponding TLS parameters
tls_config:
  [ <tls_config> ]

# Use a proxy service to scrape metrics on the target and enter the corresponding proxy service address
[ proxy_url: <string> ]

# Use static configuration to specify the target. For more information, please see the description below
static_configs:
  [ - <static_config> ... ]

# Set the CVM scrape configuration. For more information, please see the description below
cvm_sd_configs:
  [ - <cvm_sd_config> ... ]

# After scraping the data, change the label on the target through the relabeling mechanism and run multiple relabeling rules in sequence
# For more information on `relabel_config`, please see the description below
relabel_configs:
  [ - <relabel_config> ... ]

# After the data is scraped and before it is written, use the relabeling mechanism to change the label value and run multiple relabeling rules in sequence
# For more information on `relabel_config`, please see the description below
metric_relabel_configs:
  [ - <relabel_config> ... ]

# Limit of data points in one scrape. 0: no limit. Default value: 0
[ sample_limit: <int> | default = 0 ]

# Limit of targets in one scrape. 0: no limit. Default value: 0
[ target_limit: <int> | default = 0 ]

```

### `static_config` configuration

The relevant configuration items are as detailed below:

<dx-codeblock>
:::  yaml
# Specify the corresponding target host value, such as `ip:port`
targets:
  [ - '<host>' ]

# Add the corresponding label to all targets, which is similar to a global label
labels:
  [ <labelname>: <labelvalue> ... ]
:::
</dx-codeblock>


### `cvm_sd_config` configuration
CVM scrape configuration uses TencentCloud API to automatically get the CVM instance list, and the CVM instance's private IP is used by default. Scrape configuration will generate the following meta labels, which can be used in relabeling configuration.

| Label                | Description |
| ------------------- | --------- |
| \_\_meta\_cvm\_instance\_id | Instance ID |
| \_\_meta\_cvm\_instance\_name | Instance name |
| \_\_meta\_cvm\_instance\_state | Instance status |
| \_\_meta\_cvm\_instance\_type | Instance model |
| \_\_meta\_cvm\_OS | Instance OS |
| \_\_meta\_cvm\_private\_ip | Private IP |
| \_\_meta\_cvm\_public\_ip | Public IP |
| \_\_meta\_cvm\_vpc\_id | VPC ID |
| \_\_meta\_cvm_subnet_id | Subnet ID |
| \_\_meta\_cvm\_tag\_&lt;tagkey&gt; | Instance tag value |
| \_\_meta\_cvm\_region | Instance region |
| \_\_meta\_cvm\_zone | Instance AZ |

CVM scrape configuration description:

<dx-codeblock>
:::  yaml
# Tencent Cloud region. For the region list, please visit https://cloud.tencent.com/document/api/213/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8.
region: <string> 

# Custom endpoint.
[ endpoint: <string> ]

# Credential information for accessing TencentCloud API. If it is not set, the values of the `TENCENT_CLOUD_SECRET_ID` and `TENCENT_CLOUD_SECRET_KEY` environment variables will be used.
[ secret_id: <string> ]
[ secret_key: <secret> ]

# CVM list refresh interval
[ refresh_interval: <duration> | default = 60s ]

# Port for scraping metrics
ports: 
  - [ <int> | default = 80 ]

# CVM list filtering rule. For more information on the supported filtering rules, please visit https://cloud.tencent.com/document/api/213/15728#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0.
filters:
  [ - name: <string>
      values: <string>, [...] ]
:::
</dx-codeblock>

#### Sample

##### Static configuration

<dx-codeblock>
:::  yaml
job_name: prometheus
scrape_interval: 30s
static_configs:
- targets:
  - 127.0.0.1:9090
  :::
  </dx-codeblock>


##### CVM scrape configuration

<dx-codeblock>
:::  yaml
job_name: demo-monitor
cvm_sd_configs:
- region: ap-guangzhou
  ports:
  - 8080
  filters:         
  - name: tag:service
    values: 
    - demo
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
	:::
  </dx-codeblock>

## PodMonitor

The relevant configuration items are as detailed below:

<dx-codeblock>
:::  yaml
# Prometheus Operator CRD version
apiVersion: monitoring.coreos.com/v1
# Corresponding K8s resource type, which is PodMonitor here
kind: PodMonitor
# Corresponding K8s metadata. Here, only the `name` is concerned. If `jobLabel` is not specified, the value of job in the corresponding metric label will be `<namespace>/<name>`
metadata:
  name: redis-exporter # Enter a unique name
  namespace: cm-prometheus  # The namespace is fixed. Do not change it
# Describe the selection of the scrape target Pod and the configuration of the scrape task
spec:
  # Enter the target Pod label. PodMonitor will use the corresponding value as the job label value
  # If Pod YAML configuration is to be viewed, use the value in `pod.metadata.labels`
  # If `Deployment/Daemonset/Statefulset` is to be viewed, use `spec.template.metadata.labels`
  [ jobLabel: string ]
  # Add the label on the corresponding Pod to the target label
  [ podTargetLabels: []string ]
  # Limit of data points in one scrape. 0: no limit. Default value: 0
  [ sampleLimit: uint64 ]
  # Limit of targets in one scrape. 0: no limit. Default value: 0
  [ targetLimit: uint64 ]
  # Configure the Prometheus HTTP port to be exposed and scraped. You can configure multiple Endpoints
  podMetricsEndpoints:
  [ - <endpoint_config> ... ] # For more information, please see the endpoint description below
  # Select the namespace where the Pod to be monitored resides. If it is not specified, all namespaces will be selected
  [ namespaceSelector: ]  
    # Whether to select all namespaces
    [ any: bool ]
    # List of namespace to be selected
    [ matchNames: []string ]
  # Enter the label of the Pod to be monitored to locate the target Pod. For more information, please see [LabelSelector v1 meta](https://v1-17.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#labelselector-v1-meta)
  selector:  
    [ matchExpressions: array ]
      [ example: - {key: tier, operator: In, values: [cache]} ]
    [ matchLabels: object ]
      [ example: k8s-app: redis-exporter ]
	:::
</dx-codeblock>

#### Sample

<dx-codeblock>
:::  yaml
  apiVersion: monitoring.coreos.com/v1
  kind: PodMonitor
  metadata:
    name: redis-exporter # Enter a unique name
    namespace: cm-prometheus  # The namespace is fixed. Do not change it
  spec:
    podMetricsEndpoints:
    - interval: 30s
      port: metric-port  # Enter the name of the corresponding port of the Prometheus exporter in the Pod YAML configuration file
      path: /metrics  # Enter the value of the corresponding path of the Prometheus exporter. If it is not specified, it will be `/metrics` by default
      relabelings:
      - action: replace
        sourceLabels: 
        - instance
        regex: (.*)
        targetLabel: instance
        replacement: 'crs-xxxxxx' # Change it to the corresponding Redis instance ID
      - action: replace
        sourceLabels: 
        - instance
        regex: (.*)
        targetLabel: ip
        replacement: '1.x.x.x' # Change it to the corresponding Redis instance IP
    namespaceSelector:   # Select the namespace where the Pod to be monitored resides
      matchNames:
      - redis-test 
    selector:    # Enter the label value of the Pod to be monitored to locate the target Pod
      matchLabels:
        k8s-app: redis-exporter
	:::
</dx-codeblock>

## ServiceMonitor

The relevant configuration items are as detailed below:

<dx-codeblock>
:::  yaml

# Prometheus Operator CRD version
apiVersion: monitoring.coreos.com/v1
# Corresponding K8s resource type, which is ServiceMonitor here
kind: ServiceMonitor
# Corresponding K8s metadata. Here, only the `name` is concerned. If `jobLabel` is not specified, the value of job in the corresponding metric label will be the Service name
metadata:
  name: redis-exporter # Enter a unique name
  namespace: cm-prometheus  # The namespace is fixed. Do not change it
# Describe the selection of the scrape target Pod and the configuration of the scrape task
spec:
  # Enter the target Pod label (metadata/labels). ServiceMonitor will use the corresponding value as the job label value
  [ jobLabel: string ]
  # Add the label on the corresponding Service to the target label
  [ targetLabels: []string ]
  # Add the label on the corresponding Pod to the target label
  [ podTargetLabels: []string ]
  # Limit of data points in one scrape. 0: no limit. Default value: 0
  [ sampleLimit: uint64 ]
  # Limit of targets in one scrape. 0: no limit. Default value: 0
  [ targetLimit: uint64 ]
  # Configure the Prometheus HTTP port to be exposed and scraped. You can configure multiple Endpoints
  endpoints:
  [ - <endpoint_config> ... ] # For more information, please see the endpoint description below
  # Select the namespace where the Pod to be monitored resides. If it is not specified, all namespaces will be selected
  [ namespaceSelector: ]  
    # Whether to select all namespaces
    [ any: bool ]
    # List of namespace to be selected
    [ matchNames: []string ]
  # Enter the label of the Pod to be monitored to locate the target Pod. For more information, please see [LabelSelector v1 meta](https://v1-17.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.17/#labelselector-v1-meta)
  selector:  
    [ matchExpressions: array ]
      [ example: - {key: tier, operator: In, values: [cache]} ]
    [ matchLabels: object ]
      [ example: k8s-app: redis-exporter ]
	:::
</dx-codeblock>

#### Sample

<dx-codeblock>
:::  yaml
  apiVersion: monitoring.coreos.com/v1
  kind: ServiceMonitor
  metadata:
    name: go-demo    # Enter a unique name
    namespace: cm-prometheus  # The namespace is fixed. Do not change it
  spec:
    endpoints:
    - interval: 30s
      # Enter the name of the corresponding port of the Prometheus exporter in the Service YAML configuration file
      port: 8080-8080-tcp
      # Enter the value of the corresponding path of the Prometheus exporter. If it is not specified, it will be `/metrics` by default
      path: /metrics
      relabelings:
      # ** There must be a label named `application`. Here, suppose that K8s has a label named `app`
      # Use the `replace` action of `relabel` to replace it with `application`
      - action: replace
        sourceLabels:  [__meta_kubernetes_pod_label_app]
        targetLabel: application
    # Select the namespace where the Service to be monitored resides
    namespaceSelector:
      matchNames:
      - golang-demo
    # Enter the label value of the Service to be monitored to locate the target Service
    selector:
      matchLabels:
        app: golang-app-demo
	:::
</dx-codeblock>

## `endpoint_config` Configuration

The relevant configuration items are as detailed below:

<dx-codeblock>
:::  yaml
# Corresponding port name. Note that it is not the port number here. Default value: 80. Corresponding values are as follows:
# ServiceMonitor: `Service>spec/ports/name`
# PodMonitor description:
#   If Pod YAML configuration is to be viewed, use the value in `pod.spec.containers.ports.name`
# If `Deployment/Daemonset/Statefulset` is to be viewed, use `spec.template.spec.containers.ports.name`
[ port: string | default = 80]
# Scrape task request URI path
[ path: string | default = /metrics ]
# Scrape protocol: HTTP or HTTPS
[ scheme: string | default = http]
# URL parameter of the scrape request
[ params: map[string][]string]
# Scrape task interval
[ interval: string | default = 30s ]
# Scrape task timeout period
[ scrapeTimeout: string | default = 30s]
# Specify whether the scrape connection passes through a TLS secure channel and configure the corresponding TLS parameters
[ tlsConfig: TLSConfig ]
# Read the value of the bearer token through the corresponding file and add it to the header of the scrape task
[ bearerTokenFile: string ]
# You can use the corresponding K8s secret key to read the bearer token. Note that the secret namespace must be the same with that of the PodMonitor/ServiceMonitor
[ bearerTokenSecret: string ]
# Solve the conflict between the scraped label and the label added to Prometheus on the backend
# true: retain the scraped label and ignore the label conflicting with Prometheus on the backend
# false: add `exported_<original-label>` before the scraped label to add the label on the Prometheus backend
[ honorLabels: bool | default = false ]
# Whether to use the time generated on the scrape target
# true: use the time on the target
# false: directly ignore the time on the target
[ honorTimestamps: bool | default = true ]
# `basic auth` authentication information. Enter the corresponding K8s secret key value for `username/password`. Note that the secret namespace must be the same as that of the PodMonitor/ServiceMonitor
[ basicAuth: BasicAuth ]
# Use a proxy service to scrape metrics on the target and enter the corresponding proxy service address
[ proxyUrl: string ]
# After scraping the data, change the label on the target through the relabeling mechanism and run multiple relabeling rules in sequence
# For more information on `relabel_config`, please see the description below
relabelings:
[ - <relabel_config> ...]
# After the data is scraped and before it is written, use the relabeling mechanism to change the label value and run multiple relabeling rules in sequence
# For more information on `relabel_config`, please see the description below
metricRelabelings: 
[ - <relabel_config> ...]
	:::
</dx-codeblock>

## `relabel_config` Configuration

The relevant configuration items are as detailed below:

<dx-codeblock>
:::  yaml

# Specify which labels are to be taken from the original labels for relabeling. The taken values are concatenated and separated with the symbol defined in `separator`
# The corresponding configuration item for PodMonitor/ServiceMonitor is `sourceLabels`
[ source_labels: '[' <labelname> [, ...] ']' ]
# Define the separator symbol for concatenating the labels to be relabeled. Default value: `;` 
[ separator: <string> | default = ; ]

# If `action` is ` replace` or `hashmod`, you need to use the `target_label` to specify the corresponding label name
# The corresponding configuration item for PodMonitor/ServiceMonitor is `targetLabel`
[ target_label: <labelname> ]

# Regex for regular match of the values of source labels
[ regex: <regex> | default = (.*) ]

# Calculate the modulus of the MD5 value of the source label. The modulo operation is used if `action` is `hashmod`
[ modulus: <int> ]

# If `action` is `replace`, use `replacement` to define the expression to be replaced after regular match. You can replace it based on regex
[ replacement: <string> | default = $1 ]

# Perform an action based on the value matched by the regex. Valid values of `action` are as follows (the default value is `replace`):
# replace: replace the matched value with that defined in `replacement` if the regex has any match and use `target_label` to set the value and add the corresponding label 
# keep: drop the value if the regex has no matches
# drop: drop the value if the regex has any match
# hashmod: calculate the modulus of the MD5 value of the source label based on the value specified by `modulus` and add a label whose name is specified by `target_label`
# labelmap: use `replacement` to replace the corresponding label name if the regex has any match
# labeldrop: delete the corresponding label name if the regex has any match
# labelkeep: delete the corresponding label name if the regex has no matches
[ action: <relabel_action> | default = replace ]
	:::
</dx-codeblock>

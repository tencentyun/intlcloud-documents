## Overview

When using PostgreSQL, you need to monitor its running status to know whether it runs normally and troubleshoot its faults. TMP provides an exporter to monitor PostgreSQL and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to deploy the PostgreSQL exporter and integrate it with the alert feature.


>?For easier export installation and management, we recommend you use [TKE](https://intl.cloud.tencent.com/zh/document/product/457) for unified management.

## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance.
- You have located and integrated the target TKE cluster in the **Integrate with TKE** section of the **target TMP instance** in the **[TMP console](https://console.cloud.tencent.com/monitor/prometheus)**. For more information, please see Agent Management.


## Directions

### Deploying exporter

1. Log in to the [TKE](https://console.cloud.tencent.com/tke2/cluster) console.
2. Click the ID/name of the cluster whose access credential you want to get to enter the cluster management page.
3. Perform the following steps to deploy an exporter: [Using Secret to manage PostgreSQL password](#step1) > [Deploying PostgreSQL exporter](#step2) > [Getting metric](#step3).


#### Using Secret to manage PostgreSQL password[](id:step1) 

1. On the left sidebar, select **Workload** > **Deployment** to enter the **Deployment** page.
2. In the top-right corner of the page, click **Create via YAML** to create a YAML configuration as detailed below:
   You can use Kubernetes Secrets to manage and encrypt passwords. When starting the PostgreSQL exporter, you can directly use the Secret key but need to adjust the corresponding `password`. Below is a sample YAML configuration:
   <dx-codeblock>
   :::  yaml
   apiVersion: v1
   kind: Secret
   metadata:
    name: postgres-test
   type: Opaque
   stringData:
    username: postgres
    password: you-guess # Corresponding PostgreSQL password
   :::
   </dx-codeblock>

#### Deploying PostgreSQL exporter[](id:step2) 

On the Deployment management page, click **Create** and select the target **namespace** to deploy the service. You can create in the console. Here, YAML is used to deploy the exporter. Below is a sample YAML configuration (please directly copy the following content and adjust the corresponding parameters based on your actual business needs):

<dx-codeblock>
:::  yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres-test
  namespace: postgres-test
  labels:
    app: postgres
    app.kubernetes.io/name: postgresql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
      app.kubernetes.io/name: postgresql
  template:
    metadata:
      labels:
        app: postgres
        app.kubernetes.io/name: postgresql
    spec:
      containers:
      - name: postgres-exporter
        image: wrouesnel/postgres_exporter:latest
        args:
          - "--web.listen-address=:9187"
          - "--log.level=debug"
        env:
          - name: DATA_SOURCE_USER
            valueFrom:
              secretKeyRef:
                name: postgres-test
                key: username
          - name: DATA_SOURCE_PASS
            valueFrom:
              secretKeyRef:
                name: postgres-test
                key: password
          - name: DATA_SOURCE_URI
            value: "x.x.x.x:5432/postgres?sslmode=disable"
        ports:
        - name: http-metrics
          containerPort: 9187
:::
</dx-codeblock>

> ?In the above sample, the username and password in `Secret` are passed in to the environment variables `DATA_SOURCE_USER` and `DATA_SOURCE_PASS`, so the username and password cannot be viewed in plaintext. You can also use `DATA_SOURCE_USER_FILE`/`DATA_SOURCE_PASS_FILE` to read the username and password from the file, or use `DATA_SOURCE_NAME` to put them in the connection string, such as `postgresql://login:password@hostname:port/dbname`.

#### Parameter description

The `query` part (after `?`) in the `DATA_SOURCE_URI`/`DATA_SOURCE_NAME` connection string supports the following parameters (the latest supported parameters listed in [Connection String Parameters](https://pkg.go.dev/github.com/lib/pq#hdr-Connection_String_Parameters) shall prevail):
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>sslmode</td>
<td>Whether to use SSL. Valid values:</td>
</tr>
<tr>
<td>- disable</td>
<td>Do not use SSL</td>
</tr>
<tr>
<td>- require</td>
<td>Always use (skip verification)</td>
</tr>
<tr>
<td>- verify-ca</td>
<td>Always use (check whether the certificate provided by the server is issued by a trusted CA)</td>
</tr>
<tr>
<td>- verify-full</td>
<td>Always use (check whether the certificate provided by the server is issued by a trusted CA and whether the hostname matches the certificate)</td>
</tr>
<tr>
<td>fallback_application_name</td>
<td>Alternative <code>application_name</code></td>
</tr>
<tr>
<td>connect_timeout</td>
<td>Maximum connection wait time in seconds. `0` indicates to wait infinitely</td>
</tr>
<tr>
<td>sslcert</td>
<td>Certificate file path. The file data must be in <code>PEM</code> format</td>
</tr>
<tr>
<td>sslkey</td>
<td>Private key file path. The file data must be in <code>PEM</code> format</td>
</tr>
<tr>
<td>sslrootcert</td>
<td>Root certificate file path. The file data must be in <code>PEM</code> format</td>
</tr>
</tbody></table>

Other supported exporter parameters are as detailed below (for more information, please see [PostgreSQL Server Exporter](https://github.com/wrouesnel/postgres_exporter)):

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>Environment Variable</th>
</tr>
</thead>
<tbody><tr>
<td>--web.listen-address</td>
<td>Listening address. Default value: <code>:9487</code></td>
<td>PG_EXPORTER_WEB_LISTEN_ADDRESS</td>
</tr>
<tr>
<td>--web.telemetry-path</td>
<td>Path under which to expose metrics. Default value: <code>/metrics</code></td>
<td>PG_EXPORTER_WEB_TELEMETRY_PATH</td>
</tr>
<tr>
<td>--extend.query-path</td>
<td>Path of a YAML file containing custom queries to run. For more information, please see <a href="https://github.com/wrouesnel/postgres_exporter/blob/master/queries.yaml">queries.yaml</a></td>
<td>PG_EXPORTER_EXTEND_QUERY_PATH</td>
</tr>
<tr>
<td>--disable-default-metrics</td>
<td>Uses only metrics supplied from <code>queries.yaml</code></td>
<td>PG_EXPORTER_DISABLE_DEFAULT_METRICS</td>
</tr>
<tr>
<td>--disable-settings-metrics</td>
<td>Skips scraping <code>pg_settings</code> metrics</td>
<td>PG_EXPORTER_DISABLE_SETTINGS_METRICS</td>
</tr>
<tr>
<td>--auto-discover-databases</td>
<td>Whether to discover the databases in the PostgreSQL instance dynamically</td>
<td>PG_EXPORTER_AUTO_DISCOVER_DATABASES</td>
</tr>
<tr>
<td>--dumpmaps</td>
<td>Prints the internal metric information to help troubleshoot custom queries (do not use it unless for debugging)</td>
<td>-</td>
</tr>
<tr>
<td>--constantLabels</td>
<td>Custom label provided in the format of <code>key=value</code>. Multiple labels are separated with <code>,</code></td>
<td>PG_EXPORTER_CONSTANT_LABELS</td>
</tr>
<tr>
<td>--exclude-databases</td>
<td>Database to be excluded. It takes effect only if <code>--auto-discover-databases</code> is enabled</td>
<td>PG_EXPORTER_EXCLUDE_DATABASES</td>
</tr>
<tr>
<td>--log.level</td>
<td>Log level. Valid values: <code>debug</code>, <code>info</code>, <code>warn</code>, <code>error</code>, <code>fatal</code></td>
<td>PG_EXPORTER_LOG_LEVEL</td>
</tr>
</tbody></table>

[](id:way)

#### Getting metric[](id:step3)

You cannot get the PostgreSQL instance operation time through `curl http://exporter:9187/metrics`. You can define a `queries.yaml` file to get this metric:

1. Create a [ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) containing `queries.yaml`.
2. Mount the ConfigMap to a directory in the exporter as a volume.
3. Use the ConfigMap through `--extend.query-path` to aggregate the information of the aforementioned [Secret](#step1) and [Deployment](#step2). The YAML file after aggregation is as shown below:

<dx-codeblock>
:::  yaml
# Note: the following document sample code creates a namespace named `postgres-test`, which is for reference only
apiVersion: v1
kind: Namespace
metadata:
  name: postgres-test

# The following document sample code creates a Secret containing a username and password
---
apiVersion: v1
kind: Secret
metadata:
  name: postgres-test-secret
  namespace: postgres-test
type: Opaque
stringData:
  username: postgres
  password: you-guess

# The following document sample code creates a `queries.yaml` file containing custom metrics
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: postgres-test-configmap
  namespace: postgres-test
data:
  queries.yaml: |
    pg_postmaster:
      query: "SELECT pg_postmaster_start_time as start_time_seconds from pg_postmaster_start_time()"
      master: true
      metrics:
        - start_time_seconds:
            usage: "GAUGE"
            description: "Time at which postmaster started"

# The following document sample code mounts the Secret and ConfigMap and defines exporter deployment-related parameters such as image
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres-test
  namespace: postgres-test
  labels:
    app: postgres
    app.kubernetes.io/name: postgresql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
      app.kubernetes.io/name: postgresql
  template:
    metadata:
      labels:
        app: postgres
        app.kubernetes.io/name: postgresql
    spec:
      containers:
        - name: postgres-exporter
          image: wrouesnel/postgres_exporter:latest
          args:
            - "--web.listen-address=:9187"
            - "--extend.query-path=/etc/config/queries.yaml"
            - "--log.level=debug"
          env:
            - name: DATA_SOURCE_USER
              valueFrom:
                secretKeyRef:
                  name: postgres-test-secret
                  key: username
            - name: DATA_SOURCE_PASS
              valueFrom:
                secretKeyRef:
                  name: postgres-test-secret
                  key: password
            - name: DATA_SOURCE_URI
              value: "x.x.x.x:5432/postgres?sslmode=disable"
          ports:
            - name: http-metrics
              containerPort: 9187
          volumeMounts:
            - name: config-volume
              mountPath: /etc/config
      volumes:
        - name: config-volume
          configMap:
            name: postgres-test-configmap
:::
</dx-codeblock>

4. Run `curl http://exporter:9187/metrics`, and you can use the custom `queries.yaml` to query the PostgreSQL instance start time as follows:

```
# HELP pg_postmaster_start_time_seconds Time at which postmaster started
# TYPE pg_postmaster_start_time_seconds gauge
pg_postmaster_start_time_seconds{server="x.x.x.x:5432"} 1.605061592e+09
```



### Adding scrape task

After the exporter runs, you need to configure TMP to discover and collect the monitoring metrics in the following steps:

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click a **cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.
3. In **Scrape Configuration**, add `Pod Monitor` to define a Prometheus scrape task. Below is a sample YAML configuration:

<dx-codeblock>
:::  yaml
  apiVersion: monitoring.coreos.com/v1
  kind: PodMonitor
  metadata:
    name: postgres-exporter
    namespace: cm-prometheus
  spec:
    namespaceSelector:
      matchNames:
      - postgres-test
    podMetricsEndpoints:
    - interval: 30s
      path: /metrics
      port: http-metrics # Port name of the aforementioned exporter container
      relabelings:
      - action: labeldrop
        regex: __meta_kubernetes_pod_label_(pod_|statefulset_|deployment_|controller_)(.+)
      - action: replace
        regex: (.*)
        replacement: postgres-xxxxxx
        sourceLabels:
        - instance
        targetLabel: instance
    selector:
      matchLabels:
        app: postgres
:::
</dx-codeblock>

>?For more advanced usage, please see [ServiceMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#servicemonitor) and [PodMonitor](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#podmonitor).

### Visualizing Grafana dashboard

> ?You need to use the configuration in [Getting metric](#step3) to get the PostgreSQL instance start time.

1. In the [TMP instance](https://console.cloud.tencent.com/monitor/prometheus) list, find the corresponding TMP instance, click <img src="https://main.qcloudimg.com/raw/978c842f0c093a31df8d5240dd01016d.png" width="2%"> on the right of the instance ID to open your Grafana page, and enter your account and password to access the Grafana visual dashboard operation section.
2. Enter Grafana, click the <img src="https://main.qcloudimg.com/raw/7e3fff6131aa085987552a9725e9ae54.png" width="2%"> icon to expand the monitoring dashboard, and click the name of the corresponding monitoring chart to view the monitoring data.
![](https://main.qcloudimg.com/raw/91715279d22a1f6efe1844e318712391.png)

### Integrating with alert feature

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Alerting Rule** and add the corresponding alerting rules. For more information, please see Creating Alerting Rule.
> ?TMP will provide more PostgreSQL alerting templates in the near future.

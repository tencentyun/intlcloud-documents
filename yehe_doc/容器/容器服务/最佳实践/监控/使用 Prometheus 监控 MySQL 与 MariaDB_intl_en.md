## Overview

MySQL is a common relational database management system. As a branch of MySQL, MariaDB is compatible with MySQL and is becoming increasingly popular. In a Kubernetes environment, you can use Prometheus to monitor MySQL and MariaDB database using the open-source [MySQL exporter](https://github.com/prometheus/mysqld_exporter). This document describes how to use Prometheus to monitor MySQL and MariaDB.


## Introduction to MySQL Exporter

The [MySQL exporter](https://github.com/prometheus/mysqld_exporter) reads database status data from MySQL or MariaDB, converts it to Prometheus metric format, and opens it to the HTTP interface. In this case, Prometheus can collect and monitor these metrics.
<img style="width:80%" src="https://main.qcloudimg.com/raw/5b8918c8804589aa0b7cc947a6481d11.png" data-nonescope="true">

## Directions
<span id="mysqld-exporter"></span>
### Deploying the MySQL exporter

>! Before deploying the MySQL exporter, ensure that MySQL or MariaDB has been deployed in the cluster, outside the cluster, or in the cloud service used.
<span id="MySQL"></span>
#### Deploying MySQL
The following example shows how to deploy MySQL to a cluster from the Marketplace.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Marketplace** in the left sidebar.
2. On the **Marketplace** page, search for and click **MySQL**.
3. On the **Application Details** page, click **Create Application**.
4. On the **Create Application** page, enter the necessary information and click **Create**.
5. Run the following command to check whether MySQL runs properly:
``` bash
$ kubectl get pods
NAME                     READY   STATUS        RESTARTS   AGE
mysql-698b898bf7-4dc5k   1/1     Running       0          11s
```
6. Run the following command to obtain the root password:
``` bash
$ kubectl get secret -o jsonpath={.data.mysql-root-password} mysql
6ZAj33yLBo
```

#### Deploying the MySQL exporter

After [deploying MySQL](#MySQL), deploy the MySQL exporter as follows:
1. Run the following commands in sequence to create a MySQL exporter account and log in to MySQL:
```
$ kubectl exec -it mysql-698b898bf7-4dc5k bash
```
```
$ mysql -uroot -p6ZAj33yLBo
```
2. Run the following command to create an account. `mysqld-exporter/123456` is used as an example.
``` bash
CREATE USER 'mysqld-exporter' IDENTIFIED BY '123456' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, REPLICATION SLAVE, SELECT ON *.* TO 'mysqld-exporter';
flush privileges;
```
3. Use the YAML file to deploy the MySQL exporter. An example is as follows:
> ! Replace the account, password, and MySQL connection address in DATA_SOURCE_NAME with real ones.
> 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysqld-exporter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysqld-exporter
  template:
    metadata:
      labels:
        app: mysqld-exporter
    spec:
      containers:
      - name: mysqld-exporter
        image: prom/mysqld-exporter:v0.12.1
        args:
        - --collect.info_schema.tables
        - --collect.info_schema.innodb_tablespaces
        - --collect.info_schema.innodb_metrics
        - --collect.global_status
        - --collect.global_variables
        - --collect.slave_status
        - --collect.info_schema.processlist
        - --collect.perf_schema.tablelocks
        - --collect.perf_schema.eventsstatements
        - --collect.perf_schema.eventsstatementssum
        - --collect.perf_schema.eventswaits
        - --collect.auto_increment.columns
        - --collect.binlog_size
        - --collect.perf_schema.tableiowaits
        - --collect.perf_schema.indexiowaits
        - --collect.info_schema.userstats
        - --collect.info_schema.clientstats
        - --collect.info_schema.tablestats
        - --collect.info_schema.schemastats
        - --collect.perf_schema.file_events
        - --collect.perf_schema.file_instances
        - --collect.perf_schema.replication_group_member_stats
        - --collect.perf_schema.replication_applier_status_by_worker
        - --collect.slave_hosts
        - --collect.info_schema.innodb_cmp
        - --collect.info_schema.innodb_cmpmem
        - --collect.info_schema.query_response_time
        - --collect.engine_tokudb_status
        - --collect.engine_innodb_status
        ports:
        - containerPort: 9104
          protocol: TCP
        env:
        - name: DATA_SOURCE_NAME
          value: "mysqld-exporter:123456@(mysql.default.svc.cluster.local:3306)/"
--
apiVersion: v1
kind: Service
metadata:
  name: mysqld-exporter
  labels:
    app: mysqld-exporter
spec:
  type: ClusterIP
  ports:
  - port: 9104
    protocol: TCP
    name: http
  selector:
    app: mysqld-exporter
```


### Configuring monitoring data collection

After [deploying the MySQL exporter](#mysqld-exporter), configure monitoring data collection to ensure that data exposed by the MySQL exporter can be collected.
The following example shows ServiceMonitor definition (The cluster must support ServiceMonitor definition to configure collection rules):
```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: mysqld-exporter
spec:
  endpoints:
    interval: 5s
    targetPort: 9104
  namespaceSelector:
    matchNames:
    - default
  selector:
    matchLabels:
      app: mysqld-exporter
```
The following example shows a native Prometheus configuration:
```
    - job_name: mysqld-exporter
      scrape_interval: 5s
      kubernetes_sd_configs:
      - role: endpoints
        namespaces:
          names:
          - default
      relabel_configs:
      - action: keep
        source_labels:
        - __meta_kubernetes_service_label_app_kubernetes_io_name
        regex: mysqld-exporter
      - action: keep
        source_labels:
        - __meta_kubernetes_endpoint_port_name
        regex: http
```

### Adding a monitoring dashboard

Once data can be collected, add a monitoring dashboard for Grafana to display data.
- If you only need to view the MySQL or MariaDB overview information, import the [grafana.com](https://grafana.com/grafana/dashboards/7362) dashboard, as shown in the figure below.
<img style="width:80%" src="https://main.qcloudimg.com/raw/0ddd9f644530e96c7d05bfe4acc3c2d7.png" data-nonescope="true">
- If a dashboard with more features is required, import JSON files prefixed with `MySQL_` in the [percona open-source dashboard](https://github.com/percona/grafana-dashboards/tree/master/dashboards).

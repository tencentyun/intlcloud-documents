GooseFS records monitoring data based on the [Coda Hale Metrics Library](https://github.com/dropwizard/metrics). It allows you to obtain metric data in different ways such as the CLI, console, and files. GooseFS currently supports the following metric obtaining methods:
- MetricsServlet: monitoring metrics are provided to users in JSON format.
- CsvSink: monitoring metrics are provided in CSV files. After configuration, monitoring metrics are periodically generated in CSV files.
- PrometheusMetricsServlet: monitoring metrics are provided to users in the format defined by Prometheus.

The above monitoring metrics can be specified in the configuration file. The default path of the GooseFS monitoring metric configuration file is `$ GooseFS_HOME/conf/metrics.properties`. You can use `goosefs.metrics.conf.file` to specify a custom monitoring configuration file. GooseFS provides users with a default template `metrics.properties.template` that contains all configurable attributes.

## Getting Monitoring Metrics

The following describes three basic methods for obtaining monitoring metrics:

### 1. Pulling monitoring metrics via JSON format

GooseFS adopts the method of pulling monitoring metrics in JSON format by default, which corresponds to the MetricsServlet configuration item. You can use the CLI to initiate an HTTP request to the leading master node of GooseFS to pull all desired monitoring metrics. The metrics port is 9201 for the master node and 9204 for a worker node. The request format is as follows:

```plaintext
$ curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/json
```

In this format, <LEADING_MASTER_HOSTNAME> must be a valid master node IP address, and <MASTER_WEB_PORT> must be an enabled port.

To get the monitoring metrics of a specific worker node, use the following command:

```plaintext
$ curl <WORKER_HOSTNAME>:<WORKER_WEB_PORT>/metrics/json
```

### 2. Getting monitoring metrics via CSV files

GooseFS allows you to export data to CSV files. You can use this capability to get monitoring metrics. First, you need to prepare a directory to store monitoring metrics:

```plaintext
$ mkdir /tmp/goosefs-metrics
```

After the storage path is prepared, modify the `conf/metrics.properties` configuration file to enable the CsvSink capability:

```plaintext
sink.csv.class=goosefs.metrics.sink.CsvSink # Enable the CsvSink capability

sink.csv.period=1 # Set the monitoring metric export period
sink.csv.unit=senconds # Set the unit of the monitoring metric export period

sink.csv.directory=/tmp/goosefs-metrics # Set the monitoring metric export path
```


After the configuration, you need to restart the node for the configuration to take effect. After the configuration takes effect, the monitoring metrics will be periodically exported to CSV files and stored to the specified path.

>!
>- GooseFS provides a monitoring configuration template. For more information, see the `conf/metrics.properties.template` file.
>- If GooseFS is deployed on a cluster, ensure that the specified metric storage path can be read by all nodes.

### 3. Pulling Prometheus monitoring metrics
You can run the following commands to view Prometheus monitoring metrics on the GooseFS master node (metrics port: 9201) and worker node (metrics port: 9204):
```plaintext
curl <LEADING_MASTER_HOSTNAME>:<MASTER_WEB_PORT>/metrics/prometheus/
# HELP Master_CreateFileOps Generated from Dropwizard metric import (metric=Master.CreateFileOps, type=com.codahale.metrics.Counter)
...

curl <WORKER_IP>:<WOKER_PORT>/metrics/prometheus/
# HELP pools_Code_Cache_max Generated from Dropwizard metric import (metric=pools.Code-Cache.max, type=com.codahale.metrics.jvm.MemoryUsageGaugeSet$$Lambda$51/137460818)
...
```

## Overview

Compatible with the APIs of Prometheus and Grafana and the CRD usage of mainstream prometheus-operator, TKE Cloud Native Monitoring is more flexible and extensible. Combined with Prometheus open source tools, it can have more advanced usages.
This document describes how to use auxiliary scripts and migration tools to quickly migrate the self-built Prometheus to cloud native monitoring.


## Prerequisites


You have installed [Kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) on the node of the self-built Prometheus cluster and configured Kubeconfig to ensure that you can manage the cluster through Kubectl.

## Directions


### Migrating the Dynamic Collection Configuration

If the prometheus-operator is used in self-built Prometheus, CRD resources such as ServiceMonitor and PodMonitor are usually used to dynamically add collection configurations. This method also applies to cloud native monitoring. If you only need to migrate the prometheus-operator of the self-built Prometheus cluster to cloud native monitoring, and without migrating the cluster, then there is no need to migrate the dynamic configuration. You only need to use the cloud native monitoring to associate the self-built cluster, and then the ServiceMonitor and PodMonitor resources created by the self-built Prometheus will automatically take effect in cloud native monitoring.

For cross-cluster migration, you can export the CRD resources of self-built Prometheus and selectively reapply them in the associated cloud native monitoring cluster. The following describes how to export ServiceMonitor and PodMonitor in batches in a self-built Prometheus cluster.



1. Create the script `prom-backup.sh` with the following contents:
``` bash
_ns_list=$(kubectl get ns | awk '{print $1}' | grep -v NAME)
count=0
declare -a types=("servicemonitors.monitoring.coreos.com" "podmonitors.monitoring.coreos.com")
for _ns in ${_ns_list}; do
 ## loop for types
    for _type in "${types[@]}"; do
       echo "Backup type [namespace: ${_ns}, type: ${_type}]."
	     _item_list=$(kubectl -n ${_ns} get ${_type} | grep -v NAME | awk '{print $1}' )
       ## loop for items
	 	for _item in ${_item_list}; do
           _file_name=./${_ns}_${_type}_${_item}.yaml
		    echo "Backup kubernetes config yaml [namespace: ${_ns}, type: ${_type}, item: ${_item}] to file: ${_file_name}"
		    kubectl -n ${_ns} get ${_type} ${_item} -o yaml > ${_file_name}
		    count=$[count + 1]
		    echo "Backup No.${count} file done."
	     done;
    done;
   done;
```
2. Run the following command to run the `prom-backup.sh` script.
```bash
bash prom-backup.sh
```
3. The `prom-backup.sh` script will export each ServiceMonitor and PodMonitor resource into a separate YAML file. You can run the `ls` command to view the output file list. The example is as follows:
```bash
$ ls
kube-system_servicemonitors.monitoring.coreos.com_kube-state-metrics.yaml
kube-system_servicemonitors.monitoring.coreos.com_node-exporter.yaml
monitoring_servicemonitors.monitoring.coreos.com_coredns.yaml
monitoring_servicemonitors.monitoring.coreos.com_grafana.yaml
monitoring_servicemonitors.monitoring.coreos.com_kube-apiserver.yaml
monitoring_servicemonitors.monitoring.coreos.com_kube-controller-manager.yaml
monitoring_servicemonitors.monitoring.coreos.com_kube-scheduler.yaml
monitoring_servicemonitors.monitoring.coreos.com_kube-state-metrics.yaml
monitoring_servicemonitors.monitoring.coreos.com_kubelet.yaml
monitoring_servicemonitors.monitoring.coreos.com_node-exporter.yaml
```
4. You can filter, modify and reapply the YAML file to the associated cloud native monitoring cluster (do not apply the collection rules that already exist or have the same feature). The cloud native monitoring will automatically perceive these dynamic collection rules and perform collection.
>?If you need to add ServiceMonitor or PodMonitor, you can add it visually on the TKE console, or you can directly create it with YAML. The usage is fully compatible with the CRD of the Prometheus community.



### Migrating the static collection configuration

If the self-built Prometheus system directly uses the Prometheus native configuration file, you can convert it into a RawJob of cloud native monitoring with a few steps on the TKE console, making it compatible with the `scrape_configs` configuration item of the Prometheus native configuration file.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cloud Native Monitoring** in the left sidebar to go to the **Cloud Native Monitoring** page.
3. Click the instance ID/name to configure to go to its basic information page.
4. Select **Associate with Cluster** tab, select the cluster to configure, and click **Data Collection** under the **Operation** column.
![](https://main.qcloudimg.com/raw/9ae5c13778513f783654c3c74b0b8119.png)
5. Select **RawJob** > **Add**. Copy and paste the Job configuration from the native Prometheus configuration file into this configuration window.
![](https://main.qcloudimg.com/raw/05761646fb8a39d7f751bcd435e9c20a.png)
6. You can paste all the Job arrays that need to import into the cloud native monitoring, and click **Confirm**. The Job arrays will be automatically split into multiple RawJobs and named as the `job_name` field of each Job.



### Migrating the global configuration

You can modify the Prometheus CRD resource of cloud native monitoring to modify the global configuration.

1. Run the following command to obtain the Prometheus information.
```bash
$ kubectl get ns
prom-fnc7bvu9     Active   13m
$ kubectl -n prom-fnc7bvu9 get prometheus
NAME               VERSION   REPLICAS   AGE
tke-cls-hha93bp9                        11m
$ kubectl -n prom-fnc7bvu9 edit prometheus tke-cls-hha93bp9
```
2. Run the following command to modify the Prometheus configuration.
```bash
$ kubectl -n prom-fnc7bvu9 edit prometheus tke-cls-hha93bp9
```
 Modify the following parameters in the pop-up window:
 - **scrapeInterval**: the collection capture interval (default value is 15 seconds)
 - **externalLabels**: add the default label tag for all time series data.




### Migrating the aggregation configuration

The format of each Prometheus aggregation configuration rule is the same no matter it is the original static configuration [Recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) or the dynamic configuration [PrometheusRule](https://github.com/prometheus-operator/prometheus-operator/blob/master/Documentation/api.md#prometheusrule).

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cloud Native Monitoring** in the left sidebar to go to the **Cloud Native Monitoring** page.
3. Click the instance ID/name to configure to go to its basic information page.
4. Select **Aggregation Rule** > **Create Aggregation Rule**. In the **Add Aggregation Rule** window, paste each rule into the groups array in the PrometheusRule format, as shown in the figure below:
![](https://main.qcloudimg.com/raw/2b02b2d98eced78e856d320cf5e30a60.png)
>?If the self-built Prometheus uses the aggregation rules defined by PrometheusRule, it is recommended to migrate them according to the above steps. If the PrometheusRule resource is created directly in the cluster using YAML, it cannot be displayed in cloud native monitoring on the console currently.



### Migrating the alarm configuration


This document provides the self-built Prometheus Alarm original configuration YAML file as an example to describe how to convert it into a monitoring configuration similar to cloud native monitoring.[](id:prometheus-native)
```yaml
  - alert: NodeNotReady
    expr: kube_node_status_condition{condition="Ready",status="true"} == 0
    for: 5m
    labels: 
      severity: critical
    annotations: 
      description: node {{ $labels.node }} is not available for a long time (cluster id {{ $labels.cluster }})
```

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cloud Native Monitoring** in the left sidebar to go to the **Cloud Native Monitoring** page.
3. Click the instance ID/name to configure to go to its basic information page.
4. Select **Alarm Configurations** > **Create Alarm Policy** to configure the alarm policy.
![](https://main.qcloudimg.com/raw/2fd94870ef802b5a36f3eb46e81b383b.png)
Main parameters are described as follows:
	-  **PromQL**: the core configuration of the alarm and is the PromQL expression used to indicate the alarm trigger condition, which is equivalent to the “expr” field of the [original configuration](#prometheus-native).
	- **Labels**: an extra label added for the alarm, which is equivalent to the labels field of the [original configuration](#prometheus-native).
	- **Alarm Content**: the pushed alarm content. You can use a template or a template with variables. It is recommended to add the cluster ID in the alarm content. You can use the variable `{{ $labels.cluster }}` to represent the cluster ID.
	- **Duration**: indicates an alarm will be pushed when the alarm is not restored after the alarm condition is met for how long. It is equivalent to the “for” field of the [original configuration](#prometheus-native). The configuration in the following sample is 5 minutes.
	- **Convergence Time**: indicates an alarm will be pushed again when the alarm is not restored after the alarm condition is met for how long, that is, the push interval between the same alarms. It is equivalent to the [repeat_interval](https://prometheus.io/docs/alerting/latest/configuration/#route) configuration of AlertManager. The configuration in the following sample is 1 hour.
>?The above alarm configuration example shows that after the node status changes to NotReady, the alarm will be pushed if it is not restored within 5 minutes. If it has not restored for a long time, the alarm will be pushed again at an interval of 1 hour.
5. Configure the alarm channel. Currently, only Tencent Cloud and WebHook are available.
<dx-tabs>
::: Tencent Cloud alarm channel
The alarm channels of Tencent Cloud support SMS, Email, WeChat and Mobile. You can select as needed.
![](https://main.qcloudimg.com/raw/b2e482036fa9d494286790efad921ddb.png)
:::
::: WebHook alarm channel
If you need to configure other alarm channels, such as DingTalk, Zoom, you can deploy the relevant WebHook backend by yourself, and specify the URL of the WebHook in the cloud native monitoring.
![](https://main.qcloudimg.com/raw/28d3fbf11e528853927629b0370d9774.png)
:::
</dx-tabs>






### Migrating the Grafana dashboard

The self-built Prometheus is usually configured with many custom Grafana monitoring dashboards. If you need to migrate a large number of dashboards to other platforms, it is too inefficient to export and import one by one. You can use the [grafana-backup](https://github.com/ysde/grafana-backup-tool) tool to export and import Grafana dashboards in batches. For details, please refer to the following directions.

1. Run the following command to install grafana-backup, as shown below:
```bash
pip3 install grafana-backup
```
 >?It is recommended to use Python3 to avoid the compatibility problems.
2. Create API Keys.
	1. Enter the configuration page of self-buit Grafana and cloud native monitoring Grafana respectively. Select **API Keys** > **New API Key**, as shown below:
	![](https://main.qcloudimg.com/raw/b4800bdefcb3b644cbe327247c28eff9.png)
	2. In **Add API Key** window, create an API KEY whose role is Admin, as shown below:
	![](https://main.qcloudimg.com/raw/3f9c4e6f40374c47cf9ae0c7b982c1fa.png)
4. Back up the configuration file of the dashboard that you want to export.
	1. Run the following command to obtain the access address of the self-built Grafana, as shown below:
	 ```bash
	 $ kubectl -n  monitoring get svc
	 NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
	 grafana                 ClusterIP   172.21.254.127   <none>        3000/TCP                     25h
	 ```
	 >?Take the Grafana access address `http://172.21.254.127:3000` in the cluster as an example.
	2. Run the following command to generate the grafana-backup configuration file (with Grafana address and APIKey) as shown below:
	```bash
	export TOKEN=<TOKEN>
	cat > ~/.grafana-backup.json <<EOF
	{
	 "general": {
		           "debug": true,
		           "backup_dir": "_OUTPUT_"
	           },
	 "grafana": {
		           "url": "http://172.21.254.127:3000",
		           "token": "${TOKEN}"
	           }
	}
	EOF
	```
	 >? You need to replace &lt;TOKEN> with the APIKey of self-built Grafana, and replace the URL with the actual environment address.
4. Run the following command to export all dashboards, as shown below:
	```bash
	grafana-backup save
	```
	The dashboard will be saved as a compressed file in the `_OUTPUT_` directory. You can run the following command to view the files in this directory, as shown below:
	```bash
	$ tree _OUTPUT_
	_OUTPUT_
	└── 202012151049.tar.gz

	0 directories, 1 file
	```
5. Run the following command to restore the configuration file, as shown below:
```bash
export TOKEN=<TOKEN>
cat > ~/.grafana-backup.json <<EOF
{
  "general": {
        "debug": true,
        "backup_dir": "_OUTPUT_"
       },
  "grafana": {
        "url": "http://prom-xxxxxx-grafana.ccs.tencent-cloud.com",
        "token": "${TOKEN}"
       }
}
EOF
```
 >?You need to replace &lt;TOKEN> with the APIKey of cloud native monitoring Grafana, and replace the URL with the access address of cloud native monitoring Grafana. (The internet access need to be enabled).
6. Run the following command to import the exported dashboards to the cloud native monitoring Grafana with one click, as shown below:
``` bash
grafana-backup restore _OUTPUT_/202012151049.tar.gz
```
7. In Grafana configuration dashboard, select **Dashboard settings** > **Variables** > **New** to create the cluster field. It is recommended to add the filter field “cluster” for all dashboards. Cloud native monitoring supports multiple clusters. It will add the label “cluster” to the data of each cluster, and use the cluster ID to distinguish different clusters, as shown below:
![](https://main.qcloudimg.com/raw/4fc513c387eac66d7e9dbb6d0ee9ad1f.png)
>?Enter an arbitrary metric name that is involved in the current dashboard in label_values (The example is node_uname_info).
8. Modify the query statements of PromQL in all dashboards and add the filter conditions `cluster=~"$cluster"`, as shown below:
![](https://main.qcloudimg.com/raw/2fdd3bb6dfd4e59072c0bb4b41d2e6c5.png)




### Integrating with the existing systems


Cloud native monitoring supports accessing self-built Grafana and AlertManager systems.
<dx-tabs>
::: Accessing self-built Grafana
Cloud native monitoring provides Prometheus API. If you need to use self-built Grafana to display monitoring, you can add cloud native monitoring data as a Prometheus data source to self-built Grafana. You can find the Prometheus API address in the basic information of cloud native monitoring instance on TKE console.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cloud Native Monitoring** in the left sidebar to go to the **Cloud Native Monitoring** page.
3. Click the instance ID/name to go to its details page to obtain the Prometheus API address.
![](https://main.qcloudimg.com/raw/c8e1d55ca0bc4af0fcf5354196a03330.png)
 >?Ensure that the self-built Grafana and cloud native monitoring are in the same VPC or their networks have connected.
4. Add the Prometheus API address in Grafana as the Prometheus data source, as shown below:
![](https://main.qcloudimg.com/raw/b6a14e36f3325034e2b84c63f605eaec.png)
:::
::: Accessing self-built AlertManager
If you have more complex alarm requirements or want to use the self-built AlertManager for unified alarms, you can access the cloud-native monitoring alarms to the self-built AlertManager. You only need to enter the address of the self-built AlertManager in the advanced settings when [creating a monitoring instance](https://intl .cloud.tencent.com/document/product/457/38824), as shown in the figure below:
![](https://main.qcloudimg.com/raw/8b5673273cc197e8f9cf141c243b9ea8.png)
:::
</dx-tabs>


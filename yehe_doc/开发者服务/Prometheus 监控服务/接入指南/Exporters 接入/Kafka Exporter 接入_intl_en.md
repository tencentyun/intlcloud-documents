## Overview

When using Kafka, you need to monitor its running status, such as cluster status and message heap. TMP provides an exporter to monitor Kafka and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to deploy the Kafka exporter and integrate it with the alert feature.



>?For easier export installation and management, we recommend you use [TKE](https://intl.cloud.tencent.com/zh/document/product/457) for unified management.

## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance and created a [namespace](https://intl.cloud.tencent.com/document/product/1051/35487) for the cluster.
- You have located and integrated the target TKE cluster in the **Integrate with TKE** section of the **target TMP instance** in the **[TMP console](https://console.cloud.tencent.com/monitor/prometheus)**. For more information, please see Agent Management.


## Directions

### Deploying exporter


1. Log in to the [TKE](https://console.cloud.tencent.com/tke2/cluster) console.
2. Click the ID/name of the cluster whose access credential you want to get to enter the cluster management page.
3. On the left sidebar, select **Workload** > **Deployment** to enter the **Deployment** page.
4. On the Deployment management page, click **Create** and select the target **namespace** to deploy the service. You can create in the console. Here, YAML is used to deploy the exporter. Below is a sample YAML configuration:

<dx-codeblock>
:::  yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: kafka-exporter # Rename the exporter based on the business needs. We recommend you add the Kafka instance information
  name: kafak-exporter # Rename the exporter based on the business needs. We recommend you add the Kafka instance information
  namespace: kafka-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: kafka-exporter # Rename the exporter based on the business needs. We recommend you add the Kafka instance information
  template:
    metadata:
      labels:
        k8s-app: kafka-exporter # Rename the exporter based on the business needs. We recommend you add the Kafka instance information
    spec:
      containers:
      - args:
        - --kafka.server=x.x.x.x:9092 # Corresponding Kafka instance address information
        image: danielqsj/kafka-exporter:latest
        imagePullPolicy: IfNotPresent
        name: kafka-exporter
        ports:
        - containerPort: 9121
          name: metric-port  # This name is required during scrape task configuration
        securityContext:
          privileged: false
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      imagePullSecrets:
      - name: qcloudregistrykey
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
:::
</dx-codeblock>

>?For detailed exporter parameters, please see [kafka_exporter](https://github.com/danielqsj/kafka_exporter).


### Adding scrape task

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click a **cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.
3. In **Scrape Configuration**, add `Pod Monitor` to define a Prometheus scrape task. Below is a sample YAML configuration:

<dx-codeblock>
:::  yaml
  apiVersion: monitoring.coreos.com/v1
  kind: PodMonitor
  metadata:
    name: kafka-exporter  # Enter a unique name
    namespace: cm-prometheus  # The namespace is fixed. Do not change it
  spec:
    podMetricsEndpoints:
    - interval: 30s
      port: metric-port # Enter the name of the corresponding port of the Prometheus exporter in the Pod YAML configuration file
      path: /metrics # Enter the value of the corresponding path of the Prometheus exporter. If it is not specified, it will be `/metrics` by default
      relabelings:
      - action: replace
        sourceLabels:
        - instance
        regex: (.*)
        targetLabel: instance
        replacement: 'ckafka-xxxxxx' # Change it to the corresponding Kafka instance ID
      - action: replace
        sourceLabels:
        - instance
        regex: (.*)
        targetLabel: ip
        replacement: '1.x.x.x' # Change it to the corresponding Kafka instance IP
        namespaceSelector:
      matchNames:
      - kafka-demo
        selector:  # Enter the label value of the Pod to be monitored to locate the target Pod
      matchLabels:
        k8s-app: kafka-exporter
:::
</dx-codeblock>

>?As the exporter and Kafka are deployed on different servers, we recommend you use the Prometheus relabeling mechanism to add the Kafka instance information to the monitoring metrics so as to locate problems more easily.

### Viewing monitoring information

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Integration Center** to enter the **Integration Center** page. Find Kafka monitoring, install the corresponding Grafana dashboard, and then you can enable the Kafka monitoring dashboard to view instance monitoring data as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/22344bae1e3455f0d201a960acca5836.png)


### Integrating with alert feature

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Alerting Rule** and add the corresponding alerting rules. For more information, please see Creating Alerting Rule.

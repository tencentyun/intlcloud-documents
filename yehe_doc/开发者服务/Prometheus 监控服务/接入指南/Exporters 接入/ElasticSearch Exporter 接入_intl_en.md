## Overview

When using Elasticsearch, you need to monitor its running status, such as cluster and index status. TMP provides an exporter to monitor Elasticsearch and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to deploy the Elasticsearch exporter and integrate it with the alert feature.



>?For easier export installation and management, we recommend you use [TKE](https://intl.cloud.tencent.com/zh/document/product/457) for unified management.

## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance and created a [namespace](https://intl.cloud.tencent.com/document/product/1051/35487) for the cluster.
- You have located and integrated the target TKE cluster in the **Integrate with TKE** section of the **target TMP instance** in the **[TMP console](https://console.cloud.tencent.com/monitor/prometheus)**. For more information, please see Agent Management.


## Directions

### Deploying exporter



1. Log in to the [TKE](https://console.cloud.tencent.com/tke2/cluster) console.
2. Click the ID/name of the cluster whose access credential you want to get to enter the cluster management page.
3. Perform the following steps to deploy an exporter: [Using Secret to manage Elasticsearch connection string](#step1) > [Deploying Elasticsearch exporter](#step2) > [Verifying](#step3).

[](id:step1)

#### Using Secret to manage Elasticsearch connection string

1. On the left sidebar, select **Workload** > **Deployment** to enter the **Deployment** page.
2. In the top-right corner of the page, click **Create via YAML** to create a YAML configuration as detailed below:
   You can use Kubernetes Secrets to manage and encrypt passwords. When starting the Elasticsearch exporter, you can directly use the Secret key but need to adjust the corresponding URI. Below is a sample YAML configuration:
	
## Overview

When using Elasticsearch, you need to monitor its running status, such as cluster and index status. TMP provides an exporter to monitor Elasticsearch and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to deploy the Elasticsearch exporter and integrate it with the alert feature.



>?For easier export installation and management, we recommend you use [TKE](https://intl.cloud.tencent.com/zh/document/product/457) for unified management.

## Prerequisites

- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance and created a [namespace](https://intl.cloud.tencent.com/document/product/1051/35487) for the cluster.
- You have located and integrated the target TKE cluster in the **Integrate with TKE** section of the **target TMP instance** in the **[TMP console](https://console.cloud.tencent.com/monitor/prometheus)**. For more information, please see Agent Management.


## Directions

### Deploying exporter



1. Log in to the [TKE](https://console.cloud.tencent.com/tke2/cluster) console.
2. Click the ID/name of the cluster whose access credential you want to get to enter the cluster management page.
3. Perform the following steps to deploy an exporter: [Using Secret to manage Elasticsearch connection string](#step1) > [Deploying Elasticsearch exporter](#step2) > [Verifying](#step3).

[](id:step1)

#### Using Secret to manage Elasticsearch connection string[](id:step1)

1. On the left sidebar, select **Workload** > **Deployment** to enter the **Deployment** page.
2. In the top-right corner of the page, click **Create via YAML** to create a YAML configuration as detailed below:
   You can use Kubernetes Secrets to manage and encrypt passwords. When starting the Elasticsearch exporter, you can directly use the Secret key but need to adjust the corresponding URI. Below is a sample YAML configuration:
	

<dx-codeblock>
:::  yaml
apiVersion: v1
kind: Secret
metadata:
  name: es-secret-test
  namespace: es-demo 
type: Opaque
stringData:
  esURI: you-guess  # Corresponding Elasticsearch URI
:::
</dx-codeblock>

>?The Elasticsearch connection string is in the format of `<proto>://<user>:<password>@<host>:<port>`, such as `http://admin:pass@localhost:9200`.

[](id:step2)

#### Deploying Elasticsearch exporter[](id:step2)

On the Deployment management page, click **Create** and select the target **namespace** to deploy the service. You can create in the console. Here, YAML is used to deploy the exporter. Below is a sample YAML configuration:

<dx-codeblock>
:::  yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: es-exporter
  name: es-exporter
  namespace: es-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: es-exporter
  template:
    metadata:
      labels:
        k8s-app: es-exporter
    spec:
      containers:
      - env:
          - name: ES_URI
            valueFrom:
              secretKeyRef:
                name: es-secret-test
                key: esURI
          - name: ES_ALL
            value: "true"
        image: bitnami/elasticsearch-exporter:latest
        imagePullPolicy: IfNotPresent
        name: es-exporter
        ports:
        - containerPort: 9114
          name: metric-port
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

>?The above sample uses `ES_ALL` to collect all monitoring metrics of Elasticsearch, which can be adjusted through the corresponding parameters. For detailed exporter parameters, please see [elasticsearch_exporter](https://github.com/justwatchcom/elasticsearch_exporter).

[](id:step3)

#### Verifying[](id:step3)


1. Click the newly created Deployment on the **Deployment** page to enter the Deployment management page.
2. Click the **Log** tab, and you can see that the exporter is successfully started and its address is exposed as shown below:
    ![](https://qcloudimg.tencent-cloud.cn/raw/164a0ccb4b0066cfc3c6df3ffa4947b8.png)
3. Click the **Pod Management** tab to enter the Pod page.
4. In the **Operations** column on the right, click **Remote Login** to log in to the Pod. Run the following `curl` command with the address exposed by the exporter in the command line window, and you can get the corresponding Elasticsearch metrics normally. If no corresponding data is returned, please check whether the **connection string** is correct as shown below:
```
curl localhost:9114/metrics
```
The execution result is as shown below:
![](https://main.qcloudimg.com/raw/0c919a2bee21aa48f117960dc696f6e2.png)




### Adding scrape task

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click a **cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.
3. In **Scrape Configuration**, add `Pod Monitor` to define a Prometheus scrape task. Below is a sample YAML configuration:

<dx-codeblock>
:::  yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: es-exporter
  namespace: cm-prometheus
spec:
  namespaceSelector:
    matchNames:
      - es-demo
  podMetricsEndpoints:
  - interval: 30s
    path: /metrics
    port: metric-port
    selector:
    matchLabels:
    k8s-app: es-exporter
    :::
    </dx-codeblock>

### Viewing monitoring information

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Integration Center** to enter the **Integration Center** page. Find Elasticsearch monitoring, install the corresponding Grafana dashboard, and then you can enable the Elasticsearch monitoring dashboard to view instance monitoring data as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5823c806f20039bb59024c5958449f1b.png)


### Integrating with alert feature

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Alerting Rule** and add the corresponding alerting rules. For more information, please see Creating Alerting Rule.

## Overview

When using Redis, you need to monitor its running status to know whether it runs normally and troubleshoot its faults. TMP provides an exporter to monitor Redis and offers an out-of-the-box Grafana monitoring dashboard for it. This document describes how to use TMP to monitor Redis.

>?For easier export installation and management, we recommend you use [TKE](https://intl.cloud.tencent.com/zh/document/product/457) for unified management.




## Prerequisites


- You have created a [TKE cluster](https://intl.cloud.tencent.com/document/product/457/30637) in the region and VPC of your TMP instance and created a [namespace](https://intl.cloud.tencent.com/document/product/1051/35487) for the cluster.
- You have located and integrated the target TKE cluster in the **Integrate with TKE** section of the **target TMP instance** in the **[TMP console](https://console.cloud.tencent.com/monitor/prometheus)**. For more information, please see Agent Management.



## Directions

### Deploying exporter


1. Log in to the [TKE](https://console.cloud.tencent.com/tke2/cluster) console.
2. Click the ID/name of the cluster whose access credential you want to get to enter the cluster management page.
3. Perform the following steps to deploy an exporter: [Using Secret to manage Redis password](#step1) > [Deploying Redis exporter](#step2) > [Verifying](#step3).



#### Using Secret to manage Redis password[](id:step1)

1. On the left sidebar, select **Workload** > **Deployment** to enter the **Deployment** page.
2. In the top-right corner of the page, click **Create via YAML** to create a YAML configuration as detailed below:
You can use Kubernetes Secrets to manage and encrypt passwords. When starting the Redis exporter, you can directly use the Secret key but need to adjust the corresponding `password`. Below is a sample YAML configuration:
<dx-codeblock>
:::  yaml
apiVersion: v1
kind: Secret
metadata:
    name: redis-secret-test
    namespace: redis-test
type: Opaque
stringData:
    password: you-guess  # Corresponding Redis password
:::
</dx-codeblock>

#### Deploying Redis exporter[](id:step2)

On the Deployment management page, click **Create** and select the target **namespace** to deploy the service. You can create in the console. Here, YAML is used to deploy the exporter. Below is a sample YAML configuration:
>?For more information on the detailed exporter parameters, please see [redis_exporter](https://github.com/oliver006/redis_exporter).

<dx-codeblock>
:::  yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: redis-exporter # Rename the exporter based on the business needs. We recommend you add the Redis instance information
  name: redis-exporter # Rename the exporter based on the business needs. We recommend you add the Redis instance information
  namespace: redis-test
spec:
  replicas: 1
  selector:
    matchLabels:
      k8s-app: redis-exporter # Rename the exporter based on the business needs. We recommend you add the Redis instance information
  template:
    metadata:
      labels:
        k8s-app: redis-exporter # Rename the exporter based on the business needs. We recommend you add the Redis instance information
    spec:
      containers:
      - env:
        - name: REDIS_ADDR
          value: ip:port # `ip:port` of the corresponding Redis instance
        - name: REDIS_PASSWORD
          valueFrom:
            secretKeyRef:
              name: redis-secret-test
              key: password
        image: ccr.ccs.tencentyun.com/redis-operator/redis-exporter:1.12.0
        imagePullPolicy: IfNotPresent
        name: redis-exporter
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



#### Verifying[](id:step3)

1. Click the newly created Deployment on the **Deployment** page to enter the Deployment management page.
2. Click the **Log** tab, and you can see that the exporter is successfully started and its address is exposed as shown below:
	 ![](https://qcloudimg.tencent-cloud.cn/raw/7e71550de4d3f7ca78b4d97a3b2021f9.png)
3. Click the **Pod Management** tab to enter the Pod page.
4. In the **Operations** column on the right, click **Remote Login** to log in to the Pod. Run the following `curl` command with the address exposed by the exporter in the command line window, and you can get the corresponding Redis metrics normally. If no corresponding data is returned, please check whether `REDIS_ADDR` and `REDIS_PASSWORD` are correct as shown below:
```
curl localhost:9121/metrics
```
	The command execution result is as shown below:
	![](https://main.qcloudimg.com/raw/bbac65ba711420fdb81d11cf6c4a3cdb.png)




### Adding scrape task

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click a **cluster ID** in the TKE cluster list to enter the **Integrate with TKE** page.
3. In **Scrape Configuration**, add `Pod Monitor` to define a Prometheus scrape task. Below is a sample YAML configuration:

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

>?As the exporter and Redis are deployed on different servers, we recommend you use the Prometheus relabeling mechanism to add the Redis instance information to the monitoring metrics so as to locate problems more easily.



### Viewing monitoring information


1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Integration Center** to enter the **Integration Center** page. Find Redis monitoring, install the corresponding Grafana dashboard, and then you can enable the Redis monitoring dashboard to view instance monitoring data as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d2eb8e029ac10dcf8599166ea1d00dce.png)

### Integrating with alert feature

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus) and select the target TMP instance to enter the management page.
2. Click **Alerting Rule** and add the corresponding alerting rules. For more information, please see Creating Alerting Rule.

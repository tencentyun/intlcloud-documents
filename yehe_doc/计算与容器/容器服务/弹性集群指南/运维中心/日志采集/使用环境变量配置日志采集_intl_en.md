## Overview
In EKS, you can use environment variables to configure log collection, and collect logs by line without parsing, or use [custom resource definitions (CRD) to configure log collection](https://intl.cloud.tencent.com/document/product/457/40585).

This document describes how to use the environment variables to configure the log collection feature of the EKS cluster, and to send the logs of services within the cluster to [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/product/cls) or external Kafka. This feature is suitable for users who need to store and analyze service logs in EKS clusters.

To use the EKS log collection feature, you need to manually enable it for each elastic cluster when creating a workload. You can enable this feature by performing the following operations:
- [Configuring log collection via the console](#output)
- [Configuring log collection via yaml](#yaml)
- [Updating log collection](#new)


#### Notes
After the EKS log collection feature is enabled, the log collection agent will send the collected logs in JSON format to the consumer end that you have specified based on your configuration of the collection path and log consumer end. The details of the collection path and consumer end are as follows:
  - **Consumer end**: the log collection service allows you to set Kafka or CLS as the log consumer end.
  - **Collection path**: the path of the logs to collect. The collection path supports collection standard output (stdout) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”. 

## Prerequisites

- Confirm that the Kubernetes cluster can access the log consumer end.
- The length of a log is limited to 2 M. The log is truncated if this limit is exceeded.
  <dx-alert infotype="notice" title="">
If the log output rate is high, you need to adjust this parameter configuration to avoid OOM. For more information, see [How to adjust the log collection configuration to adapt to different log output rates](https://intl.cloud.tencent.com/document/product/457/40587).
</dx-alert>




## Directions

[](id:output)

### Configuring log collection via the console

The EKS log collection feature collects the log information and outputs it to the specified consumer end in JSON format with Kubernetes metadata attached, including the label of the Pod to which the container belongs, annotation, etc. The specific directions are as follows:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Elastic Cluster** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the desired cluster for log collection to enter the cluster management page.
3. Select a workload type in **Workload** on the left to go to the corresponding page, and then click **Create**.
4. In **Containers in the Pod** section, select **Advanced Settings**, and check **Activate** to enable log collection, as shown in the figure below:
![](https://main.qcloudimg.com/raw/2359897f61c9c663d31db1cdca03f3c4.png)
5. Refer to the following information to configure the log consumer end. You can choose CLS or Kafka as the log consume end.
<dx-tabs>
::: Configuring\sCLS\sas\sthe\slog\sconsumer\send
1. Select **CLS** as the **Consumer End**, and select the **Log set** and **Log topic**, as shown below:
![](https://main.qcloudimg.com/raw/37623ea379501b3b431fac609b9681c0.png)
If there is no suitable log set, you can [create a logset and a log topic](https://intl.cloud.tencent.com/document/product/614/31592).
<dx-alert infotype="notice" title="">
CLS currently only supports log collection and reporting for intra-region container clusters.
</dx-alert>
2. Enable the **log index** for the selected log topic. Index configuration is required for CLS log search and analysis. If it is not enabled, you cannot view the logs. For how to configure index, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).
You can go to the **[CLS console](https://console.cloud.tencent.com/cls/topic?region=ap-guangzhou)** > **Log Topic** page, select a log topic name, and enable the index in the **Index Configuration** tab, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a6f481ce07cafd4ecb8d13ac05950b99.png)

:::
::: Configuring\sKafka\sas\sthe\slog\sconsumer\send
If you select Kafka as the consumer end, it is recommended you to use CKafka. The experience of its consumption and production modes are the same as the native version, and it supports alarm configurations.
Specify the Broker address and Topic of Kafka in the container configuration, and ensure that all resources in the cluster can access the user-specified Kafka Topic, as shown in the figure below:
![](https://main.qcloudimg.com/raw/27e5173a642dfd0e2c84c93c0b319bcc.png)
<dx-alert infotype="notice" title="">
You need to select “delete” for `cleanup.policy` in Kafka Topic configuration. If you select “compact”, CLS will fail to report to Kafka, resulting in data loss, as shown in the figure below:
![](https://main.qcloudimg.com/raw/01e49f01c82fd0cf13229fbade701641.png)
</dx-alert>
:::
</dx-tabs>

6. Select **Role** or **Key** to authorize.
>! 
> - You can only select the same authorization method for the containers in the same Pod. The last modification shall prevail. For example, if you select key authorization for the first container and role authorization for the second container, finally both containers will adopt role authorization.
> - You can only select the same role to authorize for the containers in the same Pod.

<dx-tabs>
::: Role\sauthorization
 - Select a role that can access CLS, as shown in the figure below:
![](https://main.qcloudimg.com/raw/890940885a3fd7502cf28aa62f970e2c.png)
 - If there is no suitable role, you can create one as follows:
  1. Log in to the CAM console, and select **[Roles]**(https://console.cloud.tencent.com/cam/role) in the left sidebar.
  2. On the **Roles** page, click **Create Role**.
  3. In the “Select role entity” window that appears, select **Tencent Cloud Product Service** to go to the **Create Custom Role** page.
  4. On the **Enter role entity info** tab, select **Cloud Virtual Machine (cvm)** and click **Next**.

    <dx-alert infotype="notice" title="">
You must select **Cloud Virtual Machine (cvm)** rather than TKE as the role entity, otherwise, you cannot complete the authorization process.
    </dx-alert>
  5. On the **Configure role policy** tab, select **QcloudCLSAccessForApiGateWayRole** policy and click **Next**.
  6. On the **Review** tab, enter the role name to review the role information, and then click **Done**. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).
:::
::: Key\sauthorization
- Select the “SecretId” and “SecretKey” of your account API key as the variable values to create the cluster Secret.
![](https://main.qcloudimg.com/raw/c03d348d34fc5c5d2666b1e883138bab.png)
- If there is no suitable Secret, you need to create one. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676). You can view the SecretId and SecretKey in [API Keys](https://console.cloud.tencent.com/cam/capi).
<dx-alert infotype="notice"> The user corresponding to the API key must have the permission to access the CLS. If there is no API key, you need to create one. For more information, see [Access Key](https://intl.cloud.tencent.com/document/product/598/34228).
</dx-alert>
:::
</dx-tabs>

7. Configure the collection path, as shown in the figure below:
![](https://main.qcloudimg.com/raw/4f9fb3635b7a3c3ab35e8387d877a08b.png)
At this point, you have configured the log collection feature. You can set other configurations of the workload as needed.



[](id:yaml)
### Configuring log collection via yaml [](id:yaml)
This document provides three collection methods for your choice: collecting logs to Kafka, collecting logs to CLS via a secret and collecting logs to CLS via a role.
>! If both key and role authorization are configured in yaml, Pod actually uses role authorization.

<dx-tabs>
::: Collecting\slogs\sto\sKafka
Enable log collection by adding environment variables.
```shell
apiVersion: apps/v1beta2
kind: Deployment
metadata:
   annotations:
     deployment.kubernetes.io/revision: "1"
labels:
     k8s-app: kafka
     qcloud-app: kafka
   name: kafka
   namespace: default
spec:
   replicas: 1
   selector:
     matchLabels:
       k8s-app: kafka
       qcloud-app: kafka
  template:
metadata:
       annotations:
         eks.tke.cloud.tencent.com/cpu: "0.25"
         eks.tke.cloud.tencent.com/mem: "0.5Gi"
labels:
         k8s-app: kafka
         qcloud-app: kafka
     spec:
       containers:
       - env:
         - name: EKS_LOGS_OUTPUT_TYPE
           value: kafka
         - name: EKS_LOGS_KAFKA_BROKERS
           value: 10.0.16.42:9092
         - name: EKS_LOGS_KAFKA_TOPIC
           value: eks
		    - name: EKS_LOGS_KAFKA_MESSAGE_KEY # Optional
           valueFrom:
              fieldRef:
                fieldPath: metadata.name
         - name: EKS_LOGS_METADATA_ON
           value: "true"
         - name: EKS_LOGS_LOG_PATHS
           value: stdout,/tmp/busy*.log
         image: busybox:latest
         command: ["/bin/sh"]
         args: ["-c", "while true; do echo hello world; date; echo hello >> /tmp/busy.log; sleep 1; done"]
         imagePullPolicy: Always
         name: while
         resources:
           requests:
             cpu: 250m
             memory: 512Mi
```
**Field description:**
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer end can be kafka or CLS. The key indicates whether log collection is enabled.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: `true` or `false`. Default value: `true`.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_KAFKA_TOPIC</td> <td>Log topic</td>
	</tr>
	<tr>
		<td>EKS_LOGS_KAFKA_BROKERS</td> <td>kafka brokers: ip1:port1, ip1:port2, and ip2:port2 formats, separated by “,”. Use this environmental variable for external application. EKS_LOGS_KAFKA_HOST will no longer be visible to external users.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_KAFKA_MESSAGE_KEY</td> <td>Optional. A key can be specified to deliver the log to the specified partition. <li>If the delivery by key is not enabled, logs will be randomly delivered to different partitions. </li><li>If the delivery by key is enabled, logs with the same key will be delivered to the same partition.</li>
<b>Note</b>: here the key gets the variable value from the field of the Pod. The above examples all take the Pod name as an example, and it also supports namespace, PodIP, etc. For more information, see <a href="https://kubernetes.io/zh/docs/tasks/inject-data-application/environment-variable-expose-pod-information/">Kubernetes Documentation</a>.</td>
	</tr>
</table>


:::


::: Collecting\slogs\sto\sCLS\svia\sa\ssecret
#### Creating a secret[](id:z)
<dx-alert infotype="notice">The following sample is to manually create a secret through yaml. If you create a secret through the console, you do not need to perform 64 encoding. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676).
</dx-alert>
Run the following command via kubectl to obtain the secretid and secretkey for base64 encoding. Replace secretid and secretkey with the actual secretid and secretkey that you use. For more information, see [API Keys](https://console.cloud.tencent.com/cam/capi).
```shell
$ echo -n 'secretid' | base64
c2VjcmV0aWQ=
$ echo -n 'secretkey' | base64
c2VjcmV0a2V5
```
Manually create a secret via yaml. Specify secretid and secretkey based on the values obtained in the step of [Creating a secret](#z).
```shell
apiVersion: v1
kind: Secret
metadata:
   name: secretidkey
data:
   secretid: 
   secretkey: 
```

#### Creating a deployment
Enable log collection by adding environment variables.
```shell
apiVersion: apps/v1beta2
kind: Deployment
metadata:
   annotations:
     deployment.kubernetes.io/revision: "1"
   labels:
     k8s-app: cls
     qcloud-app: cls
   name: cls
   namespace: default
spec:
   replicas: 1
   selector:
     matchLabels:
       k8s-app: cls
       qcloud-app: cls
   template:
     metadata:
       annotations:
         eks.tke.cloud.tencent.com/cpu: "0.25"
         eks.tke.cloud.tencent.com/mem: "0.5Gi"
       labels:
         k8s-app: cls
         qcloud-app: cls
     spec:
       containers:
       - env:
         - name: EKS_LOGS_OUTPUT_TYPE
           value: cls
         - name: EKS_LOGS_LOGSET_NAME
           value: eks
         - name: EKS_LOGS_TOPIC_ID
           value: 617c8270-e8c8-46e2-a90b-d94c4bebe519
         - name: EKS_LOGS_SECRET_ID
           valueFrom:
             secretKeyRef:
               name: secretidkey
               key: secretid
         - name: EKS_LOGS_SECRET_KEY
           valueFrom:
             secretKeyRef:
               name: secretidkey
               key: secretkey
         - name: EKS_LOGS_LOG_PATHS
           value: stdout,/tmp/busy*.log
         - name: EKS_LOGS_METADATA_ON
           value: "true"
         image: busybox:latest
         command: ["/bin/sh"]
         args: ["-c", "while true; do echo hello world; date; echo hello >> /tmp/busy.log; sleep 1; done"]
         imagePullPolicy: Always
         name: hello
       - env:
         - name: EKS_LOGS_OUTPUT_TYPE
           value: cls
         - name: EKS_LOGS_LOGSET_NAME
           value: eks
         - name: EKS_LOGS_TOPIC_ID
           value: 617c8270-e8c8-46e2-a90b-d94c4bebe519
         - name: EKS_LOGS_SECRET_ID
           valueFrom:
             secretKeyRef:
               name: secretidkey
               key: secretid
         - name: EKS_LOGS_SECRET_KEY
           valueFrom:
             secretKeyRef:
               name: secretidkey
               key: secretkey
         - name: EKS_LOGS_LOG_PATHS
           value: stdout,/tmp/busy*.log
         - name: EKS_LOGS_METADATA_ON
           value: "true"
         image: busybox:latest
         command: ["/bin/sh"]
         args: ["-c", "while true; do echo hello world; date; echo hello >> /tmp/busy.log; sleep 1; done"]
         imagePullPolicy: Always
         name:world
```

**Field description:**
<table>
<tr>
<th>Field Name</th> <th>Description</th>
</tr>
<tr>
<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer end can be kafka or CLS. The key indicates whether log collection is enabled.</td>
</tr>
<tr>
<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td></tr>
<tr>
<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: `true` or `false`. Default value: `true`.</td>
</tr>
<tr>
<td>EKS_LOGS_LOGSET_NAME</td> <td>CLS logset name</td>
</tr>
<tr>
	<td>EKS_LOGS_TOPIC_ID</td> <td>CLS logset topic ID</td>
</tr>
</tr>
<td>EKS_LOGS_SECRET_ID</td> <td>SecretId</td>
</tr>
<tr>
<td>EKS_LOGS_SECRET_KEY</td> <td>SecretKey</td>
</tr>
</tr>
</table>

:::



::: Collecting\slogs\sto\sCLS\svia\sa\srole
#### Creating a role  
Create a role on the [CAM console](https://console.cloud.tencent.com/cam/role). While creating a role, you need to select **Tencent Cloud Product Service**, bind the role with a **CVM**, and select **QcloudCLSAccessForApiGateWayRole** policy. For more information, see [Creating Roles](https://intl.cloud.tencent.com/document/product/598/19381).
In the Pod template, add annotation, specify the role name, and obtain the permission policy contained in the role.
```shell
template:
   metadata:
     annotations:
       eks.tke.cloud.tencent.com/role-name: "eks-pushlog"
```
#### Creating a deployment
```shell
apiVersion: apps/v1beta2
kind: Deployment
metadata:
   annotations:
     deployment.kubernetes.io/revision: "1"
   labels:
     k8s-app: cls
     qcloud-app: cls
   name: cls
   namespace: default
spec:
   replicas: 1
   selector:
     matchLabels:
       k8s-app: cls
       qcloud-app: cls
   template:
     metadata:
       annotations:
         eks.tke.cloud.tencent.com/cpu: "0.25"
         eks.tke.cloud.tencent.com/mem: "0.5Gi"
         eks.tke.cloud.tencent.com/role-name: "eks-pushlog"
       labels:
         k8s-app: cls
         qcloud-app: cls
     spec:
       containers:
       - env:
         - name: EKS_LOGS_OUTPUT_TYPE
           value: cls
         - name: EKS_LOGS_LOGSET_NAME
           value: eks
         - name: EKS_LOGS_TOPIC_ID
           value: 617c8270-e8c8-46e2-a90b-d94c4bebe519
         - name: EKS_LOGS_LOG_PATHS
           value: stdout,/tmp/busy*.log
         - name: EKS_LOGS_METADATA_ON
           value: "true"
         image: busybox:latest
         command: ["/bin/sh"]
         args: ["-c", "while true; do echo hello world; date; echo hello >> /tmp/busy.log; sleep 1; done"]
         imagePullPolicy: Always
         name: hello
       - env:
         - name: EKS_LOGS_OUTPUT_TYPE
           value: cls
         - name: EKS_LOGS_LOGSET_NAME
           value: eks
         - name: EKS_LOGS_TOPIC_ID
           value: 617c8270-e8c8-46e2-a90b-d94c4bebe519
         - name: EKS_LOGS_LOG_PATHS
           value: stdout,/tmp/busy*.log
         - name: EKS_LOGS_METADATA_ON
           value: "true"
         image: busybox:latest
         command: ["/bin/sh"]
         args: ["-c", "while true; do echo hello world; date; echo hello >> /tmp/busy.log; sleep 1; done"]
         imagePullPolicy: Always
         name: world
```
**Field description:**
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer end can be kafka or CLS. The key indicates whether log collection is enabled.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: `true` or `false`. Default value: `true`.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_LOGSET_NAME</td> <td>CLS logset name</td>
	</tr>
	<tr>
		<td>EKS_LOGS_TOPIC_ID</td> <td>CLS logset topic ID</td>
	</tr>
	</tr>
</table>
:::
</dx-tabs>



### Updating the log collection [](id:new)
You can update log collection via the console and yaml. Please refer to the following directions:



<dx-tabs>
::: Updating\slog\scollection\svia\sthe\sconsole
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Elastic Cluster** in the left sidebar.
2. Select the ID of the desired cluster for log collection configuration to enter the cluster management page.
3. Choose **Workload** on the left, find the row of the desired workload for which you want to update log collection, and click **Update Pod Configuration** > **Advanced Settings** on the right to modify configurations, as shown in the figure below:
![](https://main.qcloudimg.com/raw/6e82866759f9704fd49d7695f57dfa47.png)
4. Click **Done**.

:::

::: Updating\slog\scollection\svia\syaml
Find the yaml corresponding to the workload for which you want to update log collection. Then modify the corresponding variable values based on the relevant variable name changes of the configuration. You can view the meanings of variable names in [Configuring log collection](#yaml).
:::
</dx-tabs>

## FAQ
If you have problems, you can refer to [EKS Log Collection FAQs](https://intl.cloud.tencent.com/document/product/457/40582). If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.

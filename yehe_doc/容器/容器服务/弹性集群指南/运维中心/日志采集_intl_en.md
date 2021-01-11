## Overview
The EKS log collection feature can send the logs of services within a cluster to [CLS](https://intl.cloud.tencent.com/product/cls), [CKafka](https://intl.cloud.tencent.com/product/ckafka), or self-built Kafka. This feature is suitable for users who need to store and analyze service logs in EKS clusters. This document describes how to use the cluster log collection feature provided by EKS.


To use the EKS log collection feature, you need to manually enable it for each elastic cluster when creating a workload. You can enable the EKS log collection feature by performing the following operations:
  - [Configuring log collection](#output)
  - [Configuring the log consumer](#output2)
  - [Configuring log collection via yaml](#yaml)
  - [Updating log collection](#new)

## Notes
After the EKS log collection feature is enabled, the log collection agent will send the collected logs in JSON format to the consumer that you have specified based on your configuration of the collection path and log consumer. The details of the collection path and consumer are as follows:
  - **Consumer**: the log collection service allows you to set Kafka or CLS as the log consumer.
  - **Collection path**: the path of the logs to collect. The collection path supports collection standard output (stdout) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”. 

## Prerequisites

- Confirm that the Kubernetes cluster can access the log consumer.
- The maximum log length is 512 K for a log. The log is truncated if this limit is exceeded.


## Directions


### Configuring log collection
The EKS log collection feature collects the log information and outputs it to the specified consumer in JSON format with Kubernetes metadata attached, including the label of the pod to which the container belongs, annotation, etc. The specific directions are as follows:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Elastic Cluster** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the desired cluster for log collection to enter the cluster management page.
3. Select a workload type in "Workload" on the left to go to the corresponding page, and then click **Create**.
4. In **Containers in the pod** section, select **Advanced Settings**, and check **Activate** to enable log collection, as shown in the figure below:
![](https://main.qcloudimg.com/raw/0ef3ce835e4d30651a48f54df9b23acb.png)
5. Refer to the following information to configure the log consumer. You can choose CLS or Kafka as the log consumer, as shown in the figure below:
  - We recommend that you choose [CLS](https://cloud.tencent.com/product/cls) as the consumer and select logsets and log topics. If there is no suitable logset, refer to [Configuring CLS as the log consumer](#output2).
   - If you choose Kafka as the consumer, refer to [Configuring Kafka as the log consumer](#output2).
![](https://main.qcloudimg.com/raw/4a0e6bef8d5b0c800dfdb6de9104fe4c.png)
6. Select **Role** or **Key** to authorize.
>! 
>- You can only select the same authorization method for the containers in the same pod. The last modification shall prevail. For example, if you select key authorization for the first container and role authorization for the second container, finally both containers will be role authorization.
>- You can only select the same role to authorize for the containers in the same pod.

<dx-tabs>
::: Role authorization
 - Select a role that can access CLS service, as shown in the figure below:
![](https://main.qcloudimg.com/raw/eb325a52c59486e1051a381ee8ae135d.png)
 - If there is no suitable role, you can create a role as follows:
  1. Log in to the CAM console, and select **[Roles]**(https://console.cloud.tencent.com/cam/role) in the left sidebar.
  2. On the **Roles** page, click **Create Role**.
  3. In the pop-up window, select **Tencent Cloud Product Service** to go to the **Create Custom Role** page.
  4. On the **Enter role entity info** tab, select **Cloud Virtual Machine (cvm)** and click **Next**.
  5. On the **Configure role policy** tab, select **QcloudCLSAccessForApiGateWayRole** policy and click **Next**.
  6. On the **Review** tab, enter the role name to review the role information, and then click **Done**. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).
:::
::: Key authorization
- Select the “SecretId” and “SecretKey” of your account API key as the variable values to create the cluster Secret.
![](https://main.qcloudimg.com/raw/90103c9759c3e2df9bd6f66a507e60fb.png)
- If there is no suitable Secret, you need to create a Secret. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676). You can view the SecretId and SecretKey in [API Keys](https://console.cloud.tencent.com/cam/capi).
>! The user corresponding to the API key must have the permission to access the CLS. If there is no API key, you need to create a new one. For more information, see [Access Key](https://intl.cloud.tencent.com/document/product/598/34227).
:::
</dx-tabs>
7. Configure the collection path, as shown in the figure below:
![](https://main.qcloudimg.com/raw/7b9799a0d2a6d1200318dfc35243ea52.png)
Thus, you have completed the configuration of the log collection. You can set other configurations of the workload as needed.


### Configuring the log consumer
The log collection feature supports setting user-built Kafka pods or log topics specified by CLS as the consumer of log content. The log collection agent will send the collected logs to the topic specified by Kafka or the log topic specified by CLS.

<dx-tabs>
::: Configuring Kafka as the log consumer
If you select Kafka as the consumer of log collection, it is recommended you to use CKafka. The experience of its consumption and production modes are the same as the native version, and it supports alarm configurations.
Specify the Broker address and Topic of Kafka in the container configuration, and ensure that all resources in the cluster can access the user-specified Kafka Topic, as shown in the figure below:
![](https://main.qcloudimg.com/raw/2a226f61d5db3a048f804e83d3f0debb.png)
>! You need to select “delete” for `cleanup.policy` in Kafka Topic configuration. If you select “compact”, CLS will fail to report to Kafka, resulting in data loss, as shown in the figure below:
![](https://main.qcloudimg.com/raw/c3f3a6f892b9c07cb24f7e210db5f80e.png)
:::
::: Configuring CLS as the log consumer
- CLS currently supports log collection reporting only for container clusters in the same region. For more information, see [Creating a logset and a log topic](https://intl.cloud.tencent.com/document/product/614/31592).
- Enable the log topic's **Log Index**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a8413fb410367e01acfa9ff62e7a291d.png)
:::
</dx-tabs>

<span id="yaml"></span>
### Configuring log collection via yaml
This document provides three collection methods for your choice: collecting logs to Kafka, collecting logs to CLS via a secret and collecting logs to CLS via a role.
>! If both key and role authorization are configured in yaml, pod actually uses role authorization.

<dx-tabs>
::: Collecting logs to Kafka
Enable log collection by adding environmental variables.
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
**Field description**:
<table>
	<tr>
		<th>Field Name</th> <th>Meaning</th>
	</tr>
	<tr>
		<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer can be kafka or CLS. The key indicates whether log collection is enabled.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: true; false. Default value: true</td>
	</tr>
	<tr>
		<td>EKS_LOGS_KAFKA_TOPIC</td> <td>Log topic</td>
	</tr>
	<tr>
		<td>EKS_LOGS_KAFKA_BROKERS</td> <td>kafka brokers: ip1:port1, ip1:port2, and ip2:port2 formats, separated by “,”. Use this environmental variable for external application. EKS_LOGS_KAFKA_HOST will no longer be visible to external users.</td>
	</tr>
</table>
:::


::: Collecting logs to CLS via a secret

<span id="z"></span>

### Creating a secret

>! The following sample is to manually create a secret through yaml. If you create a secret through the console, you do not need to perform 64 encoding. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676).

Run the following command via kubectl to obtain the secretid and secretkey for base64 encoding. Replace secretid and secretkey with the actual secretid and secretkey that you use.
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
Enable log collection by adding environmental variables.
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

**Field description**:
<table>
<tr>
<th>Field Name</th> <th>Meaning</th>
</tr>
<tr>
<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer can be kafka or CLS. The key indicates whether log collection is enabled.</td>
</tr>
<tr>
<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td></tr>
<tr>
<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: true; false. Default value: true</td>
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



::: Collecting logs to CLS via a role
#### Creating a role  
On the [CAM console](https://console.cloud.tencent.com/cam/role), create a role. While creating a role, you need to select **Tencent Cloud product services**, bind the role with a **CVM**, and select **QcloudCLSAccessForApiGateWayRole** policy. For more information, see [Creating Roles](https://intl.cloud.tencent.com/document/product/598/19381).
In the pod template, add annotation, specify the role name, and obtain the permission policy of the role.

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
**Field description**:
<table>
	<tr>
		<th>Field Name</th> <th>Meaning</th>
	</tr>
	<tr>
		<td>EKS_LOGS_OUTPUT_TYPE</td> <td>The consumer can be kafka or CLS. The key indicates whether log collection is enabled.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute paths. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
	</tr>
	<tr>
		<td>EKS_LOGS_METADATA_ON</td> <td>Valid values: true; false. Default value: true</td>
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



### Updating log collection
You can update log collection via the console and yaml. Please refer to the following directions:



<dx-tabs>
::: Updating log collection via the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and click **Elastic Cluster** in the left sidebar.
2. Select the ID of the desired cluster for log collection configuration to enter the cluster management page.
3. Choose **Workload** on the left, find the row of the desired workload for which you want to update log collection, and click **Update Pod Configuration** > **Advanced Settings** on the right, as shown in the figure below:
![](https://main.qcloudimg.com/raw/a5f93ff2724f199619f998b1b2040be1.png)
4. Click **Done**.

:::


::: Updating log collection via yaml
Find the yaml corresponding to the workload for which you want to update log collection. Then modify the corresponding variable values based on the relevant variable name changes of the configuration. You can view the meanings of variable names in [Configuring log collection](#yaml).
:::
</dx-tabs>


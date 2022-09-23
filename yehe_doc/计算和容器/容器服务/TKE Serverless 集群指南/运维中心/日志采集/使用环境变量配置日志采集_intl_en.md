## Overview
In TKE Serverless clusters, you can use environment variables to configure log collection, and collect logs by line without parsing, or [use custom resource definitions (CRD) to configure log collection](https://intl.cloud.tencent.com/document/product/457/40585).

This document describes how to use the environment variables to configure the log collection feature for a TKE Serverless cluster, and to send the logs of services within the cluster to [Cloud Log Service (CLS)](https://www.tencentcloud.com/products/cls) or external Kafka. This feature is suitable for users who need to store and analyze service logs in TKE Serverless clusters.

To use the log collection feature in a TKE Serverless cluster, you need to manually enable it for the cluster when creating a workload. You can enable this feature by performing the following operations:
- [Configuring log collection in the console](#output)
- [Configuring log collection via yaml](#yaml)
- [Updating log collection](#new)


#### Notes
After the log collection feature is enabled for the TKE Serverless cluster, the log collection agent will send the collected logs in JSON format to the specified consumer end based on your configuration. The details of the collection path and consumer end are as follows:
  - **Consumer end**: The log collection service allows you to set Kafka or CLS as the log consumer end.
  - **Collection path**: The path of the logs to collect. The collection path supports collection standard output (stdout) and absolute path. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.  

## Prerequisite

- Confirm that the Kubernetes cluster can access the log consumer end.
- The length of a log is limited to 2 M. The log is truncated if this limit is exceeded.
  <dx-alert infotype="notice" title="">
  If the log output rate is high, you need to adjust this parameter configuration to avoid OOM. For more information, see [How to adjust the log collection configuration to adapt to different log output rates](https://intl.cloud.tencent.com/document/product/457/40587).
  </dx-alert>




## Directions


### Configuring log collection in the console[](id:output)
When the log collection is enabled for the TKE Serverless cluster, the log information is collected and output to the specified consumer end in JSON format with Kubernetes metadata attached, including the label of the Pod to which the container belongs, annotation, etc. The specific directions are as follows:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the cluster management page, click the ID of the target Serverless cluster to enter the cluster details page.
3. Select a workload type in **Workload** on the left to go to the corresponding page, and then click **Create**.
4. In **Containers in the Pod** section, select **Advanced settings**, and check **Activate** to enable log collection.
![](https://main.qcloudimg.com/raw/2359897f61c9c663d31db1cdca03f3c4.png)
5. Refer to the following information to configure the log consumer end. You can choose CLS or Kafka as the log consume end.
<dx-tabs>
::: Configuring CLS as the log consumer end
1. Select **CLS** as the **Consumer end**, and select the **Logset** and **Log topic**.
![](https://main.qcloudimg.com/raw/37623ea379501b3b431fac609b9681c0.png)
If there is no suitable logset, you can [create a logset and a log topic](https://intl.cloud.tencent.com/document/product/614/31592).
<dx-alert infotype="notice" title="">
CLS currently only supports log collection and reporting for intra-region container clusters.
</dx-alert>
2. Enable the **log index** for the selected log topic. Index configuration is required for CLS log search and analysis. If it is not enabled, you cannot view the logs. For how to configure the index, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).
You can go to the **[CLS console](https://console.cloud.tencent.com/cls/topic?region=ap-guangzhou)** > **Log topic** page, select a log topic name, and enable the index in the **Index configuration** page.
![](https://main.qcloudimg.com/raw/a6f481ce07cafd4ecb8d13ac05950b99.png)

:::
::: Configuring Kafka as the log consumer end
If you select Kafka as the consumer end, it is recommended that you use CKafka. The experience of its consumption and production modes are the same as the native version, and it supports alarm configurations.
Specify the Broker address and Topic of Kafka in the container configuration, and ensure that all resources in the cluster can access the Kafka Topic specified by the user.
![](https://main.qcloudimg.com/raw/27e5173a642dfd0e2c84c93c0b319bcc.png)
<dx-alert infotype="notice" title="">
You need to select “delete” for `cleanup.policy` in Kafka Topic configuration. If you select “compact”, CLS will fail to report to Kafka, resulting in data loss.
![](https://main.qcloudimg.com/raw/01e49f01c82fd0cf13229fbade701641.png)
</dx-alert>
:::
</dx-tabs>

6. Select **Role** or **Key** to authorize.
<dx-alert infotype="notice" title="">
 - You can only select the same authorization method for the containers in the same Pod. The last modification shall prevail. For example, if you select key authorization for the first container and role authorization for the second container, finally both containers will adopt role authorization.
 - You can only select the same role to authorize for the containers in the same Pod.
</dx-alert>
<dx-tabs>
::: Role authorization
 - Select a role that can access CLS, as shown in the figure below:
![](https://main.qcloudimg.com/raw/890940885a3fd7502cf28aa62f970e2c.png)
 - If there is no suitable role, you can create one as follows:
**Creating a policy**[](id:policy)
  You need to create a policy before creating a role. This policy determines the permissions your role can have.
  1. Log in to the CAM console and select **[Policies](https://console.cloud.tencent.com/cam/policy)** in the left sidebar.
  2. On the “Polices” page, click **Create custom policy**.
  3. Select **Create by policy generator** in “Select policy creation method” pop-up window.
  4. In the “Visual Policy Generator”, select **Cloud Log Service (cls)** for **Service**, and select **Write: pushLog** for **Action**.
![](https://main.qcloudimg.com/raw/8ef0012a6e7f6f9d1c0152159fa1bc79.png)
  5. Click **Next** to go to the “Associate users/user groups” page.
  6. Confirm the policy name and click **Done**.

 **Creating a role**
  After creating a policy, you need to bind this policy to a role, so that the role has permissions corresponding to the policy.
  1. Log in to the CAM console, and select **[Roles](https://console.cloud.tencent.com/cam/role)** in the left sidebar.
  2. On the “Roles” page, click **Create role**.
  3. In the “Select role entity” window that appears, select **Tencent Cloud Product Service** to go to the “Create custom role” page.
  4. In the “Enter role entity info” step, select **Cloud Virtual Machine (cvm)** and click **Next**.
<dx-alert infotype="notice" title="">
    You must select **Cloud Virtual Machine (cvm)** as the role entity, otherwise, you cannot complete the authorization process.
</dx-alert>
  5. In the “Configure role policy” step, select **[Created policy](#policy)**, and click **Next**.
  6. In the “Review” step, enter the role name to review the role information, and then click **Done**. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).
:::
::: Key authorization
- Select the “SecretId” and “SecretKey” of your account API key as the variable values to create the cluster Secret.
![](https://main.qcloudimg.com/raw/c03d348d34fc5c5d2666b1e883138bab.png)
- If there is no suitable Secret, you need to create one. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676). You can view the SecretId and SecretKey in [API Keys](https://console.cloud.tencent.com/cam/capi).
<dx-alert infotype="notice" title="">
 The user corresponding to the API key must have the permission to access the CLS. If there is no API key, you need to create one. For more information, see [Access Key](https://www.tencentcloud.com/document/product/598/34227).
</dx-alert>
:::
</dx-tabs>
7. Configure the collection path.
![](https://main.qcloudimg.com/raw/4f9fb3635b7a3c3ab35e8387d877a08b.png)
At this point, you have configured the log collection feature. You can set other configurations of the workload as needed.



[](id:yaml)
### Configuring log collection via yaml [](id:yaml)
This document provides three collection methods for your choice: Collecting logs to Kafka, collecting logs to CLS via a secret and collecting logs to CLS via a role.
<dx-alert infotype="notice" title="">
 If both key and role authorization are configured in yaml, the Pod actually uses role authorization.
</dx-alert>
<dx-tabs>
::: Collecting logs to Kafka
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
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute path. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
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
<b>Note</b>: Here the key gets the variable value from the field of the Pod. The above examples all take the Pod name as an example, and it also supports namespace, PodIP, etc. For more information, see <a href="https://kubernetes.io/zh/docs/tasks/inject-data-application/environment-variable-expose-pod-information/">Kubernetes Documentation</a>.</td>
	</tr>
</table>

Verify whether the delivery by key is enabled, as shown below:
- If it is not enabled, the key is not displayed in the message details, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2b9c03bafbc0694ee03e817cd5e771f6.png)
- If it is enabled, the key is displayed in the message details, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/5814b84c37d6b90590bbdb7fabd08c6d.png)

:::


::: Collecting logs to CLS via a secret
#### Creating a secret[](id:z)
<dx-alert infotype="notice" title="">
 The following sample is to manually create a secret through yaml. If you create a secret through the console, you do not need to perform 64 encoding. For more information, see [Secret Management](https://intl.cloud.tencent.com/document/product/457/30676).
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
<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute path. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td></tr>
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



::: Collecting logs to CLS via a role
#### Step 1: Creating a role  
**Creating a policy**[](id:policy)
You need to create a policy before creating a role. This policy determines the permissions your role can have.
1. Log in to the CAM console and select **[Policies](https://console.cloud.tencent.com/cam/policy)** in the left sidebar.
2. On the “Polices” page, click **Create custom policy**.
3. Select **Create by policy generator** in “Select policy creation method” pop-up window.
4. In the “Visual Policy Generator”, select **Cloud Log Service (cls)** for **Service**, and select **Write: pushLog** for **Action**.
![](https://main.qcloudimg.com/raw/8ef0012a6e7f6f9d1c0152159fa1bc79.png)
5. Click **Next** to go to the “Associate users/user groups” page.
6. Confirm the policy name and click **Done**.

**Creating a role**
After creating a policy, you need to bind this policy to a role, so that the role has permissions corresponding to the policy.
1. Log in to the CAM console, and select **[Roles](https://console.cloud.tencent.com/cam/role)** in the left sidebar.
2. On the “Roles” page, click **Create role**.
3. In the “Select role entity” window that appears, select **Tencent Cloud Product Service** to go to the “Create custom role” page.
4. In the “Enter role entity info” step, select **Cloud Virtual Machine (cvm)** and click **Next**.
    <dx-alert infotype="notice" title="">
    You must select **Cloud Virtual Machine (cvm)** as the role entity, otherwise, you cannot complete the authorization process.
    </dx-alert>
5. In the “Configure role policy” step, select **[Created policy](#policy)**, and click **Next**.
6. In the “Review” step, enter the role name to review the role information, and then click **Done**. For more information, see [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381).


After creating a role, you need to add annotation, specify the role name, and obtain the permission policy contained in the role in the Pod template.
```shell
template:
   metadata:
     annotations:
       eks.tke.cloud.tencent.com/role-name: "eks-pushlog"
```
#### Step 2: Creating a Deployment
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
		<td>EKS_LOGS_LOG_PATHS</td> <td>Log path. It supports stdout (collection standard output) and absolute path. It also supports wildcard (*). If multiple paths are specified, separate them with “,”.</td>
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
You can update log collection in the console or via yaml. Please refer to the following directions:



<dx-tabs>
::: Updating log collection in the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the cluster management page, click the ID of the target Serverless cluster to enter the cluster details page.
3. Choose **Workload** on the left, find the row of the desired workload for which you want to update log collection, and click **Update Pod configuration** > **Advanced settings** on the right to modify configurations.
![](https://main.qcloudimg.com/raw/6e82866759f9704fd49d7695f57dfa47.png)
4. Click **Done** to complete the process.

:::


::: Updating log collection via yaml
Find the yaml corresponding to the workload for which you want to update log collection. Then modify the corresponding variable values based on the relevant variable name changes of the configuration. You can view the meanings of variable names in [Configuring log collection](#yaml).
:::
</dx-tabs>

## FAQs
If you have any questions, please refer to [Log Collection FAQs](https://intl.cloud.tencent.com/document/product/457/40582). If your question remains unresolved, please [Contact Us](https://intl.cloud.tencent.com/document/product/457/46718).

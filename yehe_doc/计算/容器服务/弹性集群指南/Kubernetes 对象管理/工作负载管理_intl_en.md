## Introduction
This document describes how to select different types of workloads to run your services in an elastic cluster.
>To create and manage your Elastic Kubernetes Service (EKS) workloads by using a YAML file, see [EKS Annotation Description](#workloadAnnotationDesc).

## Prerequisites
- An elastic cluster has been created and is in the Running state. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- The cluster has an appropriate namespace that is in the Active state.

## Workload Types
### Deployment
A Deployment declares a template for a pod and a policy for controlling how the pod runs. It is used to deploy stateless applications. You can specify the number of replicas, a scheduling policy, and an update policy for a pod that runs in the Deployment as required.

### StatefulSet
A StatefulSet is used to manage stateful applications. It creates a persistent identifier for each pod based on the specifications. The identifier will be retained after the pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require any persistent identifier, we recommend that you use a Deployment to deploy the application.

### Job
A Job creates one or more pods and ensures that these pods run according to the specified rules until a specified number of them successfully terminate. Jobs can be used in many scenarios, such as batch computing and data analysis. You can specify the required number of completions, concurrency (the number of pods running at any instant), and the restart policy as required.
When a Job is completed, no more pods are created, but the existing pods are retained. You can view the logs of the completed pods in **Logs**. Deleting a Job removes the pods it created, and the logs of these pods will be invisible.

### CronJob
A CronJob object is like one line of a crontab (cron table) file. It runs a Job periodically on a given schedule and uses the Cron format.
The Cron format is as follows:
```
# File format description
#  ——min (0 - 59)
# |  ——hour (0 - 23)
# | |  ——day of month (1 - 31)
# | | |  ——month (1 - 12)
# | | | |  ——day of week (0 - 6)
# | | | | |
# * * * * *
```

## Directions
1. Log in to the TKE console and click [**Elastic Cluster**](https://console.cloud.tencent.com/tke2/ecluster) in the left sidebar.
2. On the **Elastic Cluster** page that appears, click the ID of the cluster where the workload that you want to create is located. The **Deployment** page for the cluster appears.
3. Click **Create** to go to the **New Workload** page.
4. Specify a name and type of the workload to be created.
  - For the specific parameter settings for each type of workload, see the following:
     - [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
     - [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
     - [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)
     - [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
   - For the instructions on performing other operations, see the following:
     - [Setting a Resource Limit for a Workload](https://intl.cloud.tencent.com/document/product/457/30667)
     - [Setting a Scheduling Rule for a Workload](https://intl.cloud.tencent.com/document/product/457/30668)
     - [Setting Health Check for a Workload](https://intl.cloud.tencent.com/document/product/457/30669)
        - [Setting the Running Command and Parameters for a Workload](https://intl.cloud.tencent.com/document/product/457/30670)

<span id="workloadAnnotationDesc"></span>
## EKS Annotation Description
<table>
<thead>
<tr>
<th width="">Annotation Key</th>
<th width="22%">Annotation Value</th>
<th>Description</th>
<th width="30%">Required</th>
</tr>
</thead>
<tbody><tr>
<td>eks.tke.cloud.tencent.com/cpu</td>
<td>Specify the value as instructed in <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The default unit is core.</td>
<td>CPU specifications for the pod</td>
<td>Yes. An error occurs if the value is not specified or the specified specification does not exist.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/mem</td>
<td>Specify the value according to <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit should be included in the value, for example, 512Mi, 0.5Gi, or 1Gi.</td>
<td>CPU specifications for the pod</td>
<td>Yes. An error occurs if the value is not specified or the specified specification does not exist.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/security-group-id</td>
<td><a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">The ID of the security group bound to the workload. </a>You can specify multiple values and separate them with commas (<code>,</code>), for example, <code>sg-id1,sg-id2</code></td>.
<td>Security group bound to the workload by default</td>
<td>No. If no value is specified, the system binds the workload to the default security group for the region where the workload is located. <br>You must set the value to a security group ID that exists in the region where the workload is located.</td>
</tr>
</tbody></table>

### Sample code
```
apiVersion: apps/v1beta2
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    description: test
    eks.tke.cloud.tencent.com/cpu: "1"
    eks.tke.cloud.tencent.com/mem: 2Gi
    eks.tke.cloud.tencent.com/security-group-id: "sg-dxxxxxx5,sg-zxxxxxxu"
  creationTimestamp: "2019-10-11T03:47:55Z"
  generation: 1
  labels:
    k8s-app: nginx
    qcloud-app: nginx
  name: nginx
  namespace: default
  resourceVersion: "33796648"
  selfLink: /apis/apps/v1beta2/namespaces/default/deployments/nginx
  uid: e86f6533-ebd9-11e9-b061-4effc6de97a3
spec:
  minReadySeconds: 10
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      k8s-app: nginx
      qcloud-app: nginx
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
    type: RollingUpdate
  template:
    metadata:
      annotations:
        eks.tke.cloud.tencent.com/cpu: "1"
        eks.tke.cloud.tencent.com/mem: 2Gi
        eks.tke.cloud.tencent.com/wan: "true"
      creationTimestamp: null
      labels:
        k8s-app: nginx
        qcloud-app: nginx
    spec:
      containers:
      - env:
        - name: PATH
          value: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
        - name: NGINX_VERSION
          value: 1.17.4
        - name: NJS_VERSION
          value: 0.3.5
        - name: PKG_RELEASE
          value: 1~buster
        image: ccr.ccs.tencentyun.com/alex_lee/nginx:latest
        imagePullPolicy: Always
        name: nginxcontainer
        resources:
          limits:
            cpu: 500m
            memory: 1Gi
          requests:
            cpu: 250m
            memory: 256Mi
        securityContext:
          privileged: false
          procMount: Default
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /tmp
          name: vol
      dnsPolicy: ClusterFirst
      imagePullSecrets:
      - name: qcloudregistrykey
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - emptyDir: {}
        name: vol
```

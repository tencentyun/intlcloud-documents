## Overview
This document describes how to select different types of workloads to run your services in an elastic cluster.
>! 
> - Elastic clusters do not have nodes. Workloads allocate resources for each pod based on parameter settings when they are created. For more information, please see [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).
> - To create and manage Kubernetes objects using a YAML file, specify annotations. For more information, please see [Annotation Description](https://intl.cloud.tencent.com/document/product/457/36162).


## Prerequisites
- You have created an elastic cluster that is in Running state. For more information, please see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- The cluster has an appropriate namespace that is in Active state.

## Workload Types
### Deployment
A Deployment declares the pod template and pod running policies. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for pods running in the Deployment as needed.

### StatefulSet
A StatefulSet is used to manage stateful applications. A Pod created by a StatefulSet has a persistent identifier that is created according to the specifications. The identifier will be retained after the Pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require any persistent identifier, we recommend that you use a Deployment to deploy the application.

### Job
A Job creates one or more pods and ensures that these pods run according to specified rules until they are terminated. Jobs can be used in many scenarios, such as batch computing and data analysis. You can specify the number of repeated runs, concurrency, and restart policy as required.
A Job will keep existing pods and will not create new pods after it is complete. You can view the logs of completed pods in "Logs". Deleting a Job will clean up the pods it created as well as the logs of those pods.

### CronJob
A CronJob object is similar to a line in a crontab (cron table) file. It periodically runs a Job according to the specified schedule. For more information about the format, please see the Cron documentation.
The format of a Cron is as follows:
```
# File format description
# ——min (0 - 59)
# |  ——hour (0 - 23)
# | | ——day of month (1 - 31)
# | | |  ——month (1 - 12)
# | | | |  ——day of week (0 - 6)
# | | | | |
# * * * * *
```

## Directions
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** on the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the cluster where the workload that you want to create is located. The **Deployment** page for the cluster appears, as shown in the following figure.
![](https://qcloudimg.tencent-cloud.cn/raw/dd712bafab8210a8904b4f57c1302d2a.png)
3. Click **Create** to enter the **Create Workload** page.
4. Specify the workload name and select a workload type.
  - For more information about parameter settings for each workload type, please see the following:
     - [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
     - [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
     - [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)
     - [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
   - For the instructions on other operations, please see the following documents:
     - [Setting the Resource Limit of Workload](https://intl.cloud.tencent.com/document/product/457/30667)
     - [Setting the Scheduling Rule for a Workload](https://intl.cloud.tencent.com/document/product/457/30668)
     - [Setting the Health Check for a Workload](https://intl.cloud.tencent.com/document/product/457/30669)
        - [Setting the Run Command and Parameter for a Workload](https://intl.cloud.tencent.com/document/product/457/30670)

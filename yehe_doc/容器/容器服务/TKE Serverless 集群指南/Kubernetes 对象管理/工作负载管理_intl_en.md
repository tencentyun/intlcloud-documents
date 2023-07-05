
This document describes how to select a workload to run your applications in a TKE Serverless cluster.
>! 
> - Serverless clusters do not have nodes. Workloads allocate resources for each Pod based on parameter settings when they are created. For more information, see [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).
> - To create and manage Kubernetes objects using a YAML file, specify annotations. For more information, please see [Annotation Description](https://intl.cloud.tencent.com/document/product/457/36162).




## Workload Types
### Deployment
A Deployment declares the Pod template and Pod running policies. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for Pods running in the Deployment as needed.

### StatefulSet
A StatefulSet is used to manage stateful applications. A Pod created by a StatefulSet has a persistent identifier that is created according to the specifications. The identifier will be retained after the Pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require any persistent identifier, we recommend that you use a Deployment to deploy the application.

### Job
A Job creates one or more Pods and ensures that these Pods run according to specified rules until they are terminated. Jobs can be used in many scenarios, such as batch computing and data analysis. You can specify the number of repeated running, concurrency, and restart policy as required.
After the Job stops running, it will not create new Pods and only the running records of original Pods exist. However, the real underlying resources have been released. Therefore, you cannot query the logs of the corresponding Pods in "Logs" section of the console.

### CronJob
A CronJob object is similar to a line in a crontab (cron table) file. It periodically runs a Job according to the specified schedule. For more information about the format, see the Cron documentation.
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


## Prerequisite
- You have created a Serverless cluster that is in “Running” status. For more information, please see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- The cluster has an appropriate namespace that is in Active status.

## Directions
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the cluster management page, click the ID of the target Serverless cluster to enter the basic information page.
3. Select a type of workload in the left sidebar, and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/57d9524c56c30ee5c7d435b1af29820b.png)
4. On the “Create workload” page, enter a name for the workload and select the workload type.
  - For more information about parameter settings for each workload type, see the following documents:
     - [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
     - [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
     - [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)
     - [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
   - For the instructions on other operations, see the following documents:
     - [Setting the Resource Limit of Workload](https://intl.cloud.tencent.com/document/product/457/30667)
     - [Setting the Scheduling Rule for a Workload](https://intl.cloud.tencent.com/document/product/457/30668)
     - [Setting the Health Check for a Workload](https://intl.cloud.tencent.com/document/product/457/30669)
     - [Setting the Run Command and Parameter for a Workload](https://intl.cloud.tencent.com/document/product/457/30670)

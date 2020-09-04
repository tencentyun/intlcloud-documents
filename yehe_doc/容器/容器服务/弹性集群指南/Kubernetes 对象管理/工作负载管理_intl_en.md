## Scenario
This document describes how to select different types of workloads to run your services in an elastic cluster.
> 
> - Elastic clusters have no nodes. Workloads allocate resources for each pod based on parameter settings when they are created. For more information, see [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).
> - To create and manage Kubernetes objects by using a YAML file, specify annotations. For more information, see [Annotation Description](https://intl.cloud.tencent.com/document/product/457/36162).


## Prerequisites
- You have created an elastic cluster that is in Running state. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- The cluster has an appropriate namespace that is in Active state.

## Workload Types
### Deployment
A Deployment declares the pod template and pod running policies. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for pods running in the Deployment as needed.

### StatefulSet
A StatefulSet is used to manage stateful applications. It creates a persistent identifier for each pod based on the specifications. The identifier will be retained after a pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require any persistent identifier, we recommend that you use a Deployment to deploy the application.

### Job
A Job creates one or more pods and ensures that these pods run according to specified rules until they are terminated. Jobs can be used in many scenarios, such as batch computing and data analysis. You can specify the number of repeated running, concurrency, and restart policy as required.
A Job maintains existing pods and will not create new pods after it is completed. You can view the logs of completed pods in "Logs". Deleting a Job removes the pods it created and the logs of these pods.

### CronJob
A CronJob object is similar to a line in a crontab (cron table) file. It periodically runs a Job according to the specified schedule. For more information on the format, see Cron documentation.
The Cron format is as follows:
```
# File format description
# ——minute (0 – 59)
# | ——hour (0 – 23)
# | | ——day (1 – 31)
# | | | ——month (1 – 12)
# | | | |  ——day of week (0 – 6)
# | | | | |
# * * * * *
```

## Directions
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the "Elastic Cluster" page, click the ID of the cluster where the workload that you want to create resides. The **Deployment** page for the cluster appears, as shown in the following figure.
![](https://main.qcloudimg.com/raw/ad1f42c40dd0d7cc71f8980e31d851ed.png)
3. Click **Create** to go to the "Create a workload" page.
4. Specify the workload name and select a workload type.
  - For more information on parameter settings for each workload type, see the following:
     - [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
     - [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
     - [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)
     - [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
   - For more information on how to perform other operations, see the following:
     - [Setting the Resource Limit of a Workload](https://intl.cloud.tencent.com/document/product/457/30667)
     - [Setting the Scheduling Rule for a Workload](https://intl.cloud.tencent.com/document/product/457/30668)
     - [Setting the Health Check for a Workload](https://intl.cloud.tencent.com/document/product/457/30669)
        - [Setting the Running Command and Parameter for a Workload](https://intl.cloud.tencent.com/document/product/457/30670)

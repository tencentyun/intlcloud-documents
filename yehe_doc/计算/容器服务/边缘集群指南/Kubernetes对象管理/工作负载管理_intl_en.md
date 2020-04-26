## Scenario
This document describes how to run your service through various workloads in an edge cluster.

## Prerequisites
- You have an edge cluster that is in the Running state. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster has an appropriate namespace that is in the Active state.
- The cluster has sufficient edge computing resources to run the workloads.

## Workload Types
### Deployment
A Deployment declares a template for a pod and a policy for controlling how the pod runs. It is used to deploy stateless applications. You can specify the number of replicas, scheduling policy, and update policy for a pod running in the Deployment as required.

### StatefulSet
A StatefulSet is primarily used to manage stateful applications. Pods created will come with a persistent identifier according to the specification. The identifier will not change even if the pod is migrated or restarted after termination.
When persistent storage is required, you can use the identifiers to map to the corresponding storage volumes. If the application does not require persistent identifiers, we recommend that you use Deployment to deploy the application.

### Job
A Job creates one or more pods and ensures that these pods run according to the specified rules until a specified number of them successfully terminate. Jobs can be used in many scenarios, such as batch computing and data analysis. You can specify the required number of completions, concurrency (the number of pods running at any instant), and the restart policy as required.
When a Job is completed, no more pods are created, but existing pods will be retained. You can view the logs of the completed pods in **Logs**. Deleting a Job cleans up the pods it created, and the logs of these pods will be invisible.

### CronJob
A CronJob object resembles one line of a crontab (cron table) file. It runs a Job periodically on a given schedule and uses the Cron format.
The cron format is as follows:
```
# File format description
# ——minute (0 - 59)
# | ——hour (0 - 23)
# | | ——day (1 - 31)
# | | | ——month (1 - 12)
# | | | |  ——day of week (0 - 6)
# | | | | |
# * * * * *
```

## Directions
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Edge Clusters** in the left sidebar.
2. On the "Edge Clusters" page that appears, click the ID of the cluster where the workload that you want to create is located to go to the "Deployment" page.
3. Click **Create** to go to the "Create Workload" page.
4. On the "Create Workload" page, enter a name for the workload and select the workload type.
For the specific parameter settings for each type of workload, see the following:
 - [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662)
 - [StatefulSet Management](https://intl.cloud.tencent.com/document/product/457/30663)
 - [Job Management](https://intl.cloud.tencent.com/document/product/457/30665)
 - [CronJob Management](https://intl.cloud.tencent.com/document/product/457/30666)



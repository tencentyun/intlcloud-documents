
## Cluster Lifecycle Description

| Status   | Description                                     |
| :----- | :--------------------------------------- |
| Creating | You are creating the TKE Serverless cluster and applying for cloud resources.         |
| Running | The cluster is running properly.                            |
| Idle | The cluster is idle.                        |
| Activating | The cluster is changing from the idle status to the running status.  |
| Deleting | You are deleting the cluster while terminating and releasing cloud resources.    |
| Abnormal   | An exception occurred in the cluster, such as an inaccessible network.          |


## Idle Cluster Status Description

To make the most of idle cluster resources, we have launched the idle cluster repossession feature in TKE Serverless, which displays clusters without legacy Pods and Pod creation or deletion operations for seven consecutive days as "idle" clusters.

A cluster is considered idle if:

- It has no legacy Pods created by users.
- No Pods are created or deleted for seven consecutive days.
- At least three days has passed since it changes from the idle status to the normal status.
- Over seven days has passed since it is created.

An "idle" cluster retains all its information but becomes unavailable. You can't view cluster monitoring data and cluster details or perform API server operations. You can activate the cluster by clicking **More** > **Activate** in the **Operation** column or click **Delete** to delete it.

An activated idle cluster has the same features and configuration as it used to have. Note that if it has no Pods and Pod creation or deletion operations for three consecutive days after the activation, it will become idle again.

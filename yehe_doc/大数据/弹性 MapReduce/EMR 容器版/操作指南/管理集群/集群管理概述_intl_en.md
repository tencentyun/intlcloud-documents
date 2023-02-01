This document describes how to view the information of a container-based EMR cluster in the console.

## Viewing the cluster information
1. After successfully creating a cluster, log in to the [container-based EMR console](https://console.cloud.tencent.com/emr/static/containerdeploy), click the **ID/Name** of the target cluster on the **Cluster list** page, or select **Details** in the **Operation** column in the **Cluster list**.
2. **Cluster Info** records the basic information of the EMR cluster, such as **Region Info**, **Namespace**, **Component Version**, **Container/Cluster Type**, **Container Network**, **COS**, **Bucket Name**, **Custom Service Role**, and **Resource Usage**.
3. If you need refined authorization, you can set a custom service role for accessing Tencent Cloud resources during the execution of big data jobs. You should select **Tencent Cloud Product Service** as the service role type and **Elastic MapReduce** as the service supporting the role.

## Terminating a cluster
When you no longer need a container-based EMR cluster, you can log in to the [container-based EMR console](https://console.cloud.tencent.com/emr/static/containerdeploy) and select **Terminate** in the **Operation** column in the **Cluster list**. Then, in the **Terminate Cluster** pop-up window, confirm the information of the cluster to be terminated and click **Terminate**.
![](https://qcloudimg.tencent-cloud.cn/raw/11f64ef8ad99b6e8fa8580b793da64ae.jpg)

## Deleting a cluster
When a container-based EMR cluster fails to be created, you can log in to the [container-based EMR console](https://console.cloud.tencent.com/emr/static/containerdeploy) and select **Delete** in the **Operation** column in the **Cluster list**. Then, in the **Delete Cluster** pop-up window, confirm the information of the cluster to be deleted and click **Confirm**.


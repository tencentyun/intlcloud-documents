## Introduction
Horizontal Pod Autoscaler (HPA) can automatically scale the number of Pods for services according to the average CPU utilization of target Pods and other metrics. This document describes how to implement Pod autoscaling via Tencent Cloud TKE console.

## How It Works
The HPA backend components pull monitoring metrics of containers and Pods from Tencent Cloud’s Cloud Monitor every 30 seconds and calculate the desired number of replicas based on the current monitoring data, the current number of replicas, and the desired value of the metrics. When there is a gap between the desired number and the actual number of replicas, HPA will trigger a Deployment to adjust the number of Pod replicas, thereby achieving auto-scaling.
Take CPU utilization as an example. Suppose there are two Pods with an average CPU utilization of 90%, and the target CPU utilization is set to 60% for autoscaling. Then the number of Pods will be automatically adjusted as follows: 90% × 2 / 60% = 3 Pods.
> If you set multiple auto scaling metrics, HPA will calculate the target numbers of replicas separately according to each metric and then use the maximum number for auto scaling.

## Notes
- If you choose **CPU utilization (by request)** as the metric type, a CPU request must be set for the container.
- Set reasonable targets for the policy metrics. For example, set 70% for containers and applications and leave 30%.
- Keep Pods and nodes healthy; avoid frequently recreating Pods.
- Ensure that the load balancer works stably.
- If the gap between the actual number and desired number of replicas is smaller than 10%, HPA will not adjust the number of replicas.
- If the value of Deployment.spec.replicas corresponding to the service is 0, HPA will not work.
- If multiple HPAs are bound to a single Deployment, the HPAs will take effect simultaneously, which will cause clusters to be repeatedly scaled.

## Prerequisites
- You have [registered for a Tencent Cloud account](https://cloud.tencent.com/register).
- You are logged in to the [TKE console](https://console.cloud.tencent.com/tke2).
- You have created a cluster. For details about how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).



## Directions

### Enabling Auto Scaling
You can enable auto scaling in one of the following ways.

### Setting auto-adjustment of the number of Pods
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Select **Create** as shown below:
![](https://main.qcloudimg.com/raw/35583330917b8749972f290f5847e0f8.png)
3. On the **Create Workload** page, select **Auto adjustment** for the number of Pods as shown below:
![](https://main.qcloudimg.com/raw/4d9f2de48a93f82b344cb1780242de26.png)
 - **Trigger Policy**: the policy metrics that trigger the auto-scaling. For details, see [Metric Type](#MetricType).
 - **Number of Pods**: enter the minimum and maximum numbers according to your needs. The number of Pods will be auto-adjusted within the range.

#### Creating auto-scaling group
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Auto-scaling** on the left.
3. Click **Create** on the **HorizontalPodAutoscaler** page as shown below:
![](https://main.qcloudimg.com/raw/25f05ca2148e7b7a82d8370af10058c6.png)
4. Configure the HPA on the **Create HPA** page according to the following instructions. See the figure below:
![](https://main.qcloudimg.com/raw/0e76e8abed2ba63d244415a5b6861f2d.png)
 - **Name**: enter the name of the auto scaling group to be created.
 - **Namespace**: select based on your needs.
 - **Associated Workload**: required; please select based on your needs.
 - **Trigger Policy**: the policy metrics that trigger the auto-scaling. For details, see [Metric Type](#MetricType).
 - **Number of Pods**: enter the minimum and maximum numbers according to your needs. The number of Pods will be auto-adjusted within the range.
4. Click **Create HPA** to complete the creation.

### Creating using YAML
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page.
3. Click **Creating using YAML** in the top right corner as shown below:
![](https://main.qcloudimg.com/raw/1d558af5c6057f8ac8c1682a2b1480f4.png)
4. Edit the content according to your needs and click **Complete** to create the HPA. 


### Updating Auto Scaling Rules
You can update auto scaling rules in one of the following ways.

#### Updating the number of Pods
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Update Pod Quantity** as shown below:
![](https://main.qcloudimg.com/raw/107751e7e5520fa8f11eeafdb883d080.png)
3. On the **Update Pod Quantity** page, change the settings according to your needs and click **Update Number of Pods** as shown below:
![](https://main.qcloudimg.com/raw/af155961769ad37885ea36b087756f2d.png)

#### Modifying HPA configuration
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Auto-scaling** on the left.
3. On the HorizontalPodAutoscaler page, click **Modify Configuration** to the right of the HPA you want to update.
![](https://main.qcloudimg.com/raw/5bc7933b13b005e4c695f89ac0dab0e7.png)
3. On the **Update HPA Configuration** page, change the settings according to your needs and click **Update HPA** as shown below:
![](https://main.qcloudimg.com/raw/e55638c55b122b9857ea45ae40dcf369.png)

#### Editing YAML
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group. Click **Auto-scaling** on the left.
3. On the **HorizontalPodAutoscaler** page, locate the HPA to be updated, and click **Edit YAML** to its right.
![](https://main.qcloudimg.com/raw/707f99e989bb733663f1a21685b74ce8.png)
3. Edit the content according to your needs and click **Complete**.


<span id="MetricType"></span>
## Metric Type
For more information on metrics and types, see [Autoscaling Metrics](https://cloud.tencent.com/document/product/457/38929).

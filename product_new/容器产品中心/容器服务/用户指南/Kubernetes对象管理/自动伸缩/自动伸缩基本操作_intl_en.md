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
![](https://main.qcloudimg.com/raw/c6d54e147a7b2e0e789781a9b743b30b.png)
3. On the **Create Workload** page, select **Auto adjustment** for the number of Pods as shown below:
![](https://main.qcloudimg.com/raw/3d7e13d6372ee8f5f657ce9f524c362a.png)
 - **Trigger Policy**: the policy metrics that trigger the auto-scaling. For details, see [Metric Type](#MetricType).
 - **Number of Pods**: enter the minimum and maximum numbers according to your needs. The number of Pods will be auto-adjusted within the range.

#### Creating auto-scaling group
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Auto-scaling** on the left.
3. Click **Create** on the **HorizontalPodAutoscaler** page as shown below:
![](https://main.qcloudimg.com/raw/462b1796da9e8f8ccc45c33415fe6b61.png)
4. Configure the HPA on the **Create HPA** page according to the following instructions. See the figure below:
![](https://main.qcloudimg.com/raw/585e9028065458d53c303ef0ede1fed7.png)
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
![](https://main.qcloudimg.com/raw/1cb1fa4df085a3f6f76a789adbd058e0.png)
4. Edit the content according to your needs and click **Complete** to create the HPA. 


### Updating Auto Scaling Rules
You can update auto scaling rules in one of the following ways.

#### Updating the number of Pods
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Update Pod Quantity** as shown below:
![](https://main.qcloudimg.com/raw/09d6825bb349718712d8b94843a96cf9.png)
3. On the **Update Pod Quantity** page, change the settings according to your needs and click **Update Number of Pods** as shown below:
![](https://main.qcloudimg.com/raw/2291d0a52e3cb84791b5b7657b629919.png)

#### Modifying HPA configuration
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group to go to the Deployment page. Click **Auto-scaling** on the left.
3. On the HorizontalPodAutoscaler page, click **Modify Configuration** to the right of the HPA you want to update.
![](https://main.qcloudimg.com/raw/d0e498827dd05a95a095634411791a8b.png)
3. On the **Update HPA Configuration** page, change the settings according to your needs and click **Update HPA** as shown below:
![](https://main.qcloudimg.com/raw/47aa6413af8e046d4ccb053aa37856d6.png)

#### Editing YAML
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click the ID of the cluster for which you want to create the scaling group. Click **Auto-scaling** on the left.
3. On the **HorizontalPodAutoscaler** page, locate the HPA to be updated, and click **Edit YAML** to its right.
![](https://main.qcloudimg.com/raw/9eeec0fbf70fdc27f57fb5812b85e88c.png)
3. Edit the content according to your needs and click **Complete**.


<span id="MetricType"></span>
## Metric Type
For more information on metrics and types, see [Autoscaling Metrics](https://cloud.tencent.com/document/product/457/38929).

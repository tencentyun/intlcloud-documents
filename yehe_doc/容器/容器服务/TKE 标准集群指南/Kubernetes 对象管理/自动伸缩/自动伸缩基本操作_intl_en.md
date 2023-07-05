## Overview
Horizontal Pod Autoscaler (HPA) can automatically scale the number of Pods for services according to the average CPU utilization of target Pods and other metrics. This document describes how to implement Pod autoscaling via Tencent Cloud TKE console.

## How it Works
The HPA backend components pull monitoring metrics of containers and Pods from Tencent Cloud’s Cloud Monitor every 15 seconds and calculate the desired number of replicas based on the current monitoring data, the current number of replicas, and the desired value of the metrics. When there is a gap between the desired number and the actual number of replicas, HPA will trigger a Deployment to adjust the number of Pod replicas, thereby achieving auto-scaling.
Take CPU utilization as an example. Suppose there are two Pods with an average CPU utilization of 90%, and the target CPU utilization is set to 60% for autoscaling. Then the number of Pods will be automatically adjusted as follows: 90% × 2 / 60% = 3 Pods.
>! If you set multiple auto scaling metrics, HPA will separately calculate the target numbers of replicas according to each metric and then take the maximum number to use for auto scaling.

## Notes
- If you choose **CPU utilization (by request)** as the metric type, a CPU request must be set for the container.
- Set reasonable targets for the policy metrics. For example, set 70% for containers and applications and leave 30%.
- Keep Pods and nodes healthy; avoid frequently recreating Pods.
- Ensure that the load balancer works stably.
- If the gap between the actual number and desired number of replicas is smaller than 10%, HPA will not adjust the number of replicas.
- If the value of Deployment.spec.replicas corresponding to the service is 0, HPA will not work.
- If multiple HPAs are bound to a single Deployment, the HPAs will take effect simultaneously, which will cause workload replicas to be repeatedly scaled.

## Prerequisites
- You have registered a [Tencent Cloud account](https://www.tencentcloud.com/account/register).
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2).
- You have created a cluster. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).



## Directions

### Enabling Auto Scaling
You can enable auto scaling in one of the following ways.

### Setting auto-adjustment of the number of Pods
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the cluster ID for which a scaling group is to be created.
2. Select **Workload** > **Deployment**. On the **Deployment** page, click **Create**.
3. On the **Create Deployment** page, select **Auto adjustment** for the number of Pods as shown below:
![](https://main.qcloudimg.com/raw/4d9f2de48a93f82b344cb1780242de26.png)
 - **Trigger Policy**: the policy metrics that trigger the auto-scaling. For details, see [Metric Type](#MetricType).
 - **Number of Pods**: enter the minimum and maximum numbers according to your needs. The number of Pods will be auto-adjusted within the range.

#### Creating auto-scaling group
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the cluster ID for which a scaling group is to be created.
2. Select **Auto Scaling** > **HorizontalPodAutoscaler**. On the **HorizontalPodAutoscaler** page, and click **Create**.
3. On the **Create HPA** page, configure the HPA as needed.
![](https://main.qcloudimg.com/raw/0e76e8abed2ba63d244415a5b6861f2d.png)
 - **Name**: Enter the name of the auto scaling group to be created.
 - **Namespace**: select based on your needs.
 - **Workload Type**: select based on your needs.
 - **Associated Workload**: select based on your needs. The value cannot be empty.
 - **Trigger Policy**: the policy metrics that trigger the auto-scaling. For details, see [Metric Type](#MetricType).
 - **Number of Pods**: enter the minimum and maximum numbers according to your needs. The number of Pods will be auto-adjusted within the range.
4. Click **Create HPA**.

### Creating using YAML
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the cluster ID for which a scaling group is to be created.
2. On the cluster basic information page, click **Creating using YAML** in the top right corner.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AnHM733_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223162548.png)
3. Edit the content according to your needs and click **Complete** to create the HPA.


### Updating Auto Scaling Rules
You can update auto scaling rules in one of the following ways.

#### Updating the Pod Quantity
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the target cluster ID.
2. Select **Workload** > **Deployment** to enter the **Deployment** page and click **Update Pod Number**.
![](https://main.qcloudimg.com/raw/107751e7e5520fa8f11eeafdb883d080.png)
3. On the **Update Pod Number** page, select **Auto adjustment** and set parameters as needed.
![](https://main.qcloudimg.com/raw/af155961769ad37885ea36b087756f2d.png)
4. Click **Update number of instance**.

#### Modifying HPA Configuration
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the cluster ID for which a scaling group is to be created.
2. Select **Auto Scaling** > **HorizontalPodAutoscaler**. On the **HorizontalPodAutoscaler** page, click **Modify configuration** in the **Operation** column of the HPA whose configuration is to be updated.
![](https://main.qcloudimg.com/raw/5bc7933b13b005e4c695f89ac0dab0e7.png)
3. On the **Update Configuration** page, change the settings according to your needs and click **Update HPA**.

#### Editing YAML
1. On the **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster)** page, click the cluster ID for which a scaling group is to be created.
2. Select **Auto Scaling** > **HorizontalPodAutoscaler**. On the **HorizontalPodAutoscaler** page, click **Edit YAML** in the **Operation** column of the HPA whose configuration is to be updated.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/e9zP324_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223165911.png)
3. On the **Edit YAML** page, edit parameters as needed and click **Complete**.


[](id:IndicatorType)
## Metric Type
For more information on metrics and types, see [HPA Metrics](https://intl.cloud.tencent.com/document/product/457/34025).



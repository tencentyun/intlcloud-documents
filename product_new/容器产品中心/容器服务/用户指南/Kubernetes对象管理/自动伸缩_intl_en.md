## Operation Scenario
Horizontal Pod Autoscaler (HPA) can automatically scale the number of pods for services according to the average CPU utilization of target pods and other metrics. This document describes how to implement pod autoscaling using the Tencent Cloud TKE console.

## How Does It Work
The HPA backend component pulls the monitoring metrics of the container and pods from Tencent Cloud’s Cloud Monitor every 30 seconds and then does calculations based on the current metric data, the current number of replicas, and the target value of the metric. The results of this calculation are used as the expected number of replicas for services. When the expected number of replicas is not the same as the current number of replicas, HPA will trigger deployment to adjust the number of pod replicas, thereby achieving auto-scaling.
Taking CPU utilization as an example, if there are currently two pods with an average CPU utilization (the current metric data) of 90%, and the target CPU utilization is set to 60% for autoscaling, the number of pods will be automatically adjusted as follows: 90% × 2 / 60% = 3 pods.
>! If you set multiple auto scaling metrics, HPA will separately calculate the target numbers of replicas according to each metric and then take the maximum number to use for auto scaling.

## Considerations
- When the type of metric is selected as **CPU utilization (by request)**, a CPU request must be set up for the container.
- Set a reasonable target for the policy metric. For example, 70% for the container and application, which leaves 30% remaining.
- Keep pods and nodes healthy (avoid frequently recreating pods).
- Ensure that the load balancing you request operate stably.
- The target number of replicas calculated by HPA is allowed to fluctuate within 10%, under which HPA will not adjust the number of replicas.
- If the value of Deployment.spec.replicas corresponding to the service is 0, HPA will not take effect.
- If multiple HPAs are simultaneously bound to a single deployment, then the HPAs created will take effect simultaneously, which will cause clusters to be repeatedly scaled.

##  Prerequisites
- Complete [Tencent Cloud account registration](https://intl.cloud.tencent.com/register).
- Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
- Create a cluster. For details on how to create a cluster, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637).



## Steps

### Enable Auto Scaling
Auto scaling can be enabled using the following three methods.

### Setting the Number of Pods
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the cluster ID for which the scaling group is to be created, and go to the Deployment page. Select **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/c6d54e147a7b2e0e789781a9b743b30b.png)
3. Set up the number of pods on the **Create Workload** page as **Auto adjustment**. See the figure below:
![](https://main.qcloudimg.com/raw/3d7e13d6372ee8f5f657ce9f524c362a.png)
 - **Trigger policy**: The policy metrics that the auto scaling feature relies on. For details, see [Metric Type](#MetricType).
 - **Pod range**: Select this according to your specific requirements. The number of pods will be auto adjusted within the pre-set range and will not exceed this pre-set range.

#### Creating Auto Scaling Group
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the cluster ID for which the scaling group is to be created, and go to the Deployment page. Select **Auto Scaling**.
3. Click **Create** on the **HorizontalPodAutoscaler** page. See the figure below:
![](https://main.qcloudimg.com/raw/462b1796da9e8f8ccc45c33415fe6b61.png)
4. Configure HPA on the **Create HPA** page according to the following instructions. See the figure below:
![](https://main.qcloudimg.com/raw/585e9028065458d53c303ef0ede1fed7.png)
 - **Name**: Enter the name of the auto scaling group to be created.
 - **Namespace**: To be selected based on your requirements.
 - **Associate deployment**: This cannot be left blank. To be selected according to your specific requirements.
 - **Trigger policy**: The policy metrics that the auto scaling feature relies on. For details, see [Metric Type](#MetricType).
 - **Pod range**: Select this according to your specific requirements. The number of pods will be auto adjusted within the pre-set range and will not exceed this pre-set range.
4. Click **Create HPA** to complete the process of creating the HPA.

### YAML Creation
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the cluster ID for which the scaling group is to be created, and go to the Deployment page.
3. Click **YAML-created Resources** at the top right corner of the page. See the figure below:
![](https://main.qcloudimg.com/raw/1cb1fa4df085a3f6f76a789adbd058e0.png)
4. Edit the contents on the **YAML-created Resources** page according to your specific requirements and click **Complete** to create the HPA. 


### Updating Auto Scaling Rules
The service auto scaling rules can be updated using the following three methods.

#### Updating the Number of Pods
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Select the cluster ID for which the scaling group is to be created, and go to the Deployment page. Click **Update Number of Pods**. See the figure below:
![](https://main.qcloudimg.com/raw/09d6825bb349718712d8b94843a96cf9.png)
3. Change the settings according to your specific requirements on the **Update Number of Pods** page and click **Update Number of Pods**. See the figure below:
![](https://main.qcloudimg.com/raw/2291d0a52e3cb84791b5b7657b629919.png)

#### Modifying HPA Configuration
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Select the cluster ID for which the scaling group is to be created, and go to the workload deployment details page. Select **Auto Scaling**.
3. Click **Modify Configuration** to the right of the row of the HPA that needs to have its configuration updated on the HorizontalPodAutoscaler page.
![](https://main.qcloudimg.com/raw/d0e498827dd05a95a095634411791a8b.png)
3. Change the settings according to your specific requirements on the **Update HPA Configuration** page and click **Update HPA**. See the figure below:
![](https://main.qcloudimg.com/raw/47aa6413af8e046d4ccb053aa37856d6.png)

#### Editing YAML
1. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the **Cluster Management** page.
2. Click on the cluster ID for which the scaling group is to be created, and select **Auto Scaling**.
3. In **HorizontalPodAutoscaler** page, locate the  HPA to update, click **Edit YAML**.
![](https://main.qcloudimg.com/raw/9eeec0fbf70fdc27f57fb5812b85e88c.png)
3. Edit the contents according to your requirements on the **Update HorizontalPodAutoscaler** page and click **Complete**.


<span id="MetricType"></span>
## Metric Type

### CPU Metric
| Metric | Unit | Description |
|----------------|---------|------------------------------------------------------|
| CPU usage |  Core | Pod’s CPU usage |
|CPU utilization (by node) |  %  | Ratio of pod’s CPU usage to total CPU of node  |
|CPU utilization (by requests)| % | Ratio of pod’s CPU usage to the set Request value |
|CPU utilization (by limit)|  %  | Ratio of pod’s CPU usage to the set Limit value|

### Memory
| Metric | Unit | Description |
|----------------|---------|------------------------------------------------------|
| Memory usage |  B | Pod’s memory usage (including cache) |
| Memory usage (exclude cache) | B | The actual memory usage of all containers in the pod (not including cache)|
| Memory utilization (% node)| %  | Ratio of pod’s memory usage to the total node memory |
| Memory utilization (% node, exclude cache)| % |Ratio of the actual memory usage (not including cache) of all containers in the pod to total nodes|
| Memory utilization (% request) | %  | Ratio of pod’s memory usage to the set Request value |
| Memory utilization (% request, exclude cache)| % | Ratio of actual memory usage (not including cache) of all containers in the pod to the set Request value |
| Memory utilization (% limit)|  %  | Ratio of pod’s memory usage to the set Limit value|
| Memory utilization (% limit, exclude cache)| % | Ratio of actual memory usage (excludeing cache) of all containers in the pod to the set Limit value |

### Disk
| Metric | Unit | Description |
|----------------|---------|------------------------------------------------------|
| Disk write traffic | KB/s | Pod’s disk write speed |
| Disk read traffic | KB/s | Pod’s disk read speed |
| Disk read operations | op/s | Number of times that the pod reads data from a disk  |
| Disk write operations | op/s | Number of times that the pod writes data into a disk |

### Networking
| Metric | Unit | Description |
|----------------|---------|------------------------------------------------------|
| Network inbound bandwidth | Mbps | Sum of pod’s inbound bandwidth |
| Network outbound bandwidth | Mbps | Sum of pod’s outbound bandwidth |
| Network inbound traffic | KB/s | Sum of pod’s inbound traffic |
| Network outbound traffic | KB/s | Sum of pod’s outbound traffic |
| Network inbound packets | Each/s | Sum of pod’s inbound packets |
| Network outbound packets | Each/s | Sum of pod’s outbound packets |

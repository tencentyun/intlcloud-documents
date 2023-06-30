
## Overview
TKE cost optimization tool supports the analysis of resource utilization and range distribution of users’ node resources. The analysis objects include CVMs, TKE nodes, etc. With the cloudification maturity models, it can provide cost optimization suggestions to improve resource utilization, help enterprises easily migrate to the cloud, reduce costs, and increase efficiency.

<dx-alert infotype="explain" title="">
For details on the utilization of cluster node resources, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
</dx-alert>



## Maturity Model of Resource Utilization
Tencent Cloud native team researches the authorized customer data, analyzes the resource utilization during the cloudification, and makes the following conclusions: making full use of auto scaling is one of the key points to improve resource utilization and reduce resource costs. Compared with the case where auto scaling is not used, the overall resource utilization can be increased by more than 20-30%. Tencent Cloud native team provides a maturity model of containerization resource utilization, as shown in the following figure:
![](https://main.qcloudimg.com/raw/3a1761406fd958a326bf83a7e4c8b73c.png)

#### First stage
The service adopts the traditional deployment model. In order to cope with the computing resources differences in different periods, users must purchase the infrastructures with the peak resources usage and a certain amount of buffer. The average utilization rate is reduced.

#### Second stage
The service has completed a simple containerization transformation. After being migrated to the cloud and containerized, it can use the containers for hybrid service deployment, which improves the resource utilization.

#### Third stage
The service has performed a microservice transformation. It can use the auto scaling of containers and cloud, and combine with Kubernetes' HPA, VPA, CA and other capabilities to scale out in the peak hours and scale in during idle time, greatly improving the resource utilization.

#### Fourth stage
The service can make full use of the auto scaling capability of the cloud and containerization, and improve the sensitivity and accuracy of auto scaling. Meanwhile, online and offline hybrid deployments are supported. The average resource utilization rate is greatly increased.


## Resource Utilization Analysis
Through the average CPU utilization, high CPU utilization nodes (TOP 10), low CPU utilization nodes (TOP 10), CPU utilization distribution, and other charts, you can have a better understanding of the resource usage of the company's business. The following is a sample chart of resource utilization analysis:

#### Average CPU usage
![](https://main.qcloudimg.com/raw/4c1f8302528059b5cc055b527253e700.png)

#### High CPU utilization/low CPU utilization nodes
![](https://main.qcloudimg.com/raw/064a3e4d11211daf0e6523347b739599.png)

#### CPU utilization distribution pie chart
![](https://main.qcloudimg.com/raw/f5a3df74f8d61b13236be0d12332b712.png)

## Cost Optimization Suggestions
Based on your business characteristics, it can match the typical cost waste phenomenon, and give the cost optimization suggestions to solve the waste phenomenon.

### Periodic business
#### Business characteristics
The business traffic has periodicity, and resources are usually applied for based on the peak value. The utilization is very low when the service load is low. Although the auto scaling (in minute-level) is configured, the optimization space is also limited.

#### Cost optimization suggestions
- After the containerization of the service, it can effectively improve resource utilization while ensuring the stability of the business based on the K8s scheduling and orchestration capabilities, and resource management.
- Scheduled auto scaling solutions
 - cronHPA (Horizontal Pod Autoscaler): when the user-defined time is reached, the Pods will be automatically scaled in or out within 30 seconds.
 - CA (Cluster Autoscaler): when the Pod is pending due to the restriction of node resources, the node-level scaling out and in will be triggered.
 - For traffic surges in a short period, the TKE cluster supports auto scaling of the EKS Pods (Elastic Kubernetes Service) in seconds. You do not need to purchase other nodes.

#### Schematic diagram of cost optimization tool
![](https://main.qcloudimg.com/raw/c2cd6a3d2876a914eef8ee2d4f0f5faf.png)

### Business with surge traffic

#### Business characteristics
The business traffic may surge at any time. In order to ensure business stability and good performance during the peak hours, a large buffer is reserved for resource specification configuration, which causes a huge waste of resources in daily running.

#### Cost optimization suggestions
- Business containerization transformation
 - Based on the K8s scheduling and orchestration capability, it supports dynamic scheduling according to the real load of the Pod to improve node resource utilization.
 - With intelligent resource management, intelligent request recommendation, Resource Quote, and Limit Ranges, it can effectively improve resource utilization while ensuring business stability.
- Auto scaling solutions
 - HPA (Horizontal Pod Autoscaler): when the user-defined threshold is reached (such as the CPU utilization and CPU usage), the Pods will be automatically scaled in or out within 30 seconds.
 - CA (Cluster Autoscaler): when the Pod is pending due to the restriction of node resources, the node-level scaling out and in will be triggered.
 - For traffic surges in a short period, the TKE cluster supports auto scaling of the EKS Pods (Elastic Kubernetes Service) in seconds. You do not need to purchase other nodes.

#### Schematic diagram of cost optimization tool
![](https://main.qcloudimg.com/raw/a5d04afcf9fa958d88e3aaaa4f45c851.png)




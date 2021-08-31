



## Overview

Horizontal Pod Autoscaler (HPA) for Kubernetes pods can automatically adjust the number of pod replicas based on CPU usage, memory usage, and other custom metrics to match the overall level of workload services to the user-defined target value. This document introduces the HPA feature of TKE and describes how to use this feature to achieve automatic scaling of pods.

## Use Cases

The HPA feature provides TKE with flexible self-adaptation capabilities, allowing it to quickly increase the number of pod replicas within the user-defined scope to cope with a sudden increase in service loads and then scale in when service loads decrease to save computing resources for other services. The entire process is automatic and requires no manual intervention. It’s suitable for service scenarios with large service fluctuations, a large number of services, and frequent scaling, such as e-commerce services, online education, and financial services.

## Principle Overview

The HPA feature is implemented by Kubernetes API resources and the controller. Resources use metrics to determine the behavior of the controller, whereas the controller periodically adjusts the number of replicas of service pods based on pod resource usage. This matches the level of workloads to the user-defined target value. The following figure shows the scaling process:
>! The automatic horizontal scaling for pods does not apply to objects that cannot be scaled, such as DaemonSet resources.

![hpa](https://main.qcloudimg.com/raw/3049a13a7f4e5446e989a5d64826d6ea.png)
Key content:
- **HPA Controller**: the control component that controls the HPA scaling logic.
- **Metrics Aggregator**: normally, the controller obtains metric values from a series of aggregation APIs (`metrics.k8s.io`, `custom.metrics.k8s.io`, and `external.metrics.k8s.io`). The `metrics.k8s.io` API is usually provided by the Metrics server. The community edition can provide the basic CPU and memory metric types. Compared with the community edition, the custom Metrics Server collection used by TKE supports a wider range of HPA metric trigger types, providing relevant metrics such as CPU, memory, disk, network, and GPU metrics. For more information, see [TKE Auto-scaling Metrics](https://intl.cloud.tencent.com/document/product/457/34025).
>? The controller can also obtain metrics from Heapster. However, starting from Kubernetes 1.11, the controller can no longer obtain metrics from Heapster.

- **HPA Algorithm for Calculating the Target Number of Replicas**: for the TKE HPA scaling algorithm, see [How It Works](https://intl.cloud.tencent.com/document/product/457/32424). For more detailed algorithm information, see [Algorithm Details](https://kubernetes.io/zh/docs/tasks/run-application/horizontal-pod-autoscale/#algorithm-details).

## Prerequisites

- You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register).
- You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2).
- You have created a TKE cluster. For more information about how to create a TKE cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions
### Deploying test workloads

Here, we use a Deployment-type workload as an example. Create an odd number of replicas, with the service type set to the "test" workload of the web service. For more information about how to create a Deployment-type workload on the TKE console, see [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).
The following figure shows the creation result in this example: 
![image-20201105173748658](https://main.qcloudimg.com/raw/fcf3e06cc63523b8a3a0ca58797c5786.png)

### Configuring HPA 

On the TKE console, bind the test workload with an HPA configuration. For more information about how to bind an HPA configuration, see [HPA Directions](https://intl.cloud.tencent.com/document/product/457/32424). As an example, this document describes the configuration of a policy under which scale-out is triggered when the network egress bandwidth reaches 0.15 Mbps (150 Kbps), as shown in the figure below:
![image-20201106155539282](https://main.qcloudimg.com/raw/f48e8de9ba6cfd4d2fa1a26135cf2c34.png)

### Feature verification
#### Simulating the scale-out process
Run the following command to launch a temporary pod in the cluster to test the configured HPA feature (simulated client):
```bash
kubectl run -it --image alpine hpa-test --restart=Never --rm /bin/sh
```
Run the following command in the temporary pod to simulate a situation where large numbers of requests accessing the "hpa-test" service in a short period cause the egress traffic bandwidth to increase:
```bash
# hpa-test.default.svc.cluster.local is the domain name of the service in the cluster. To stop the script, press Ctrl+C.
while true; do wget -q -O - hpa-test.default.svc.cluster.local; done   
```
After running the request simulation command in the test pod, observe the monitored number of pods of the workload. You will see that the number of replicas for the workload increase to 3 at 18:46, which indicates that an HPA scale-out event was been triggered, as shown in the figure below:
![image-20201106164540791](https://main.qcloudimg.com/raw/09348b121a1c2b18bcf993d5e26dae2d.png)
Then, through the monitoring of the network egress bandwidth of the workload, you can see that, at 16:21, the network egress bandwidth increased to about 424 Kbps, exceeding the target value of the network egress bandwidth set by HPA. This further indicates that the HPA [Scaling Algorithm](https://intl.cloud.tencent.com/document/product/457/32424) has been triggered to add a replica to meet the set target value. Therefore, the number of replicas of the workload has changed to 3, as shown in the figure below:

>! The HPA [Scaling Algorithm](https://intl.cloud.tencent.com/document/product/457/32424) does not just rely on formula calculation to control the scaling logic but takes multiple dimensions into consideration to decide whether scale-out or scale-in is needed. Therefore, the actual implementation may differ slightly from expectations. For more information, see [Algorithm Details](https://kubernetes.io/zh/docs/tasks/run-application/horizontal-pod-autoscale/#algorithm-details).

![image-20201106165107310](https://main.qcloudimg.com/raw/f88174b70e9251abcf81f9d1ba82192f.png)

 #### Simulating the scale-in process

When simulating the scale-in process, manually stop executing the request simulation command at about 18:49. Through monitoring, you can observe that the network egress bandwidth decreases to the level before scale-out. At this time, according to the HPA logic, the conditions for workload scale-in are met, as shown in the figure below:
![image-20201106165205910](https://main.qcloudimg.com/raw/d82036dc4b3815d53c1df38ebdbdc53c.png)
However, according to the monitoring of the number of workload pods shown in the figure below, the workload did not trigger HPA scale-in until 18:55. This is because, after HPA is triggered, there is a default 5-minute toleration time algorithm to prevent frequent scaling operations caused by metric fluctuations within a short period of time. For more information, see [Cooling/Delay Support](https://kubernetes.io/zh/docs/tasks/run-application/horizontal-pod-autoscale/#%E5%86%B7%E5%8D%B4-%E5%BB%B6%E8%BF%9F%E6%94%AF%E6%8C%81). As shown in the figure below, 5 minutes after the command was stopped, the number of workload replicas was decreased back to the initial setting of 1 replica according to the HPA [Scaling Algorithm](https://intl.cloud.tencent.com/document/product/457/32424).
![image-20201106164648921](https://main.qcloudimg.com/raw/6b502fcc13ebe69262aa989300d97e6e.png)
When an HPA scaling event occurs in TKE, the event will be displayed in the event list of the corresponding HPA instance. Note that the time on the event notification list includes "First Occurrence Time" and "Last Occurrence Time". "First Occurrence Time" indicates the first time when the same event occurred, while "Last Occurrence Time" indicates the latest time when the same event occurred. Therefore, as you can see in the event list shown in the figure below, the "Last Occurrence Time" field displays 18:46:01 for the scale-out event in this example and 18:54:40 for the scale-in event. The points in time displayed here match those in the workload monitoring.
![image-20201106164245358](https://main.qcloudimg.com/raw/869ff57ed157324a1e0ee7680bfaf8fd.png)
In addition, the workload event list also records the events of adding/deleting replicas by workloads when HPA occurs. As shown in the figure below, the points in time of workload scale-out and scale-in match those displayed in the HPA event list. The point in time when the number of replicas increased is 18:46:01, and the point in time when the number of replicas decreased is 18:54:40.
![image-20201106164329173](https://main.qcloudimg.com/raw/95acba9dc8190f597cdaecba8ac98dcd.png)



## Summary

This example demonstrates the HPA feature of TKE and shows how to use the TKE custom metric type network egress bandwidth as the metric for triggering workload HPA scaling.
 - When the actual metric value of the workload exceeds the target metric value configured by HPA, HPA calculates the proper number of replicas according to its scale-out algorithm and implements scale-out. This ensures that the metric levels of the workload meet expectations and that the workload can run in a healthy and stable manner.
 - When the actual metric value of the workload is far lower than the target metric value configured by HPA, HPA waits until the toleration time expires and then calculates the proper number of replicas to implement scale-in and release idle resources. This improves resource utilization. Moreover, throughout the process, relevant events are recorded in the HPA and workload event lists so that the whole workload scaling process is traceable.

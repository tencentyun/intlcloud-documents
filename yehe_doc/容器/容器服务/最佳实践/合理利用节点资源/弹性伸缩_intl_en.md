This document describes how to use auto scaling, so that services can make full use of available resources based on actual production experience. You can adjust your configurations based on this document.

## Coping Abrupt Traffic Spikes
Typically, services have peak and off-peak hours of resource usage. To properly use resources, you can define a Horizontal Pod Autoscaler (HPA) for services to automatically scale out the number of pods during peak hours and scale in the number of pods during off-peak hours. For example, when the traffic of online services is low at night, the HPA can automatically release resources of online services and use them for big data offline tasks.


To use the HPA, you need to install resource metrics (metrics.k8s.io) or custom metrics (custom.metrics.k8s.io) in advance. The HPA controller can then query related APIs to obtain resource use information for services. In this way, Kubernetes obtains resource usage data (metric data) of services in advance.
Previously, the HPA used resource metrics to obtain metric data. After custom metrics became available, the HPA used more flexible metrics to control scaling. To implement HPA, Kubernetes uses metrics-server, communities use prometheus-adapter, and cloud vendors that manage Kubernetes clusters usually use their own APIs. For example, TKE uses HPA to implement CPU, memory, hard disk, and network metrics. You can create an HPA on the web client and convert the metrics to a Kubernetes YAML file, as shown below:
```
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx
spec:
  scaleTargetRef:
    apiVersion: apps/v1beta2
    kind: Deployment
    name: nginx
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Pods
    pods:
      metric:
        name: k8s_pod_rate_cpu_core_used_request
      target:
        averageValue: "100"
        type: AverageValue
```

### Reducing costs
HPA implements horizontal pod scaling. When node resources are insufficient, scaled-out pods are in the pending state. If a large number of nodes are prepared in advance, pending pods will not occur, but the cost will be high.
Typically, Kubernetes clusters managed by cloud vendors support cluster-autoscaler. This means nodes can be dynamically added or deleted based on resource usage to maximize computing resource utilization. In addition, pay-as-you-go is used to reduce the cost. For example, TKE uses scaling groups and extended features that contain scaling groups (node pools).


### Using vertical scaling 
For applications that do not support horizontal scaling or applications with uncertain optimal request and limit ratios, you can use VPA for vertical scaling. In this case, the request and limit values are automatically updated, and pods are restarted. This feature may cause service unavailability for a short period. We do not recommend you use it on a large scale in the production environment. 

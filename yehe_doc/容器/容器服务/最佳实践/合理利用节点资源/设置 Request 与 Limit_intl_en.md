The request and limit parameters of a container need to be flexibly set based on the service type, your requirements, and the relevant scenario. This document describes how to set request and limit based on actual production experience. You can adjust your configurations based on this document.



## How Request Works
The request value does not represent the size of the resources actually assigned to the container, but is a reference value provided to the scheduler. The scheduler detects the resources on each node that can be assigned (assignable node resources = total amount of node resources - sum of requests scheduled to containers in all Pods on the node) and records the assigned resources on each node (sum of requests scheduled to containers defined in all Pods on the node). If the amount of assignable node resources is smaller than the sum of requests in a Pod that needs to be scheduled, the Pod will not be scheduled to the node; otherwise, it will be scheduled to the node.

If request is not configured, the scheduler cannot perceive node resource usage to make correct scheduling decisions. As a result, scheduling may not be rational, resulting in chaotic node statuses. We recommend that you set request for all containers to enable the scheduler to perceive node resource usage and make proper scheduling decisions. In this way, node resources in a cluster can be properly allocated, and faults caused by uneven resource allocation can be prevented.




## Setting Default Request and Limit Values
You can use LimitRange to set the default, minimum, and maximum request and limit values for a namespace, as shown below:
```
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
  namespace: test
spec:
  limits:
  - default:
      memory: 512Mi
      cpu: 500m
    defaultRequest:
      memory: 256Mi
      cpu: 100m
    type: Container
```


## Setting Request and Limit Values for Important Online Applications
When node resources are insufficient, pods of low priorities will be deleted automatically to release node resources. The following lists pods with priorities in ascending order:
1. Pods with no request or limit values
2. Pods with different request and limit values
3. Pods with the same request and limit values

We recommend that you set the same request and limit values for important online applications to ensure a high pod priority. When a node fault occurs, these applications will not be affected because the pods used for these applications are generally not deleted.



## Improving Resource Utilization
If a large request value is set for an application but the occupied resource amount of the application is much less than the preset value, resource utilization of the node is low.

Except for services that are sensitive to latency, we recommend that you lower the request value for non-core applications that do always need resources in order to improve resource utilization. Services that are sensitive to latency do not expect high node resource utilization because it affects the packet sending and receiving speeds. If your service supports horizontal scale-out, the request value for a single replica is usually set to less than one core, except for CPU-intensive applications. For example, the request value of CoreDNS can be set to 0.1 core, which indicates 100 MB.


## Preventing Large Request and Limit Values
If your service uses a single replica or a few replicas and the request and limit values are large, sufficient resources will be allocated to your service. However, when a replica encounters a fault, your service will be greatly affected. When the node where the pod resides is faulty, other nodes do not have sufficient resources to meet the pod request because the request value is large and cluster resources are allocated in a fragmented manner. As a result, the pod cannot be shifted or recovered. 

We recommend that you set small request and limit values and scale out replicas to ensure that your service is more flexible and reliable.



## Preventing High Resource Consumption by the Test Namespace


If a production cluster contains a test namespace and the request and limit values of the namespace are not restricted, the cluster may be overloaded and production services could be affected. You can use `ResourceQuota` to restrict the request and limit values of the test namespace, as shown below:
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: quota-test
  namespace: test
spec:
  hard:
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```

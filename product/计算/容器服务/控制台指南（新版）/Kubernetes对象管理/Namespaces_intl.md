A Namespace is the object of logical environment division in the same cluster in Kubernetes. You can manage the division of multiple teams or projects using Namespaces. In a Namespace, the name of a Kubernetes object must be unique. You can use ResourceQuotas to allocate available resources and control the access to different Namespace networks.

## How to Use

- Use in the TKE console: You can add, delete, change, and query Namespaces in the TKE console.
- Use with kubectl: For more information, see [Kubernetes' official documentation](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/).

## Setting Usage Quota of a Namespace Resource with a ResourceQuota

You can have multiple ResourceQuota resources under one Namespace, and each ResourceQuota can set usage constraints for each Namespace resource. You can set the following usage constraints for Namespace resources:
- Compute resource quotas, such as CPU and memory.
- Storage resource quotas, such as total storage of requests.
- Kubernetes object count quotas, such as the number of Deployments.

The quota settings supported by ResourceQuota vary slightly by Kubernetes version. For more information, see [Kubernetes' official document about ResourceQuota](https://kubernetes.io/docs/concepts/policy/resource-quotas/).
Below is an example of ResourceQuota:
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: object-counts
  namespace: default
spec:
  hard:
    configmaps: "10"  ## Up to 10 ConfigMaps
    replicationcontrollers: "20" ## Up to 20 ReplicationControllers
    secrets: "10" ## Up to 10 Secrets
    services: "10" ## Up to 10 Services
    services.loadbalancers: "2"  ## Up to 2 Services in LoadBalancer mode
    cpu: "1000" ## Up to 1,000 CPU resources can be used under this Namespace
    memory: 200Gi ## Up to 200 Gi of memory can be used under this Namespace
```

## Setting Access Control for a Namespace Network Using a NetworkPolicy

NetworkPolicy is a resource provided by Kubernetes (K8s) to define a Pod-based network isolation policy. You can not only restrict Namespaces, but also control network access among Pods, i.e., controlling whether a group of Pods can communicate with another group or other network endpoints.

For details about how to deploy a NetworkPolicy Controller in a cluster and implement network access control among Namespaces using a NetworkPolicy, see [Using NetworkPolicy for Network Access Control](https://cloud.tencent.com/document/product/457/19793).


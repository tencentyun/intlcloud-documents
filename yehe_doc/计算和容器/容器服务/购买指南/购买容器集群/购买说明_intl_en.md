
### Purchase Notes

>? If the service is unavailable due to the failure of you to abide by the following suggestions, the corresponding service downtime shall not be counted towards the service unavailability period. For more information, see [TKE Service Level Agreement](https://intl.cloud.tencent.com/document/product/457/12356).

The availability of TKE clusters are relevant to the number of resources (such as Pod, ConfigMap, CRD and Event) in the cluster, as well as QPS of Get/List read operations and Patch/Delete/Create/Update write operations of the resources. To improve the cluster availability, do not initiate List-like operations for clusters with large amount of resources, and do not write too many ConfigMap/CRDs/EndPoints into the cluster.

The common **List-like operations** are as follows (take Pod resources as an example):
- Query with a label
```
kubectl get pod -l app=nginx
```
- Query for a specified namespace
```
kubectl get pod -n default
```
- Query the Pods across the cluster
```
kubectl get pod --all-namespaces
```
- Initiate a List request through client-go
```
k8sClient.CoreV1().Pods("").List(metav1.ListOptions{})
```

If you want to **query all resources in the cluster**, it is recommended that you use the **informer mechanism** to query through local cache. In some simple scenarios, you can add the ResourceVersion parameter in List to query in kube-apiserver cache. For example, `k8sClient.CoreV1().Pods("").List(metav1.ListOptions{ResourceVersion: "0"})`. Note: When you query in kube-apiserver cache, if you initiate List requests frequently to many resources, it still causes high pressure on kube-apiserver memory. It is recommended that you use this query method for low-frequency requests.

### Recommended Configuration
Refer to the recommended configuration below and choose the model that best suits your requirements, so as to prevent cluster unavailability caused by heavy load of the control plane.
Assume that you want to deploy 50 nodes in a cluster and need 2,000 Pods. You need to select a model with the maximum number of nodes of 100, but not 50.
>? 
>- The nodes indicate Kubnernetss nodes, including CVM nodes, BM nodes and external nodes. **Supernodes are excluded**.
>- The number of Pods includes Pods in all namespaces and in any status, and excludes the Pods related to system components such as cni-agent.
>- ConfigMap does not include the Pods related to system components such as cni-agent.
> - **Maximum other resources** refers to the number of resources in the manged cluster excluding the Pods, nodes and ConfigMap. For example, for a L100 cluster, the number of the resources, such as ClusterRole, Services and Endpoints, cannot exceed 2,500 respectively.
>- It is recommended that the size of all objects under each type of resource does not exceed 800 MiB, and the size of each object does not exceed 100 KB.
>

| Cluster specification | Max nodes | Max Pods (recommended) | Max ConfigMap (recommended) | Maximum CRDs/Maximum other resources (recommended) | 
| ---------------- | ------------------- | ------------------------- | ------------------- |------------------- |
| L5           | 5                | 150                 | 128                        | 150                 | 
| L20           | 20               | 600                 | 256                       | 600                 |
| L50 | 50               | 1,500                | 512                     | 1,250                |
| L100   | 100              | 3,000                | 1,024                    | 2,500                |
| L200     | 200              | 6,000                | 2,048                    | 5,000                |
| L500 | 500              | 15,000               | 4,096                   | 10,000               |
| L1000 | 1,000             | 30,000               | 6,144                     | 20,000               |
| L3000  | 3,000             | 90,000               | 8,192                  | 50,000              |
| L5000 | 5,000             | 150,000              | 10,240                     | 100,000              |

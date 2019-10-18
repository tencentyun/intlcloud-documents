New console is now supported in all regions. Follow the steps below to access the new console.
1. Access [new console](https://console.qcloud.com/tke2) directly.
2. Log in to [Tencent Cloud console](https://console.cloud.tencent.com) and select **Cloud Products** > **Compute** > **Tencent Kubernetes Engine** to enter the TKE Overview page.
![](https://main.qcloudimg.com/raw/748c11e287af0a3379135a2a1a8d3c25.png)
>
>- To provide you with better service, TKE released a new version of console on Jun 17, 2019. The new console is compatible with native Kubernetes. The old TKE console will stop service in a near future.
>- Features on the new and old consoles are compatible. You can switch between using either one without affecting your business. You can use the new console to continue operations on existing TKE clusters.
>- We recommend using the new TKE2 console. If you have any questions about the new console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1).
>
The new TKE2 console provides you with a more native and easy-to-use platform. Not only does the new console help you build managed/self-deployed clusters and custom node images, set workload affinity scheduling, and other basic operations, it also provides monitoring services like event and metric monitoring, comparative monitoring, self-deployed cluster Master & Etcd monitoring, etc. See below for a detailed comparison of the features of the new and old consoles.

## Comparison of New and Old Console Features
| Feature                         | New Console TKE2 (Recommended) | Old Console TKE |
| --------------------------- | ------------- | -------- |
| Basic Cluster CRUD                   | Supported            | Supported       |
| Managed/Self-deployed Cluster Modes                | Supported            | Not Supported      |
| Basic Node CRUD                    | Supported            | Supported       |
| Node Drain and Cordon                   | Supported            | Supported       |
| Custom Node Image                     | Supported            | Not Supported      |
| Cluster Scaling Group Management                  | Supported            | Supported       |
| In-cluster Workload Management                   | Supported            | Limited Support     |
| Workload Affinity Scheduling                   | Supported            | Not Supported      |
| In-cluster Service & Ingress Management       | Supported            | Limited Support     |
| Services Support Using Existing LBs             | Supported            | Not Supported      |
| Service LBs Bind Only w/Certain Nodes | Supported            | Limited Support     |
| In-cluster Configuration Management (`configmap`, `secret`)   | Supported          | Not Supported      |
| Cluster Storage Management                    | Supported            | Not Supported      |
| View In-cluster K8s Resource Logs                 | Supported            | Limited Support     |
| View In-cluster K8s Resource Events                | Supported            | Limited Support     |
| Image Registry               | Supported            | Supported       |
| Application Management (Application Templates + Configuration Items) | Recommended to use Helm    | Limited Support     |
| Template Market                   | Helm Recommended      | Limited Support     |
| Log Collection Features                      | Supported            | Limited Support     |
| Alarm Configuration Features                      | Supported            | Not Supported      |
| Event Persistence                       | Supported            | Not Supported      |
| Use Existing CVMs to Create Clusters          | Supported            | Not Supported      |
| View Node K8s Properties           | Supported            | Not Supported      |
| Event/Metric Monitoring                      | Supported            | Limited Support     |
| Comparative Monitoring                        | Supported            | Not Supported      |
| Self-deployed Cluster Master & Etcd Monitoring           | Supported            | Not Supported      |

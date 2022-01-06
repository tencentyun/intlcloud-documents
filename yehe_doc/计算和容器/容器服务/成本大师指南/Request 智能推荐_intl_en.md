
## Request Recommendation
>? The Request Recommendation feature is currently in beta. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
### Description

Kubernetes can effectively improve business orchestration capability and resource utilization rate. However, the improvement is very limited if it is not supported by additional capabilities. According to [Kubernetes Standards for Cost Reduction and Efficiency Enhancement | Analysis of Containerized Computing Resource Utilization Rate](https://mp.weixin.qq.com/s/8sHsI1pVm-1RX5w1F3uWPg), which is the statistics provided by the TKE team, the average utilization rate of the TKE nodes is only about 14%. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/752008abf44f7387482cb40b9a1fbafc.png)


Why the utilization rate of the Kubernetes clusters resources is still low? It is mainly because of the resource scheduling logic of the Kubernetes. When a Kubernetes workload is created, the "Request" and "Limit" of resources usually need to be configured to indicate the occupancy and limitation for the resources, and the utilization rate is affected most by "Request". To prevent the resources used by their workloads from being occupied by other workloads, or to cope with high demands on resources during peak traffic, users usually set a high value for "Request". Therefor, there is difference between the set value of "Request" and the actual usage. In addition, the resources corresponding to the difference cannot be used by other workloads, and this causes waste. A high value of "Request" is a common reason that causes low utilization rate of the Kubernetes clusters resources.

Request Recommendation can recommend the values of Request/Limit for resources of Kubernetes workloads at the container level to reduce waste of resources.

### Resource objects deployed in the cluster

The following Kubernetes objects will be deployed in the cluster when Request Recommendation is enabled.

| Kubernetes Object | Type | Required Resources | Namespaces |
| ----------------------------- | ------------------ | --------------------- | --------------- |
| v1beta1.recommendation.tke.io | APIService         | -                    | -               |
| recommendation-server         | ClusterRole        | -                     |-              |
| recommendation-server         | ClusterRoleBinding |-                     | -               |
| recommendation-server         | Service            | -                    | kube-system     |
| recommendation-server         | ServiceAccount     | -                     | kube-system     |
| recommendation-server         | Deployment         | CPU: 250m; Mem: 512Mi | kube-system     |


## Feature Description

  - It supports recommending suitable Request/Limit values of resources for each container in Deployment, StatefulSet and DaemonSet.
  - It supports quick updating the resource values for containers in the workload with recommended values.
  - It supports maintaining the ratio of Request/Limit. The recommended Request/Limit maintains the original ratio of Request/Limit set to the containers in the workload. If no value of "Limit" is set at the time of workload creation, no value will be recommended for "Limit".



## Notes

#### Environment requirements

Kubernetes version: 1.10+


#### Node requirements
X86. ARM model is not supported

#### Requirement on resource to be controlled

- It supports Deployment, StatefulSet and DaemonSet.
- It does not support Job and CronJob, as well as the Pods that are not managed by a workload.

#### Thresholds of recommended values

Minimum values: the recommended minimum CPU per Pod is 0.025 core (25m); minimum memory is 100Mi.

>!If a Pod has multiple containers, it is possible that the recommended CPU value per container is less than 0.025, but the recommended minimum value for the Pod is 0.025. The same applies to the memory.



## Directions

### Enabling/Disabling Request Recommendation

1. Log in to the [TKE console](https://console.qcloud.com/tke2).
2. Enter a cluster and click **Basic Information** in the left sidebar to go to the cluster basic information page.
3. Locate **Request Recommendation** and toggle on the switch on the right.


### Using Request Recommendation

When Request Recommendation is enabled, the values will be entered in the column of **Recommended Request** on the pages of Deployment, StatefulSet and DaemonSet under **Workload**, as shown by "1" in the figure below.
>!
> - This feature does not take effect immediately upon enabling. The system will analyze the resource usage history to provide accurate recommended values.
> - The period for calculation is varied depending on the workload. A workload may be affected by another workload in the cluster.
> - After this feature is enabled, values will be recommended for the workloads that run at least for one day.
> - For workloads created after this feature is enabled, it usually takes one day to recommend values.

If the "Request" of the current workload is not reasonable, a red exclamation mark will appear to inform you to adjust the "Request" value manually.

You can hover over the red exclamation mark and click to view the recommended value for "Request", and compare the existing value with the recommended value.


>!After the value of "Request" is updated, the workload will be updated on a rolling basis with the new "Request" value and the Pod will be rebuilt.

You can click "Update" in the red box below to use the recommended value for "Request" to update the original value quickly.



### Obtaining recommended values for the workload via Kubectl

After enabling Request Recommendation, you can view the recommended values for the workload via Kubectl. For more information on Kubectl configuration, see [Connecting to a TKE Cluster](https://intl.cloud.tencent.com/document/product/457/30639).

Sample:
```shell
kubectl get --raw "/apis/recommendation.tke.io/v1beta1/namespaces/default/deployments/<name>"
```

For example:
After enabling Request Recommendation, if you want to access the recommended values for a daemonset with the name of `kube-proxy` in the namespace `kube-system`:
![](https://main.qcloudimg.com/raw/504e5341c7f95319c1615034fabe6664.png)

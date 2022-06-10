
### Overview

Tencent Cloud upgraded the basic monitoring architecture to improve the stability of the TKE basic monitoring and alarming feature. After the upgrade, a DaemonSet named `tke-monitor-agent` is deployed under the `kube-system` namespace in the cluster, and the K8s resource objects of authentication and authorization are created, including ClusterRole, ServiceAccount, and ClusterRoleBinding. These resource objects are all named `tke-monitor-agent`.

### Strengths

This add-on collects the monitoring data of containers, Pods, nodes, and community add-ons. The collected data is used for basic monitoring metrics display, metrics alarming, and metric-based HPA service in the console. By deploying this add-on, you can fix the problem that the monitoring data can't be obtained due to the instability of the basic monitoring service, thereby enjoying more stable monitoring, alarming, and HPA services.

### Impact

- Deploying this add-on does not affect the normal running of the cluster.

- If your **node resources are allocated unreasonably**, **node load is too heavy**, or **node resources are not enough**, deploying the basic monitoring add-on may cause the problem where the Pod corresponding to the `tke-monitor-agent` DaemonSet is in the status of **Pending**, **Evicted**, **OOMKilled** or **CrashLoopBackOff**. The details of the status are as follows:
  - **Pending**: The resources on the cluster node are not enough to schedule a Pod. You can schedule the Pod to the node by setting the quantity of requested resources for the `tke-monitor-agent` DaemonSet to `0`. For more information, see [Pod Remains in Pending](https://intl.cloud.tencent.com/document/product/457/35763).
  - **Evicted**: This status may be caused by insufficient node resources or a heavy load on the node. You can find out the cause and solve the problem in the following ways:
      - Run `kubectl describe pod -n kube-system <podName>` to check the cause according to the description in the `Message` field.
      - Run `kubectl describe pod -n kube-system <podName>` to check the cause according to the description in the `Events` field.
  - **CrashLoopBackOff** or **OOMKilled**: Run `kubectl describe pod -n kube-system <podName>` to check whether an OOM error occurs. If yes, you can increase the value of `memory limits`, which can't exceed 100 MB. If the error still occurs after the value is set to 100 MB, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
  - **ContainerCreating**: Run `kubectl describe pod -n  kube-system <podName>` to check the `Events` field. If `Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create a sandbox for pod "<pod name >": Error response from daemon: Failed to set projid for /data/docker/overlay2/xxx-init: no space left on device` is displayed, the container data disk is full, and you can clear the data disk to restore it.
>? If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

- Quantity of resources consumed in each Pod managed by the DaemonSet (named `tke-monitor-agent`) is positively correlated with the number of Pods and containers running on the node. Below is a sample stress test with low MEM and CPU usage:
**Data volume**
220 Pods are deployed on a node, and each Pod contains three containers.
**Resources consumed**
<table>
<thead>
<tr>
<th align="left">MEM (peak)</th>
<th align="left">CPU (peak)</th>
</tr>
</thead>
<tbody><tr>
<td align="left">About 40 MiB</td>
<td align="left">0.01C</td>
</tr>
</tbody></table>

 - The stress test result of the CPU usage is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/868ec976f40aac5668135fee957b3bdd.png)

 - The stress test result of the memory usage is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/d682d3a56a2b0e2d662f39533bd058e3.png)





### Add-on Description

Tencent Cloud upgraded the basic monitoring structure to improve stability of TKE basic monitoring and alarm service. After the upgrade, a DaemonSet named “tke-monitor-agent” is deployed under the kube-system namespace in the cluster, and the corresponding K8s resource objects related to authentication authorization are created, including ClusterRole, ServiceAccount and ClusterRoleBinding. These resource objects are all named “tke-monitor-agent”.

### Benefits

This add-on collects monitoring data of containers, Pods, nodes and official add-ons. The collected data is used for basic monitoring metrics display, metrics alarm and metric-based HPA service in the console. By deploying this add-on, you can fix the problem where the monitoring data is unable to be obtained due to instability running of basic monitoring service. Therefor, you can obtain more stable monitoring, alarm and HPA service.

### Impacts

- Deploying this add-on does not affect the normal running of cluster.

- If your **node resources are allocated unreasonably**, **node load is too heavy** or **node resources are not enough**, deploying basic monitoring add-on may cause the problem where the Pod corresponding to DaemonSet tke-monitor-agent is in the status of **Pending**, **Evicted**, **OOMKilled** or **CrashLoopBackOff**. The details of the status are as follows:
  - **Pending**: The resources on the cluster node are not enough to schedule a Pod. You can schedule the Pod to the node by setting the quantity of requested resources for DaemonSet tke-monitor-agent to “0”. For more information, see [Troubleshooting Guide for Pods in Pending Status](https://intl.cloud.tencent.com/document/product/457/35763).
  - **Evicted**: This status may be caused by insufficient node resources or heavy load on the node. You can find out the reasons and solve the problem through the following ways:
      - Run `kubectl describe pod -n kube-system <podName>`, and check the reasons through the description in Message field.
      - Run `kubectl describe pod -n kube-system <podName>`, and check the reasons through the description in Events field.
  **CrashLoopBackOff** or **OOMKilled**: Run `kubectl describe pod -n kube-system <podName>` to see if an OOM error occurs. If yes, you can increase the value of memory limits, which cannot exceed 100M. If the error still occurs after the value is set to 100M, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
  - **ContainerCreating**: Run `kubectl describe pod -n  kube-system <podName>` and check the Events field. If `Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create a sandbox for pod "<podName >": Error response from daemon: Failed to set projid for /data/docker/overlay2/xxx-init: no space left on device` is prompted, it indicates that the container data disk is full. You can clear the data disk to restore it.
>? If the problem persists, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>

- Quantity of resources consumed in each Pod managed by the DaemonSet (named “tke-monitor-agent”) has a positive correlation with the number of Pods and containers running on the node. See the figure below for a stress test sample.
**Data volume**
220 Pods are deployed on a node, and each Pod contains 3 containers.
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

 - Stress test result of CPU usage:
![](https://qcloudimg.tencent-cloud.cn/raw/06eb3b094d9f73b164f1b21ba76804d6.png)

 - Stress test result of MEM usage:
![](https://qcloudimg.tencent-cloud.cn/raw/bb86d3cbf10863e4eba541a1bbb893bc.png)




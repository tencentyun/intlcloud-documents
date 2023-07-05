
## Basic Monitoring

### Why is a node assigned more CPU cores and memory than the node resource specification?

**Reason:** CPU cores and memory assigned to a node are calculated based on the CPU and memory requests in each Pod on the node, but the requests of failed Pods are not subtracted in the calculation.

Example. A node's specification is 4-core 8 GB MEM, and three Pods are running on it. Below is the resource request usage:

- Pod 1's requests are two CPU cores and 4 GB memory during normal operations.
- Pod 2's requests are one CPU core and 2 GB memory during normal operations.
- Pod 3 is in **Failed** status, and its requests are 0.5 CPU core and 1 GB memory.

The idle resources on the node are 4 - 2 - 1 = 1 CPU core and 8 - 4 - 2 = 2 GB memory. Pod 4's requests are 0.8 CPU core and 1.5 GB memory, which meets the scheduler's requirements and is scheduled to the node normally. At this point, the node has four Pods, three normal ones and one failed one, and is assigned 4.3 CPU cores and 8.5 GB memory (as the requests of the failed Pod are not subtracted in the calculation, the node specification is exceeded).

This problem was fixed in the new version in May, that is, requests of failed Pods are subtracted during the calculation of the node resources to be assigned.

### Why the Pod status is normal, but the `k8s_workload_abnormal` monitoring metric is abnormal?

**Reason:** The metric status is subject to whether Pods of the workload are normal, and whether a Pod is normal is subject to the four types in `pod.status.condition`. `k8s_workload_abnormal` will be considered normal only when the four metrics are all `True` at the same time; otherwise, it will be considered abnormal.
- PodScheduled: The Pod has been scheduled to a node.
- ContainersReady: All containers in the Pod are ready.
- Initialized: All init containers have completed successfully.
- Ready: The Pod can provide the Service to requests and should be added to the load balancer pool of the corresponding Service.

### Causes of `tke-monitor-agent` DaemonSet errors

<table>
<thead>
  <tr>
    <th>Error</th>
    <th>Cause</th>
    <th>Solution</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>The domain name `receiver.barad.tencentyun.com` failed to be resolved, and the metric failed to be reported, so the cluster didn't have the monitoring data.</td>
    <td>The node DNS was modified.</td>
    <td>Add `hostAlias` to the `tke-monitor-agent` DaemonSet as follows:
```
hostAliases:
- hostnames:
  - receiver.barad.tencentyun.com
  ip: 169.254.0.4
```
</td>
  </tr>
</tbody>
</table>


## Operation Scenario

To deploy applications in TKE and use static pod IP addresses, you can use StatefulSets with static IP addresses. Tencent Cloud TKE supports this type of StatefulSets that create pods with IP addresses in an actual VPC instance assigned through ENIs. TKE’s VPC-CNI plugin assigns IP addresses that do not change after pods are restarted or migrated.
By using StatefulSets with static IP addresses, you can:
- Authorize through source IP addresses.
- Review processes based on IP addresses.
- Query logs based on pod IP addresses.

>Note that when StatefulSets with static IP addresses are used, static IPs survive only within the lifecycle of their StatefulSets.

## Prerequisites

You have enabled the VPC-CNI mode for the cluster. For more information, see [Enabling the VPC-CNI Mode for a Cluster](https://intl.cloud.tencent.com/document/product/457/35250).

## Directions

### Using the console
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and go to the management page of the **[cluster](https://console.qcloud.com/tke2/cluster?rid=1)**.
2. Select the ID or name of the cluster that you want to view to go to the cluster management page.
3. Choose **Workload** > **StatefulSet** to go to the cluster management page of **StatefulSet**.
4. Click **Create** to view **Number of Pods**, as shown below:
![](https://main.qcloudimg.com/raw/0ebc313ec37d0f4dc6506ecbcecd3fc7.png)
5. Click **Advanced Settings** and set the StatefulSet parameters as needed. The key parameters are as follows:
   ![Create a StatefulSet](https://main.qcloudimg.com/raw/fa66910444475fcab224844c200a217c.png)
 - Network mode: select **Use VPC-CNI mode**.
 - IP address range: currently, only the Random value is supported.
 - Static pod IP: select **Enable**.

### YAML sample

```yaml

apiVersion: apps/v1beta1

kind: StatefulSet

metadata:

annotations:

tke.cloud.tencent.com/enable-static-ip: "true"

name: busybox

spec:

serviceName: "busybox"

replicas: 3

template:

metadata:

annotations:

tke.cloud.tencent.com/networks: "tke-route-eni"

labels:

app: busybox

spec:

terminationGracePeriodSeconds: 0

containers:

- name: busybox

image: busybox

command: ["sleep", "10000000000"]

resources:

requests:

tke.cloud.tencent.com/eni-ip: "1"

limits:

tke.cloud.tencent.com/eni-ip: "1"
```

- metadata.annotations: to create StatefulSets with static IP addresses, you need to set annotations, that is, `tke.cloud.tencent.com/enable-static-ip`.
- spec.template.annotations: to create pods in VPC-CNI mode, you need to set annotations, that is, `tke.cloud.tencent.com/networks`.
- spec.template.spec.containers.0.resources: to create pods in VPC-CNI mode, you need to add limits on "requests" and "limits", that is, `tke.cloud.tencent.com/eni-ip`.

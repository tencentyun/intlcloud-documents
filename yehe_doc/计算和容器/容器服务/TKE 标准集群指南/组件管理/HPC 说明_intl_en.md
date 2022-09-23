## Overview

### Add-on description

HorizontalPodCronscaler (HPC) is an add-on to modify the number of replicas of K8s workload. Used in conjunction with HPC CRD resources, it can support scheduled actions in seconds.

### Add-on features

- Configures "Pod Range" (when the associated object is HPA) or "Desired Number of Pods" (when the associated object is Deployment or StatefulSet).
- Sets an “Exceptional Time”. The smallest granularity of the setting is Day. Multiple exceptional times are allowed.
- Specifies whether the scheduled task runs only once.



### Kubernetes objects deployed in a cluster

Deploying HPC Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object | Type | Required Resources | Namespaces |
| ------------------------------------------------------ | ------------------------ | ---------------------- | -------------- |
| horizontalpodcronscalers.autoscaling.cloud.tencent.com | CustomResourceDefinition | - | - |
| hpc-leader-election-role | Role | - | kube-system |
| hpc-leader-election-rolebinding | RoleBinding | - | kube-system |
| hpc-manager-role | ClusterRole | - | - |
| hpc-manager-rolebinding | ClusterRoleBinding | - | - |
| cronhpa-controller-manager-metrics-service | Service | - | kube-system |
| hpc-manager | ServiceAccount | - | kube-system |
| tke-hpc-controller | Deployment | 100mCPU, 100Mi/pod | kube-system |




## Limits

### Environment requirements


>?If you create a cluster of version 1.12.4 or later, you can use the cluster directly without any parameter changes.


- This add-on is supported only by Kubernetes 1.12 or later versions.
- The launch parameters of kube-apiserver must be set as follows: `--feature-gates=CustomResourceSubresources=true`.

#### Node Requirements

- The HPC add-on follows the timezone of the associated server. Please make sure that the `/etc/localtime` file exists in the node.
- By default, two HPC Pods are installed on different nodes. Therefore at least two nodes are required.

#### Requirement on resource to be controlled

When you create an HPC resource, please make sure that the workload (K8s resource) to be controlled exists in the cluster.


## Directions

### Installing HPC

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the "Add-on List" page, click **Create**, On the "Create Add-on" page that appears, select **HPC**.
5. Click **Done**.


### Examples

#### Creating a scheduled task resource that associated with Deployment
The example is as follows:
<dx-codeblock>
:::  yaml
apiVersion: autoscaling.cloud.tencent.com/v1
kind: HorizontalPodCronscaler
metadata:
  name: hpc-deployment
  namespace: default 
spec:
  scaleTarget:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
    namespace: default 
  crons:
- name: "scale-down"
  excludeDates:
    - "* * * 15 11 *"
    - "* * * * * 5"
  schedule: "30 */1 * * * *"
  targetSize: 1
- name: "scale-up"
  excludeDates:
    - "* * * 15 11 *"
    - "* * * * * 5"
  schedule: "0 */1 * * * *"
  targetSize: 3
:::
</dx-codeblock>

#### Creating a scheduled task resource that associated with StatefulSet
The example is as follows:
<dx-codeblock>
:::  yaml
apiVersion: autoscaling.cloud.tencent.com/v1
kind: HorizontalPodCronscaler
metadata:
  name: hpc-statefulset
  namespace: default
spec:
  scaleTarget:
    apiVersion: apps/v1
    kind: Statefulset
    name: nginx-statefulset
    namespace: default
  crons:
  - name: "scale-down"
    excludeDates:
      - "* * * 15 11 *"
    schedule: "0 */2 * * * *"
    targetSize: 1
  - name: "scale-up"
    excludeDates:
      - "* * * 15 11 *"
    schedule: "30 */2 * * * *"
    targetSize: 4
:::
</dx-codeblock>

#### Creating a scheduled task resource that associated with HPA
The example is as follows:
<dx-codeblock>
:::  yaml
apiVersion: autoscaling.cloud.tencent.com/v1
kind: HorizontalPodCronscaler
metadata:
  labels:
    controller-tools.k8s.io: "1.0"
  name: hpc-hpa
spec:
  scaleTarget:
    apiVersion: autoscaling/v1
    kind: HorizontalPodAutoscaler
    name:  nginx-hpa
    namespace: default
  crons:
  - name: "scale-up"
    schedule: "30 */1 * * * *"
    minSize: 2
    maxSize: 6
  - name: "scale-down"
    schedule: "0 */1 * * * *"
    minSize: 1
    maxSize: 5
:::
</dx-codeblock>

### Scheduled duration settings

| Field Name | Required | Value Range | Allowed Special Characters |
| ------------ | -------- | ------------------- | -------------- |
| Seconds | Yes | 0 - 59 | * / , - |
| Minutes | Yes | 0 - 59 | * / , - |
| Hours | Yes | 0 - 23 | * / , - |
| Day of month | Yes | 1 - 31 | * / , - ? |
| Month | Yes | 1 - 12 or JAN - DEC | * / , - |
| Day of week | Yes | 0 - 6 or SUN - SAT | * / , - ? |

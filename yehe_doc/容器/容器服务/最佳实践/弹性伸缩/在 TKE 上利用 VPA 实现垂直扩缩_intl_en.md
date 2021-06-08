## Overview
Kubernetes [Vertical Pod Autoscaler](https://github.com/kubernetes/autoscaler/tree/vpa-release-0.8/vertical-pod-autoscaler) (VPA) can automatically adjust the reserved CPU and memory of Pod, improve cluster resource utilization and release CPU and memory for other Pods. This document describes how to use the VPA community edition in TKE to implement the scaling up and scaling down of Pods.

## Use Cases

The auto-scaling feature of VPA makes the TKE very flexible and adaptive. When the business load increases sharply, VPA can quickly increase the Request of the container within the user's setting range. When the business load decreases, VPA can appropriately reduce the Request based on the actual needs to save computing resources. The entire process is automated without manual intervention. It is suitable for scenarios that require rapid expansion and stateful application expansion. In addition, VPA can be used to recommend a more reasonable Request to user, and improve the resource utilization of the container while ensuring that the container has sufficient available resources.


## VPA Strengths
Compared with [Horizontal Pod Autoscaler (HPA)](https://intl.cloud.tencent.com/document/product/457/32424), VPA has the following advantages:
- VPA does not need to adjust the replicas of Pod for expansion, and the expansion speed is faster.
- VPA can achieve the expansion of the stateful applications, while HPA is not suitable for the scaling out of the stateful applications.
- If the Request is set too large, the cluster resource utilization is still very low when HPA is used to scale in the Pods to a Pod. In this case, you can use VPA to scale down to improve the cluster resource utilization.



## VPA Limits


>!VPA community edition is in testing. Use this feature with caution. We recommend setting "updateMode" to "Off" to ensure that VPA will not automatically change the value of Request. You can still view the recommended value of request bound to the load in the VPA object.


- You can use the VPA to update the resource configurations of the running Pods. This feature is in testing. The configuration updates will lead to Pod restart and rebuilding, and the Pods may be scheduled to other nodes.
- The VPA does not evict the Pods that are not run under a controller. For these Pods, the `Auto` mode is equivalent to the `Initial` mode.
- You cannot run VPA simultaneously with the HPA that uses the CPU and memory as metrics. If the HPA uses other metrics except CPU and memory, you can run the VPA with the HPA at the same time. For details, see [Using Custom Metrics for Auto Scaling in TKE](https://intl.cloud.tencent.com/document/product/457/38941).
- The VPA uses an Admission Webhook as its admission controller. If there are other Admission Webhooks in the cluster, you need to ensure that they do not conflict with the Admission Webhooks of the VPA. The execution sequence of admission controllers is defined in the configuration parameters of the API Server.
- The VPA can react to most Out of Memory (OOM) events.
- The VPA performance has not been tested in large-scale clusters.
- The recommended value of Pod resource Request set by the VPA may exceed the upper limit of the available resources (such as node resources, idle resources, and resource quotas). In this case, the Pod may go to Pending and cannot be scheduled. This can be partly addressed by using the VPA together with the [Cluster Autoscaler](https://intl.cloud.tencent.com/document/product/457/35900).
- Multiple VPA resources matching the same pod have undefined behavior.

For more limitations on VPA, see [VPA Known limitations](https://github.com/kubernetes/autoscaler/tree/vpa-release-0.8/vertical-pod-autoscaler#known-limitations).

## Prerequisites
- You have created a TKE cluster. For how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster has been connected via the command line tool Kubectl. For how to connect to a cluster, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).


## Directions

[](id:VPA)

### Deploying VPA

1. Log in to the CVM in the cluster. 
2. You can connect to a TKE cluster from a local client using the command line tool kubectl.
3. Run the following command to clone the [kubernetes/autoscaler](https://github.com/kubernetes/autoscaler) from GitHub Repository.
```sh
git clone https://github.com/kubernetes/autoscaler.git
```
4. Run the following command to switch to the`vertical-pod-autoscaler` directory.
```
cd autoscaler/vertical-pod-autoscaler/
```
5. (Optional) If you have already deployed another version of VPA, run the following command to remove it. Otherwise an exception may occur.
```
./hack/vpa-down.sh
```
6. Run the following command to deploy VPA related components to your cluster.
```
./hack/vpa-up.sh
```
7. Run the following command to verify whether the VPA component is successfully created.
```
kubectl get deploy -n kube-system | grep vpa
```
After successfully creating the VPA component, you can check the three Deployments in the kube-system namespace, namely vpa-admission-controller, vpa-recommender, and vpa-updater, as shown below:
![](https://main.qcloudimg.com/raw/fb4cdfb049c81f5ca3c0e535acbf0d75.png)




### Sample 1: using VPA to obtain the recommended value of Request

>? 
>- We do not recommend using VPA to automatically update Request in a production environment.
>- You can use VPA to view the recommended value of Request and manually trigger the update as needed.



In this sample, you will create a VPA object with `updateMode` set to `Off` and create a Deployment with two Pods, and each Pod has a container. After the Pod is created, VPA will analyze the CPU and memory requirements of the container and record the recommended value of Request in the `status` field. VPA will not automatically update the resource requests of the running containers.

Run the following command in kubectl to generate a VPA object named `tke-vpa`, pointing to a Deployment named `tke-deployment`:

```shell
cat <<EOF | kubectl apply -f -
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
    name: tke-vpa
spec:
    targetRef:
      apiVersion: "apps/v1"
      kind: Deployment
      name: tke-deployment
    updatePolicy:
      updateMode: "Off"
EOF
```

Run the following command to generate a Deployment object named `tke-deployment`:

```shell
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
    name: tke-deployment
spec:
    replicas: 2
    selector:
      matchLabels:
        app: tke-deployment
    template:
      metadata:
        labels:
          app: tke-deployment
      spec:
        containers:
        - name: tke-container
          image: nginx
EOF
```

The generated Deployment object is show as follows:
![](https://main.qcloudimg.com/raw/556334a46666d4f74c18432ed6083c55.png)

>! The `tke-deployment` created above does not set the Request of CPU or memory, and the [Qos](https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/) of the Pod is set to BestEffort. In this case, Pod is easy to be evicted. We recommend that you set the Request and Limit when creating the Deployment of the application. If you create a workload via the TKE console, the default Request and Limit of each container will be automatically set.
![](https://main.qcloudimg.com/raw/cda9a5c1e169eb2b0caa56eb514fc8b7.png)
>


Run the following command to view the recommended Requests of CPU and memory by VPA:
```shell
kubectl get vpa tke-vpa -o yaml
```

The execution results are as follows:
```yaml
...
recommendation:
      containerRecommendations:
      - containerName: tke-container
        lowerBound:
          cpu: 25m
          memory: 262144k
        target:# Recommended value
          cpu: 25m
          memory: 262144k
        uncappedTarget:
          cpu: 25m
          memory: 262144k
        upperBound:
          cpu: 1771m
          memory: 1851500k
```

The CPU and memory corresponding to `target` are the recommended Requests. You can remove the previous Deployment and create a new Deployment with the recommended Request.

| Field | Description |
|---------|---------|
| **lowerBound** | The minimum value recommended. The use of a Request smaller than this value may have a major impact on performance or availability. |
| **target** | Recommended value. The VPA calculates the most appropriate Request. |
| **uncappedTarget** | The latest recommended value. It is only based on the actual resource usage and does not consider the recommended value range of the container set in `.spec.resourcePolicy.containerPolicies`. The uncappedTarget may differ from the recommended `lowerBound` and `upperBound`. This field is only used to indicate the status and will not affect the actual resource allocation. |
| **upperBound** | The maximum value recommended. The use of a Request larger than this value may cause a resource waste. |



### Sample 2: Disabling a specific container

If there are multiple containers in the Pod, for example, one is an application container and the other is a secondary container. You can choose to stop recommending Request for the secondary container to save the cluster resources.

In this sample, you will create a VPA with a specific container disabled, and create a Deployment with a Pod, and the Pod contains two containers. After the Pod is created, VPA only creates and calculates the recommended value for one container, and stops recommending Request for the other container.

Run the following command in the kubectl to generate a VPA object named `tke-opt-vpa`, pointing to a Deployment named `tke-opt-deployment`:

```shell
cat <<EOF | kubectl apply -f -
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
    name: tke-opt-vpa
spec:
    targetRef:
      apiVersion: "apps/v1"
      kind: Deployment
      name: tke-opt-deployment
    updatePolicy:
      updateMode: "Off"
    resourcePolicy:
      containerPolicies:
      - containerName: tke-opt-sidecar
        mode: "Off"
EOF
```

>! In the `.spec.resourcePolicy.containerPolicies` of the VPA, the `mode` of `tke-opt-sidecar` is set to "Off", and VPA will not calculate and recommend a new Request for `tke-opt-sidecar`.


Run the following command to generate a Deployment object named `tke-deployment`:
```sh
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
    name: tke-opt-deployment
spec:
    replicas: 1
    selector:
      matchLabels:
        app: tke-opt-deployment
    template:
      metadata:
        labels:
          app: tke-opt-deployment
      spec:
        containers:
        - name: tke-opt-container
          image: nginx
        - name: tke-opt-sidecar
          image: busybox
          command: ["sh","-c","while true; do echo TKE VPA; sleep 60; done"]
EOF
```

The generated Deployment object is show as follows:
![](https://main.qcloudimg.com/raw/54c88b647bfe17489cf8cea1cc1ca95e.png)


Run the following command to view the recommended Requests of CPU and memory by VPA:
```shell
kubectl get vpa tke-opt-vpa -o yaml
```

The execution results are as follows:

```yaml
...
    recommendation:
      containerRecommendations:
      - containerName: tke-opt-container
        lowerBound:
          cpu: 25m
          memory: 262144k
        target:
          cpu: 25m
          memory: 262144k
        uncappedTarget:
          cpu: 25m
          memory: 262144k
        upperBound:
          cpu: 1595m
          memory: 1667500k
```

In the execution result, there is only the recommended value of `tke-opt-container`, and no recommended value of `tke-opt-sidecar`.

### Sample 3: updating the Request automatically

>! Automatic updating the resources of the running Pods is an experimental feature of VPA. We recommend that you do not use this feature in a production environment.


In this sample, you will create a VPA that can automatically adjust the CPU and memory Requests, and create a Deployment with two Pods. Each Pod will set the Request and Limit of the resource.


Run the following command in the kubectl to generate a VPA object named `tke-auto-vpa`, pointing to a Deployment named `tke-auto-deployment`:
```yaml
cat <<EOF | kubectl apply -f - 
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
    name: tke-auto-vpa
spec:
    targetRef:
      apiVersion: "apps/v1"
      kind: Deployment
      name: tke-auto-deployment
    updatePolicy:
      updateMode: "Auto"
EOF
```

>! The `updateMode` field of this VPA is set to `Auto`, which means that the VPA can update the CPU and memory Requests during the life cycle of the Pod. VPA can remove the Pod, adjust the CPU and memory Requests, and then rebuild a Pod.


Run the following command to generate a Deployment object named `tke-auto-deployment`:
```shell
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
    name: tke-auto-deployment
spec:
    replicas: 2
    selector:
      matchLabels:
        app: tke-auto-deployment
    template:
      metadata:
        labels:
          app: tke-auto-deployment
      spec:
        containers:
        - name: tke-container
          image: nginx
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
            limits:
              cpu: 200m
              memory: 200Mi
EOF
```


>! When the Deployment is created in the above operation, the Request and Limit of the resource have been set. In this case, VPA will not only recommend the Request, but also automatically recommend the Limit based on the initial ratio of Request and Limit. For example, the initial ratio of CPU’s Request and Limit in YAML is 100m:200m, namely 1:2, then the value of Limit recommended by VPA is twice the value of Request recommended in the VPA object.



The generated Deployment object is show as follows:
![](https://main.qcloudimg.com/raw/10b6c1a69ea1a3270bd3b9b286a561b3.png)



Run the following command to obtain the detailed information of the running Pod:

```sh
kubectl get pod pod-name -o yaml
```

The execution result is shown below. VPA modified the original Request and Limits to the recommended value of VPA, and maintained the initial ratio of Request and Limits. At the same time, an annotation that recorded the updates is generated:

```yaml
apiVersion: v1
kind: Pod
metadata:
    annotations:
      ...
      vpaObservedContainers: tke-container
      vpaUpdates: Pod resources updated by tke-auto-vpa: container 0: memory request, cpu request
...
spec:
    containers:
    ...
      resources:
        limits:# The new Request and Limits will maintain the initial ratio
          cpu: 50m	
          memory: 500Mi
        requests:
          cpu: 25m
          memory: 262144k
      ...
```

Run the following command to obtain the detailed information of the relevant VPA:

```sh
kubectl get vpa tke-auto-vpa -o yaml
```

The execution results are as follows:

```yaml
...
    recommendation:
      containerRecommendations:
      - containerName: tke-container
        Lower Bound:
          Cpu:     25m
          Memory:  262144k
        Target:
          Cpu:     25m
          Memory:  262144k
        Uncapped Target:
          Cpu:     25m
          Memory:  262144k
        Upper Bound:
          Cpu:     101m
          Memory:  262144k
```

`target` means that the container will run in the best state when the Requests of CPU and memory are 25m and 262144k respectively.

VPA uses the recommended values of `lowerBound` and `upperBound` to decide whether to evict a Pod and replace it with a new Pod. If the Pod’s Request is smaller than the lower limit or larger than the upper limit, VPA will remove the Pod and replace it with a Pod with a recommended value.

## Troubleshooting

### 1. An error occurs when running the `vpa-up.sh` script.

#### Errors
```shell
ERROR: Failed to create CA certificate for self-signing. If the error is "unknown option -addext", update your openssl version or deploy VPA from the vpa-release-0.8 branch.
```

#### Solutions
1. If you have not run the command through the CVM in the cluster, we recommend that you download the Autoscaler project in the CVM and [deploy VPA](#VPA). If you need to connect the cluster to your CVM, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639).
2. If the errors still exist, please check whether the following problems exist:
 - Check whether the `openssl` version of the cluster CVM is later than v1.1.1.
 - Whether the `vpa-release-0.8` branch of the Autoscaler project is used.

### 2. The VPA-related load could not be started up.

#### Errors
If the VPA-related load fails to start up, and the following message is generated:
![](https://main.qcloudimg.com/raw/026ae791429cb584fa1c61af3ac8340f.png)
**Message 1**: indicates that the Pods in the load fail to run.
**Message 2**: indicates the address of the image.


#### Solutions
The VPA-related load could not be started up because the image located in GCR could not be downloaded. You can try the following steps to solve the problem:
1. **Download the image**.
    Visit the "k8s.gcr.io/" image repository and download the images of vpa-admission-controller, vpa-recommender, and vpa-updater.
2. **Replace the image tags and push the images**.
    Replace the image tags of vpa-admission-controller, vpa-recommender, and vpa-updater and push them to your image repository. For how to push and upload the image, please see [TCR Personal Edition](https://intl.cloud.tencent.com/document/product/1051/38866).
3. **Change the image address in YAML**.
    In the YAML file, update the image addresses of vpa-admission-controller, vpa-recommender, and vpa-updater to the new addresses you set.


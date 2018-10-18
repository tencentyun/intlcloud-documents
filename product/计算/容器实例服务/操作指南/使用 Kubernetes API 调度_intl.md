## Overview
After Virtual Kubelet is deployed in the Kubernetes cluster, the cluster's apiserver component can be used to schedule and manage CIS instances.

## Procedure
In the following example, CIS is used to schedule and deploy Deployment in Tencent Cloud TKE's Kubernetes cluster.
1. Log in to any Kubernetes cluster that communicates with Tencent Cloud via a network, such as a TKE cluster, a Kubernetes cluster you built with a CVM, a Kubernetes cluster you built with a Direct Connect or an IDC interconnected with Tencent Cloud, etc.

2. Use Kubectl or call the Kubernetes API to deploy Virtual Kubelet on the cluster node. For more information, see [How to Deploy Virtual-kubelet](https://cloud.tencent.com/document/product/858/17680).

3. After Virtual Kubelet is deployed, check the node and Pod.
```
kubectl get nodes -o wide
```
```
kubectl get pods -o wide
```
You will find that a Pod and a virtual node are added to the cluster with the same name: virtual-kubelet.
![][1]

4. Deploy Deployment, and specify virtual-kubelet as the nodeName, and schedule the Deployment's Pod to the virtual node virtual-kubelet.
```
kubectl create -f service-nginx.yaml
```
![][2]
Check the Pod status, as shown in the example below:
![][3]

5. After the deployment is completed, the Deployment you just created can be found in the **Service** on the [TKE console](https://console.cloud.tencent.com/ccs).
![][4]
However, the Deployment does not use the resources of the TKE cluster node, but has created the Pod into CIS. So, the Pod can be found in the **Container Instance** on the [CIS console](https://console.cloud.tencent.com/cis).
![][5]

[1]:https://main.qcloudimg.com/raw/e26ab86e8de97abf36380482703b932f.png
[2]:https://main.qcloudimg.com/raw/c1406a0b424a94a04fd90d19eec83c55.png
[3]:https://main.qcloudimg.com/raw/8e4c0d95784dee3700c783f8bd911a60.png
[4]:https://main.qcloudimg.com/raw/8066e7a39d8686f9ca226dd606000e1a.png
[5]:https://main.qcloudimg.com/raw/d49e91a8c69dcf3e44253e262a4cbaef.png


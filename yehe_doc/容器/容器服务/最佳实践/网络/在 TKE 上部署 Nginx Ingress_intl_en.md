## Overview

Nginx Ingress provides robust features and extremely high performance as well as multiple deployment modes. This document introduces the three deployment schemes of Nginx Ingress on Tencent Kubernetes Engine (TKE): [Deployment + LB](#step1), [Daemonset + HostNetwork + LB](#step2), and [Deployment + LB directly connected to Pod](#step3) and their deployment methods.

## Nginx Ingress Introduction

Nginx Ingress is an implementation of Kubernetes Ingress. By watching the Ingress resources of Kubernetes clusters, it converts Ingress rules into an Nginx configuration to enable Nginx to perform Layer-7 traffic forwarding, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/cc1260950a0cc812508cf25819e3c129.png" data-nonescope="true">
Nginx Ingress can be implemented in the following two modes. This document mainly introduces the implementation of Kubernetes in the open-source community:

- [Implementation of Kubernetes in the Open-Source Community](https://github.com/kubernetes/ingress-nginx)
- [Official Implementation of Nginx](https://github.com/nginxinc/kubernetes-ingress)

### Suggestions for deployment solution selection
Based on a comparison of the three deployment solutions for Nginx Ingress on TKE, this document offers the following selection suggestions:
1. [Deployment + LB](#step1): this solution is relatively simple and applicable to general scenarios, but performance issues may arise in large-scale and high-concurrency scenarios. If your performance requirements are low, you can consider adopting this solution.
2. [Daemonset + HostNetwork + LB](#step2): the use of hostNetwork offers good performance, but manual maintenance of CLBs and Nginx Ingress nodes is required and auto scaling cannot be implemented. Therefore, we do not recommend this solution.
3. [Deployment + LB directly connected to pod](#step3): this solution offers good performance, without the need for manual CLB maintenance, making this the ideal solution. However, in this solution, clusters need to support VPC-CNI. If the existing clusters use the VPC-CNI network plug-in or the Global Router network plug-in and have enabled support for VPC-CNI (mixed use of two modes), we recommend that you adopt this solution.
<span id="step1"></span>
## Solution 1: Deployment + LB

The simplest way to deploy Nginx Ingress on TKE is to deploy Nginx Ingress Controller in Deployment mode and create a LoadBalancer-type Service for it (automatically creating a CLB or binding an existing CLB) to enable the CLB to receive external traffic and forward it into Nginx Ingress, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/337cf2fa30cb27f89eed438b0458d557.png" data-nonescope="true">
Currently, by default, a LoadBalancer-type Service on TKE is implemented based on NodePort: the CLB binds the NodePort of each node as the RS (Real Server) and forwards traffic to the NodePort of each node. Then through Iptables or IPVS, nodes route requests to the corresponding backend pod of the Service (namely the pod of Nginx Ingress Controller). Subsequently, if nodes are added or deleted, the CLB will automatically update the node NodePort binding.
Run the following commands to install Nginx Ingress:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-deployment.yaml -n nginx-ingress
```
<span id="step2"></span>
## Solution 2: Daemonset + HostNetwork + LB

In solution 1, traffic passes through a NodePort layer, introducing one more layer for forwarding, which leads to the following issues:
- The forwarding path is relatively long: after reaching NodePort, traffic goes through the LB within Kubernetes and is then forwarded through Iptables or IPVS to Nginx. This increases network time consumption.
- Passing through NodePort will necessarily cause SNAT. If traffic is too concentrated, port exhaustion or conntrack insertion conflicts can easily occur, leading to packet loss and causing some traffic exceptions.
- The NodePort of each node also serves as a CLB. If the CLB is bound with the NodePorts of a large number of nodes, the LB status is distributed among each node, which can easily cause a global load imbalance.
- The CLB carries out health probes on NodePort, and probe packets are ultimately forwarded to the Pods of Nginx Ingress. If the CLB is bound with too many nodes, and the Nginx Ingress has a small number of pods, the probe packets will put immense pressure on Nginx Ingress.

In solution 2, the following solution is proposed:
Nginx Ingress uses hostNetwork, and the CLB is directly bound with node IP address + port (80,443), without passing through NodePort. With the use of hostNetwork, the pods of Nginx Ingress cannot be scheduled to the same node. To avoid port listening conflicts, you can preselect some nodes as edge nodes dedicated to the deployment of Nginx Ingress and label them. Then, Nginx Ingress can be deployed as a DaemonSet on these nodes. The following figure shows the architecture:
<img style="width:450px" src="https://main.qcloudimg.com/raw/09e4a46655dcaa2a32d6b8e02fb8d96c.png" data-nonescope="true">
To install Nginx Ingress, perform the following steps:
1. Run the following command to attach a label to the nodes planned for the deployment of Nginx Ingress (be sure to replace the node names):
```
kubectl label node 10.0.0.3 nginx-ingress=true
```
2. Run the following commands to deploy Nginx Ingress on these nodes:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-daemonset-hostnetwork.yaml -n nginx-ingress
```
3. Manually create a CLB, create a TCP listener for ports 80 and 443, and bind them with ports 80 and 443 of the nodes where Nginx Ingress has been deployed.
<span id="step3"></span>
## Solution 3: Deployment + LB Directly Connected to Pod
Solution 2 offers more advantages than solution 1, but it has the following issues:
- It increases the OPS cost for manual maintenance of the CLB and Nginx Ingress nodes.
- Nginx Ingress nodes need to be planned in advance. When Nginx Ingress nodes are added or deleted, you need to manually bind or unbind nodes on the CLB console.
- Automatic scaling is not supported.

In solution 3, the following solution is proposed:
- If the network mode is VPC-CNI and all pods use ENI, you can directly bind the CLB with the ENI pods, bypassing NodePort. This saves the trouble of manual management of the CLB and enables support for automatic scaling, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/83630c50a259482ede83742945fc591e.png" data-nonescope="true">
- If the network mode is Global Router, you can go to the cluster information page and [enable VPC-CNI support for the cluster](https://intl.cloud.tencent.com/document/product/457/35250). This enables the mixed use of the two network modes, as shown in the figure below:
![](https://main.qcloudimg.com/raw/c3e443f268b63abf9dd37075ebd73b91.png)
After ensuring that the cluster supports VPC-CNI, run the following commands in sequence to install Nginx Ingress:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-deployment-eni.yaml -n nginx-ingress
```



## FAQs
### How can private network Ingress be supported?   
In [solution 2: Daemonset + HostNetwork + LB](#step2), the CLB is manually managed. When creating a CLB, you can select public network or private network. In [solution 1: Deployment + LB](#step1) and [solution 3: Deployment + LB directly connected to pod](#step3), public network CLBs are created by default.  
To use a private network, you can redeploy YAML and add a key to the Service in nginx-ingress-controller, for example, `service.kubernetes.io/qcloud-loadbalancer-internal-subnetid`, with value set to the annotation of the subnet ID created by the private network CLB. Refer to the following code:
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxx # value should be replaced with a subnet ID in the VPC where the cluster belongs.
  labels:
    app: nginx-ingress
    component: controller
  name: nginx-ingress-controller
```

### How can an existing LB be shared?

In [solution 1: Deployment + LB](#step1) and [solution 3: Deployment + LB directly connected to Pod](#step3), new CLBs are automatically created by default. The traffic entry address of Ingress depends on the IP address of the newly created CLB. If a business is dependent upon the entry address, you can bind Nginx Ingress with an existing CLB.
The specific method is to redeploy YAML and add a key to the Service in nginx-ingress-controller, such as `service.kubernetes.io/tke-existed-lbid`, with value set to the annotation of the CLB ID. Refer to the following code:
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx # value should be replaced with the CLB ID.
  labels:
    app: nginx-ingress
    component: controller
  name: nginx-ingress-controller
```

### What’s the size of the Nginx Ingress public network bandwidth?

There are two types of Tencent Cloud accounts: bill-by-IP accounts and bill-by-CVM accounts:
>! You can refer to [Distinguishing Between Tencent Cloud Account Types](https://intl.cloud.tencent.com/document/product/684/15246) to identify your account type.

- **Bill-by-IP account type:** bandwidth is moved to the CLB or IP address for management.
  If your account is a bill-by-IP account, the Nginx Ingress bandwidth equals the purchased CLB bandwidth, which is 10 Mbps by default (pay-as-you-go) and can be adjusted as needed.
- **Bill-by-CVM account type:** bandwidth is managed on CVMs.
    If your account is a bill-by-CVM account, Nginx Ingress uses a public network CLB, and the public network bandwidth of Nginx Ingress is the sum of the bandwidth of all TKE nodes bound with the CLB. If [solution 3: Deployment + LB directly connected to pod](#step3) is adopted, the CLB is directly connected to pods, which means that the CLB is directly bound with ENI. In that case, the public network bandwidth of Nginx Ingress is the sum of the bandwidth of all nodes where Nginx Ingress Controller Pods are scheduled.

<span id="ingress"></span>

### How can I create an Ingress?
When you deploy Nginx Ingress on TKE and need to use Nginx Ingress to manage Ingress, if you cannot create an Ingress on the TKE console, you can use YAML to create an Ingress and you need to specify the annotation of Ingress Class for each Ingress. Refer to the following code:
```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    kubernetes.io/ingress.class: nginx # this is the key part
spec:
  rules:
  - host: *
    http:
      paths:
      - path: /
        backend:
          serviceName: nginx-v1
          servicePort: 80
```

### How can I enable monitoring?

For Nginx Ingress installed through the method in [How can I create an Ingress](#ingress), the metrics port has been opened and can be used for Prometheus collection. If prometheus-operator is installed in the cluster, you can use ServiceMonitor to collect monitoring data for Nginx Ingress. Refer to the following code:
```
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: nginx-ingress-controller
  namespace: nginx-ingress
  labels:
    app: nginx-ingress
    component: controller
spec:
  endpoints:
  - port: metrics
    interval: 10s
  namespaceSelector:
    matchNames:
    - nginx-ingress
  selector:
    matchLabels:
      app: nginx-ingress
      component: controller
```

For native Prometheus configuration, refer to the following code:
```
    - job_name: nginx-ingress
      scrape_interval: 5s
      kubernetes_sd_configs:
      - role: endpoints
        namespaces:
          names:
          - nginx-ingress
      relabel_configs:
      - action: keep
        source_labels:
        - __meta_kubernetes_service_label_app
        - __meta_kubernetes_service_label_component
        regex: nginx-ingress;controller
      - action: keep
        source_labels:
        - __meta_kubernetes_endpoint_port_name
        regex: metrics
```

After collecting monitoring data, you can configure the [dashboards provided by the Nginx Ingress community](https://github.com/kubernetes/ingress-nginx/tree/master/deploy/grafana/dashboards) for grafana and display data.   
In actual operation, you can directly copy JSON data and import it to grafana to import dashboards. `nginx.json` is used to display the various regular monitoring dashboards for Nginx Ingress, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/f6c14b7cd6ff9f2959a818b0c4c4f644.png" data-nonescope="true">
`request-handling-performance.json` is used to display the performance monitoring dashboard of Nginx Ingress, as shown in the figure below:
<img style="width:450px" src="https://main.qcloudimg.com/raw/d21748c1903103a5b6988051848292f5.png" data-nonescope="true">


## References

- [TKE Service YAML Sample](https://intl.cloud.tencent.com/document/product/457/36833)
- [TKE Service Using an Existing CLB](https://intl.cloud.tencent.com/document/product/457/36835)
- [Distinguishing Between Tencent Cloud Account Types](https://intl.cloud.tencent.com/document/product/684/15246)

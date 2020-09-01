## Overview

NGINX Ingress has powerful features, excellent performance, and supports various deployment methods. This document describes how to deploy NGINX Ingress on Tencent Kubernetes Engine (TKE) using [Deployment + LB](#step1), [Daemonset + HostNetwork + LB](#step2), and [Deployment + LB Direct Connect to Pods](#step3).

## Introduction to NGINX Ingress

NGINX Ingress is an implementation method of Kubernetes ingress resources. It watches ingress resources in a Kubernetes cluster to convert ingress rules into NGINX configurations and enable NGINX to forward L7 traffic, as shown below.
<img style="width:450px" src="https://main.qcloudimg.com/raw/cc1260950a0cc812508cf25819e3c129.png" data-nonescope="true">
NGINX Ingress supports the following two implementation methods. This document describes the implementation method provided by the Kubernetes open-source community.
- [NGINX Ingress implementation provided by the Kubernetes open-source community](https://github.com/kubernetes/ingress-nginx)
- [NGINX Ingress implementation provided on the official NGINX website](https://github.com/nginxinc/kubernetes-ingress)

### Recommended deployment solutions
The following describes three solutions for deploying NGINX Ingress on TKE.
1. [Deployment + LB](#step1): this solution is simple and common but has performance issues in large-scale and high-concurrency scenarios. If you have low performance requirements, you can use this solution.
2. [Daemonset + HostNetwork + LB](#step2): this solution uses hostNetwork to ensure a good performance. However, you need to manually maintain the CLB and NGINX Ingress nodes, and auto scaling is not supported. We do not recommend this solution.
3. [Deployment + LB Direct Connection to Pods](#step3): this solution provides good performance and does not require manual CLB maintenance. However, the solution requires that the cluster support VPC-CNI. If your cluster uses VPC-CNI plugins or Global Router network plugins with VPC-CNI enabled (hybrid mode), we recommend that you use this solution.
<span id="step1"></span>
## Solution 1: Deployment + LB

The simplest way to deploy NGINX Ingress on TKE is to deploy the NGINX Ingress controller as a Deployment workload and create a LoadBalancer service for it. A CLB is automatically created for the service or the service is bound to an existing CLB. The CLB receives external traffic and forwards the traffic to NGINX Ingress, as shown below.
<img style="width:450px" src="https://main.qcloudimg.com/raw/337cf2fa30cb27f89eed438b0458d557.png" data-nonescope="true">
Currently, LoadBalancer services on TKE are implemented based on NodePort by default. The CLB binds NodePorts of different nodes as the backend real server (RS) and forwards traffic to these NodePorts. The nodes use Iptables or IPVS to forward the traffic to the backend pods of the service, that is, the pods where the NGINX Ingress controller is located. If nodes are added or deleted later, the CLB will automatically update the NodePort binding.
To install NGINX Ingress, run the following command:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-deployment.yaml -n nginx-ingress
```
<span id="step2"></span>
## Solution 2: Daemonset + HostNetwork + LB

In solution 1, traffic is forwarded through NodePorts, which causes the following issues:
- The forwarding path is long. After traffic is forwarded to NodePorts, they forward the traffic to nodes through the internal Kubernetes load balancer (LB), and the nodes use Iptables or IPVS to forward the traffic to the NGINX Ingress controller. This increases the forwarding time.
- Source network address translation (SNAT) occurs. If traffic is centralized, source ports are easily used up and packet loss may occur due to conntrack insertion conflicts. As a result, some traffic may be abnormal.
- The NodePort of each node also functions as an LB. If the CLB is bound to a large number of NodePorts, the load balancing status will be distributed to each node, which can easily result in uneven loads on a global scale.
- The CLB detects the health status of NodePorts, and the detection packets are forwarded to the pods where NGINX Ingress is located. If the CLB is bound to a large number of NodePorts and there are few NGINX Ingress pods, the detection packets will put great pressure on the NGINX Ingress.

Solution 2 provides the following solutions to these problems:
NGINX Ingress uses hostNetwork, and the CLB is bound to the IP addresses and port numbers (80 or 443) instead of the NodePorts of nodes. With hostNetwork, the pods where NGINX Ingress is located will not be scheduled to the same node. To prevent port listening conflicts, you can select certain nodes as edge nodes to deploy NGINX Ingress, label these nodes, and deploy NGINX Ingress on these nodes as a DaemonSet workload. The following figure shows the architecture.
<img style="width:450px" src="https://main.qcloudimg.com/raw/09e4a46655dcaa2a32d6b8e02fb8d96c.png" data-nonescope="true">
To install NGINX Ingress, perform the following steps:
1. Run the following command to label the nodes used to deploy NGINX Ingress (replace the example node names with actual ones):
```
kubectl label node 10.0.0.3 nginx-ingress=true
```
2. Run the following command to deploy NGINX Ingress on these nodes:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-daemonset-hostnetwork.yaml -n nginx-ingress
```
3. Manually create a CLB and TCP listeners on ports 80 and 443, and bind the TCP listeners to ports 80 and 443 of the nodes where NGINX Ingress is deployed.
<span id="step3"></span>
## Solution 3: Deployment + LB Direct Connection to Pods

Solution 2 is superior to solution 1 but still has the following issues:
- The costs of manual CLB and NGINX Ingress maintenance are increased.
- The nodes where NGINX Ingress is to be deployed must be planned in advance. To add or delete nodes where NGINX Ingress is deployed, you need to manually bind or unbind these nodes in the CLB console.
- Auto scaling is not supported.

3Solution 2 provides the following solutions to these problems:
- If the network mode is VPC-CNI and all pods use ENIs, you can bind the CLB to pods with ENIs. In this way, traffic is not forwarded through NodePorts, and you do not need to manually manage the CLB. In addition, auto scaling is supported. The following figure shows the architecture.
<img style="width:450px" src="https://main.qcloudimg.com/raw/83630c50a259482ede83742945fc591e.png" data-nonescope="true">
- If the network mode is Global Router, you can [enable VPC-CNI for a cluster](https://intl.cloud.tencent.com/document/product/457/35250) on the cluster details page to use both modes, as shown below.
![](https://main.qcloudimg.com/raw/c3e443f268b63abf9dd37075ebd73b91.png)
After the cluster supports VPC-CNI, run the following commands in sequence to install NGINX Ingress:
```
kubectl create ns nginx-ingress
```
```
kubectl apply -f https://raw.githubusercontent.com/TencentCloudContainerTeam/manifest/master/nginx-ingress/nginx-ingress-deployment-eni.yaml -n nginx-ingress
```



## FAQs
### How can I create NGINX Ingress for private network access?   
In [Solution 2: Daemonset + HostNetwork + LB](#step2), the CLB is manually managed. When you create a CLB, you can select a public or private network. In [Solution 1: Deployment + LB](#step1) and [Solution 3: Deployment + LB Direct Connection to Pods](#step3), a public CLB is created by default.  
To provide NGINX Ingress for private access, reconfigure the YAML file. Add a key for the service of the NGINX Ingress controller, for example, `service.kubernetes.io/qcloud-loadbalancer-internal-subnetid`. The key value is the annotation of the subnet ID of the private CLB. See the following code:
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxx # Replace the value with the ID of a subnet in the VPC where the cluster is located.
  labels:
    app: nginx-ingress
    component: controller
  name: nginx-ingress-controller
```

### How can I reuse an existing LB?

In [Solution 1: Deployment + LB](#step1) and [Solution 3: Deployment + LB Direct Connection to Pods](#step3), a CLB is automatically created by default. The traffic entry address of NGINX Ingress depends on the IP address of the created CLB. If your businesses depend on the entry address, bind NGINX Ingress to an existing CLB.
To bind NGINX Ingress to an existing CLB, reconfigure the YAML file. Add a key to the service of the NGINX Ingress controller, for example, `service.kubernetes.io/tke-existed-lbid`. The value is the annotation of the CLB ID. See the following code:
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-6swtxxxx # Replace the value with the CLB ID.
  labels:
    app: nginx-ingress
    component: controller
  name: nginx-ingress-controller
```

### How is the public bandwidth of NGINX Ingress?

Tencent Cloud accounts are classified into bill-by-IP accounts and bill-by-CVM accounts.
>! To check your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>
- **Bill-by-IP**: public network fees are charged by the public IP address or CLB instead of the CVM.
  If you use a bill-by-IP account, the NGINX Ingress bandwidth is equal to the bandwidth of the purchased CLB. The default bandwidth is 10 Mbps (pay-as-you-go), which can be adjusted based on your actual needs.
- **Bill-by-CVM**: public network fees are charged by the CVM.
    If you use a bill-by-CVM account, NGINX Ingress uses a public CLB, and the public bandwidth of NGINX Ingress is the sum of the bandwidth of TKE nodes bound to the CLB. If you use [Solution 3: Deployment + LB Direct Connection to Pods](#step3), the CLB directly connects to pods, that is, the CLB is bound to ENIs. The public bandwidth of NGINX Ingress is the sum of the bandwidth of the nodes to which NGINX Ingress controller pods are scheduled.

<span id="ingress"></span>

### How can I create an ingress?
If you deploy NGINX Ingress on TKE yourself, you need to use NGINX Ingress to manage ingress resources and cannot create ingresses in the TKE console. In this case, you can use the YAML file to create ingresses and specify an ingress class annotation for each ingress. See the following code:
```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    kubernetes.io/ingress.class: nginx # This is the key.
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

### How can I monitor NGINX Ingress?

When NGINX Ingress is installed using the method in [How can I create an ingress?](#ingress), metrics ports are exposed and metrics can be collected using Prometheus. If a cluster has prometheus-operator installed, ServiceMonitor can be used to collect NGINX Ingress monitoring data. See the following code:
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

For more information about the native Prometheus configuration, see the following code:
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

After monitoring data is collected, you can configure [dashboards provided by the NGINX Ingress community](https://github.com/kubernetes/ingress-nginx/tree/master/deploy/grafana/dashboards) for Grafana to display data.   
Copy the JSON file and import it to Grafana to import the data to dashboards. `nginx.json` displays the common monitoring dashboards of NGINX Ingress, as shown below.
<img style="width:450px" src="https://main.qcloudimg.com/raw/f6c14b7cd6ff9f2959a818b0c4c4f644.png" data-nonescope="true">
`request-handling-performance.json` displays performance monitoring dashboards of NGINX Ingress, as shown below.
<img style="width:450px" src="https://main.qcloudimg.com/raw/d21748c1903103a5b6988051848292f5.png" data-nonescope="true">


## References

- [TKE Service YAML Example](https://intl.cloud.tencent.com/document/product/457/36833)
- [Using Existing CLBs](https://intl.cloud.tencent.com/document/product/457/36835)
- [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246)

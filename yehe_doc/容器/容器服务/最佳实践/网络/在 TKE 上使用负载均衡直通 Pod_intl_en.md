## Overview

Kubernetes officially provides a NodePort-type Service. This means it provides all nodes with the same port through which a Service can be opened. Traditionally, most Services of the Cloud Load Balancer (CLB) type are implemented based on NodePort. Specifically, the CLB backend is bound with the NodePort of each node. When the CLB receives external traffic, it forwards the traffic to the NodePort of one of the nodes. Then, traffic is forwarded through the CLB within Kubernetes to pods by using iptables or ipvs. See the figure below:
<img style="width:80%" src="https://main.qcloudimg.com/raw/dd6fa146520ca178ab17bc94e7f0fb1f.png" data-nonescope="true">
TKE adopts the same approach to implement the default CLB-type Service and Ingress. Currently, however, it also supports the CLB-pod direct connection mode, in which the CLB backend is directly bound with pod IP + Port, without being bound with the NodePort of nodes. See the figure below:
<img style="width:35%" src="https://main.qcloudimg.com/raw/26a46cfd9e9687ec455260028b19353f.png" data-nonescope="true">



## Analysis of Implementation Methods

### Analysis of issues in the traditional NodePort method
Traditionally, users create a cloud Ingress or LB-type Service by using a CLB directly bound to Nodeport. However, the traditional method involves the following issues:
- After traffic is forwarded from the CLB to NodePort, it needs to go through SNAT before being forwarded to pods. This causes additional performance loss.
- If traffic is overly concentrated on a few NodePorts (for example, when gateways are deployed on a few nodes by using nodeSelector), source port exhaustion or conntrack insertion conflicts may occur.
- The NodePort of each node also serves as a CLB. If the CLB is bound with the NodePorts of too many nodes, the CLB status may be overly distributed, leading to a global load imbalance.


### Advantages of the CLB-pod direct connection method
The CLB-pod direct connection method not only solves the issues of the traditional NodePort method but also offers the following advantages:
- As there is no SNAT, `externalTrafficPolicy: Local` is no longer needed to obtain the source IP address.
- Session persistence is easier to achieve. You only need to enable session persistence for the CLB, without having to set `sessionAffinity` in the Service.


## Operation Scenarios
The CLB-pod direct connection method can be used in the following scenarios:
- You need to obtain the actual source IP address of the client in Layer-4 but do not expect to use the `externalTrafficPolicy: Local` method.
- The network performance needs to be further improved.
- Session persistence needs to be easier to achieve.
- Load imbalance in global connection scheduling needs to be resolved.

## Prerequisites
- The Kubernetes version of the cluster must be 1.12 or later.
For CLB-pod direct connection, you need to check whether pods are Ready. Specifically, check whether Pods are Running and have passed the readinessProbe and the CLB’s pod health monitoring. This is dependent on the `ReadinessGate` feature, which is supported in Kubernetes 1.12 and later versions.
- The `VPC-CNI` ENI mode must be enabled for the cluster network mode. You can refer to [Confirming whether ENI is enabled](#ElasticNetworkCard) to perform confirmation.
Currently, CLB-pod direct connection is implemented based on ENI and does not support the common network mode.

## Directions
<span id="ElasticNetworkCard"></span>
### Confirming whether ENI is enabled
Perform the following steps based on your actual situation:
- If you have selected **VPC-CNI** for "Container network plugin" during cluster creation, then the pods created use ENI by default and you can skip this step.
- If you have selected **Global Router** for "Container network plugin" during cluster creation and then enabled VPC-CNI support, then the two modes are used at the same time. In that case, created pods do not use ENI by default. In this case, you need to use YAML to create workloads and specify the annotation `tke.cloud.tencent.com/networks: tke-route-eni` for pods to declare the use of ENI. In addition, you need to add requests and limits such as `tke.cloud.tencent.com/eni-ip: "1"` for one of the containers. The YAML sample is as follows:
``` yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     labels:
       app: nginx
     name: nginx-deployment-eni
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         annotations:
           tke.cloud.tencent.com/networks: tke-route-eni
         labels:
           app: nginx
       spec:
         containers:
           - image: nginx
             name: nginx
             resources:
               requests:
                 tke.cloud.tencent.com/eni-ip: "1"
               limits:
                 tke.cloud.tencent.com/eni-ip: "1"
```


### Declaring the direct connection mode during Service creation
When opening services through a CLB Service, you need to declare the use of the direct connection mode. The steps are as follows:

#### Using the console to create a Service
To use the console to create a Service, select **Direct CLB-Pod Connection Mode**. For more information, see [Creating a Service](https://intl.cloud.tencent.com/document/product/457/36833). See the figure below:
![](https://main.qcloudimg.com/raw/15fad1c82fe84d3b55d144c08a65e3a9.png)

#### Using YAML to create a Service
To use YAML to create a Service, you need to add the annotation `service.cloud.tencent.com/direct-access: "true"` for the Service. A sample is as follows:
>? For more information on how to use YAML to create a Service, see [Creating a Service](https://intl.cloud.tencent.com/document/product/457/36833#creating-a-service).
>
``` yaml
   apiVersion: v1
   kind: Service
   metadata:
     annotations:
       service.cloud.tencent.com/direct-access: "true"
     labels:
       app: nginx
     name: nginx-service-eni
   spec:
     externalTrafficPolicy: Cluster
     ports:
     - name: 80-80-no
       port: 80
       protocol: TCP
       targetPort: 80
     selector:
       app: nginx
     sessionAffinity: None
     type: LoadBalancer
```


### Declaring the direct connection mode during Ingress creation
When opening services through an Ingress, you also need to declare the use of the direct connection mode. The steps are as follows:

#### Using the console to create an Ingress
To use the console to create an Ingress, select **Direct CLB-Pod Connection Mode**. For more information, see [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673#creating-an-ingress). See the figure below:
![](https://main.qcloudimg.com/raw/5d3bbba1604e27ff7b601cadb9313911.png)

#### Using YAML to create an Ingress
To use YAML to create an Ingress, you need to add the annotation `ingress.cloud.tencent.com/direct-access: "true"` for the Ingress. A sample is as follows:
>? For more information on how to use YAML to create an Ingress, see [Creating an Ingress](https://intl.cloud.tencent.com/document/product/457/30673#creating-an-ingress).
>
``` yaml
   apiVersion: networking.k8s.io/v1beta1
   kind: Ingress
   metadata:
     annotations:
       ingress.cloud.tencent.com/direct-access: "true"
       kubernetes.io/ingress.class: qcloud
     name: test-ingress
     namespace: default
   spec:
     rules:
     - http:
         paths:
         - backend:
             serviceName: nginx
             servicePort: 80
           path: /
```

## References

* [TKE in Direct Connection to the CLB of Pods Based on ENI](https://mp.weixin.qq.com/s/fJtlm5Qjm2BfzekC4RegCQ)
* [Enabling VPC-CNI for a Cluster](https://intl.cloud.tencent.com/document/product/457/38971)

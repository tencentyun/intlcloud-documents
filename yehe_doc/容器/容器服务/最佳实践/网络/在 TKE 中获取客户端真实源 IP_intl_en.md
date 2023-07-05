 

## Application Scenarios
When your business requires to know the sources of service requests, the backend server must be able to accurately obtain the real client source IP of the request client. Possible scenarios:
- Audit the source of a service request. For example unusual login location alarms.
- Trace the source of a security attack or security event, such as APT attacks and DDoS attacks.
- Analyze data, such as service traffic region statistics.


## Implementation Methods
In TKE, the default external load balancer is [Tencent Cloud Load Balancer](https://intl.cloud.tencent.com/product/clb), which serves as the first access entry for incoming traffic. The CLB forwards request traffic loads to Kubernetes Service (default) of Kubernetes worker nodes. During this load-balancing process, the real client source IP is preservec (pass-through forwarded). However, in Kubernetes Service forwarding scenarios, data packets will go through SNAT during forwarding no matter whether the CLB forwarding mode is iptables or ipvs, which means that the real client source IP will not be preserved. For your reference, this document provides the following four methods for obtaining the real client source IP in TKE use cases. You can choose an appropriate method based on your actual needs.


### Preserving the client source IP through Service resource configuration
The advantage and disadvantage of this method are as follows:
- **Advantage**: you only need to configure Kubernetes Service resources.
- **Disadvantage**: potential risks of traffic load imbalance across pods (endpoints) may occur.

To enable the feature of preserving the client source IP, you can configure the `Service.spec.externalTrafficPolicy` field in Service resources. This field has two possible values, `Cluster` (default) and `Local`, which respectively indicate whether to route external traffic to the local or cluster endpoints of nodes, as shown in the figure below:
![externalTrafficPolicy](https://main.qcloudimg.com/raw/86ebb7dfe772cd1e290ed3783d2c4462.png)

 - `Cluster`: hides the client source IP. Service traffic of the `LoadBalancer` and `NodePort` types may be forwarded to the pods of other nodes.
 -  `Local`: preserves the client source IP and prevents service traffic of the `LoadBalancer` and `NodePort` types from being forwarded to the pods of other nodes. For more information, see [Create an External Load Balancer](https://kubernetes.io/zh/docs/tasks/access-application-cluster/create-external-load-balancer/). The sample YAML configuration is as follows:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: example-Service
spec:
  selector:
    app: example-Service
  ports:
    - port: 8765
      targetPort: 9376
  externalTrafficPolicy: Local
  type: LoadBalancer
```


### Obtaining the source IP address in the TKE native CLB-to-pod direct connection forwarding mode
The advantage and disadvantage of this method are as follows:
 - **Advantage**: this feature is supported by native TKE. You only need to complete configuration in the console based on the corresponding reference document.
 - **Disadvantage**: the VPC-CNI network mode needs to be enabled for the cluster. For more information, see [VPC-CNI Mode Description](https://intl.cloud.tencent.com/document/product/457/35250).

The CLB-to-pod direct connection forwarding is a TKE native feature, which is actually CLB pass-through forwarding and bypasses Kubernetes Service traffic forwarding) is used, the source IP address of a request received by backend pods is the real source IP address of the client. This method applies to layer-4 and layer-7 service forwarding scenarios. The following figure shows how the forwarding works:
![LB_TO_POD](https://main.qcloudimg.com/raw/bb9884e4b7bfaa776e8741a468694f65.jpg)
For more information and configuration details, see [Using CLB-to-Pod Direct Connection on TKE](https://intl.cloud.tencent.com/document/product/457/38408).


### Obtaining the source IP address through the HTTP header
The advantage and disadvantage of this method are as follows:
 - **Advantage**: this method is recommended for layer-7 (HTTP/HTTPS) traffic forwarding scenarios. The fields in the HTTP header can be directly obtained through web service proxy configuration or backend application code. In this way, the real source IP address of a client can be obtained easily and efficiently.
 - **Disadvantage**: this method only applies to layer-7 (HTTP/HTTPS) traffic forwarding scenarios, not layer-4 forwarding scenarios.



In layer-7 (HTTP/HTTPS) service forwarding scenarios, the real source IP address of a client can be obtained from the `X-Forwarded-For` and `X-Real-IP` fields in the HTTP header. There are two use cases in TKE, as shown in the figure below:
![HttpHeader](https://main.qcloudimg.com/raw/2f40628e7211e3043ed54cfebe7f6b77.png)

#### Scenario 1: using TKE Ingress to obtain the real source IP address
[CLB](https://intl.cloud.tencent.com/product/clb) (CLB layer-7) stores the real source IP address of a client in the `X-Forwarded-For` and `X-Real-IP` fields of the HTTP header by default. When service traffic goes through Service layer-4 forwarding, both fields are retained, and the backend can obtain the real source IP address of the client through web server proxy configuration or application code. For more information, see [Obtain Acutual IP for Layer 7 Load Balancing](https://intl.cloud.tencent.com/document/product/214/3728). The process for obtaining the source IP address in the TKE console is as follows:
1. Create a NodePort-type Service for workloads. In this document, nginx is used as an example, as shown in the figure below:
![](https://main.qcloudimg.com/raw/ad9c3c161c485ecbd1be91f09965a918.png)
2. Create an Ingress access entry for Service. In this document, test is used as an example, as shown in the figure below:
![](https://main.qcloudimg.com/raw/8db332b6cc7c26b7134a55f7a43dfe76.png)
3. After the configuration takes effect, you can obtain the real source IP address of a client from the `X-Forwarded-For` or `X-Real-IP` field of the HTTP header on the backend. The following figure shows the packet capture test results on the backend:
![](https://main.qcloudimg.com/raw/a5f36c927c12c616c37039fb0d7a5e76.png)


#### Scenario 2: using Nginx Ingress to obtain the real source IP address
Nginx Ingress service deployment requires Nginx Ingress to be able to perceive the real source IP address of a client. You can preserve the client source IP by [create an external load balancer](https://kubernetes.io/zh/docs/tasks/access-application-cluster/create-external-load-balancer/) or [using CLB-Pod direct connection on TKE](https://intl.cloud.tencent.com/document/product/457/38408). When forwarding requests, Nginx Ingress uses the `X-Forwarded-For` and `X-Real-IP` fields to store the client source IP, and the backend can obtain the real client source IP from these fields. The configuration process is as follows:

1. Nginx Ingress can be installed through TKE marketplace, custom YAML configuration, or the official (helm) installation method. For more information on its principles and deployment methods, see deployment solution 1 or 3 in [Deploying Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072). If you choose solution 1 for deployment, you must change the value of the `externalTrafficPolicy` field of Nginx Ingress Controller Service to `Local`.
After the installation is completed, a CLB (layer-4) access entry is automatically created for Nginx Ingress Controller Service, which can be checked in the TKE console as shown in the figure below:
![image-20200928153915958](https://main.qcloudimg.com/raw/669856ac57fe103c8fcf0d7088a9c880.png)
2. Create an Ingress for the backend server that requires forwarding, and configure forwarding rules. The sample YAML file is as follows:
```yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx  # ingressClass is "nginx".
  name: example
  namespace: default
spec:
  rules:  # Configure service forwarding rules
     - http:
        paths:
          - backend:
              serviceName: nginx  
              servicePort: 80
            path: /
```
3. After the configuration takes effect, you can obtain the real client source IP from the `X-Forwarded-For` or `X-Real-IP` field of the HTTP header on the backend. The following figure shows the packet capture test results on the backend:
![image-20200928195217294](https://main.qcloudimg.com/raw/5285ddcb8f56cb3efbc184293b7076b3.png)


### Obtaining the real source IP through TOA kernel component loading
The advantage and disadvantages of this method are as follows:
 - **Advantage**: in the TCP transmission mode, only the first TCP connection packet is reconstructed at the kernel layer with almost no performance loss.
 - **Disadvantages**:
  - You must load the TOA kernel component on cluster worker nodes and call functions on the server side to obtain the source IP address and port information carried by requests. The configuration and usage are relatively complex.
  - In the UDP transmission mode, each data packet is reconstructed to include option data (the source IP address and source port), which results in performance loss on the network transmission connection.


For the principles and loading method of the TOA kernel component, see [Obtaining the Real IPs of Access Users](https://intl.cloud.tencent.com/document/product/608/14426).



## References
- How Tencent CLB obtains real client IP addresses: [Obtaining Real IP for Layer 7 Load Balancing](https://intl.cloud.tencent.com/document/product/214/3728)
- Introduction to Tencent CLB: [Cloud Load Balancer](https://intl.cloud.tencent.com/product/clb)
- [Deploying Nginx Ingress on TKE](https://intl.cloud.tencent.com/document/product/457/38072) 
- Introduction to the TKE network mode: [GlobalRouter VPC-CNI Mode Description](https://intl.cloud.tencent.com/document/product/457/35250)
- [Using CLB-to-Pod Direct Connection on TKE](https://intl.cloud.tencent.com/document/product/457/38408)
- Introduction to TOA module usage: [Obtaining the Real IPs of Access Users](https://intl.cloud.tencent.com/document/product/608/14426)
- Description of external load balancer configuration for Kubernetes: [Create an External Load Balancer](https://kubernetes.io/zh/docs/tasks/access-application-cluster/create-external-load-balancer/)

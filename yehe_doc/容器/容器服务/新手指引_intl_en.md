This document helps you quickly understand and get started with Tencent Kubernetes Engine (TKE) as instructed.

## 1. What Is TKE?


Based on the native Kubernetes system, [TKE](https://intl.cloud.tencent.com/document/product/457/6759) provides container-centric, highly scalable and high-performance container management services. You can easily run applications on a hosted CVM instance cluster. Tencent Cloud also provides [Elastic Kubernetes Service (EKS)](https://intl.cloud.tencent.com/document/product/457/34040) and [Tencent Kubernetes Engine for Edge (TKE Edge)](https://intl.cloud.tencent.com/document/product/457/35390) so that you can choose the service you need.


TKE enables you to manipulate clusters and services through the [TKE console](https://console.cloud.tencent.com/tke2/overview) and [Kubectl](https://intl.cloud.tencent.com/document/product/457/30639).




## 2. TKE Billing
TKE charges cluster management fees based on the specifications of the managed clusters, and charges cloud resources fees based on the actual usage. For more information about the billing modes and prices, see [TKE Billing Overview](https://intl.cloud.tencent.com/document/product/457/45157).





## 3. Using TKE
#### 3.1 Registration and authentication
Before using TKE, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/zh/account/register) and complete the [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

#### 3.2 Role authorization
You need to authorize the current service role and grant operation permissions for TKE before accessing your other Tencent Cloud service resources.
Open the Tencent Cloud console, select **Products** > **Tencent Kubernetes Engine** to enter the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and authorize TKE according to the prompts. After that, get relevant resource operation permissions, and you can start to create a cluster.



#### 3.3 Creating a cluster
For information about how to quickly create a standard managed cluster, please see [Quickly Creating a Standard Cluster](https://intl.cloud.tencent.com/document/product/457/40029). For information about the complete processes of creating a standard managed cluster, please see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
If you need more types of clusters, please see [Creating Elastic Cluster](https://intl.cloud.tencent.com/document/product/457/34048) and [Creating Edge Cluster](https://intl.cloud.tencent.com/document/product/457/35385).


#### 3.4 Deploying workloads
You can deploy workloads by deploying images or orchestrating the YAML file.
- If you want to deploy stateless workloads through image templates, see directions in [Creating Simple Nginx Service](https://intl.cloud.tencent.com/document/product/457/7851) or [WordPress with Single Pod](https://intl.cloud.tencent.com/document/product/457/7205).
If you want to deploy workloads through custom images, see directions in [Building Hello World Service Manually](https://intl.cloud.tencent.com/document/product/457/7204).




####. 3.5 Cluster operations
TKE is a management platform for clusters, applications, storage and networks. For more information or directions, please refer to the table below.

| Features | Reference | 
|---------|---------|
| To connect to a TKE cluster from a local client using Kubectl, the Kubernetes command line tool | [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/30639) | 
| To upgrade a running Kubernetes cluster | [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640) |
| To add a pod to the created Kubernetes cluster | [Adding a Node](https://intl.cloud.tencent.com/document/product/457/30652) |
| To manage nodes in a Kubernetes cluster | [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901) |
| To operate native Kubernetes objects on the console | [ Kubernetes Object Management ](https://intl.cloud.tencent.com/document/product/457/30658) |
| To provide a fixed access entry for a set of containers through service | [Basic Features](https://intl.cloud.tencent.com/document/product/457/36833) |
| To configure different forwarding rules through Ingress resources | [Ingress Management](https://intl.cloud.tencent.com/document/product/457/37013) |
| To leverage TKE’s storage capability | [Storage Management Overview](https://intl.cloud.tencent.com/document/product/457/37769) |
| To assign the IP addresses within the container network address range to containers in the cluster | [Container Network Overview](https://intl.cloud.tencent.com/document/product/457/38966) |
| To store and analyze service logs in Kubernetes clusters | [Log Collection](https://intl.cloud.tencent.com/document/product/457/32419) |
| To monitor clusters | [TPS Instance Management](https://intl.cloud.tencent.com/document/product/457/38824) |
| To use a private image hosted in Tencent Container Registry (TCR) to deploy applications | [Using a Container Image in a TCR Enterprise Instance to Create a Workload](https://intl.cloud.tencent.com/document/product/457/36838) |



















## 4. Beginner's Guide	

- **Can I use TKE in classic network?**
No. Currently, you can use TKE in a VPC but not a classic network.

- **Can I add an existing CVM to a cluster?**
Yes. After creating a cluster, you can add an existing CVM to it. For more information, see [Adding a Node](https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9)

- **Why does my service keep starting?**
If there is no process running in the container, the service may keep starting. For more information on service startup, see [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).

- **How do I perform network planning before creating a cluster?**
When creating a cluster, make sure that the IP ranges of the cluster network and container network do not overlap. Generally, you can select a subnet of a VPC instance as the node network of the cluster. For more information, see [Container Network and Cluster Network Descriptions](https://intl.cloud.tencent.com/document/product/457/38966#.E5.AE.B9.E5.99.A8.E7.BD.91.E7.BB.9C.E4.B8.8E.E9.9B.86.E7.BE.A4.E7.BD.91.E7.BB.9C.E8.AF.B4.E6.98.8E).

- **How do I access a created service?**
Different access methods have different access entries. For more information, see the “Service Access” section in [Service Management Overview](https://intl.cloud.tencent.com/document/product/457/36832).

- **How does a container access the public network?
If the host where the container resides has a public IP address and public bandwidth, the container can directly access the public network. Otherwise, a NAT gateway is required for accessing the public network.

- **Can I use TKE if I don’t know how to create an image?**
The features related to Helm 3.0 that are integrated in TKE enable you to create products and services such as Helm Chart, TCR, and software services. Created applications will run in the cluster you specify to offer corresponding capabilities. For more information, see [Managing Applications](https://intl.cloud.tencent.com/document/product/457/30683).

- **How do I manage configuration files or environment variables for my services?**
You can manage configuration files by editing [configuration items](https://intl.cloud.tencent.com/document/product/457/30675).

- **How do services access each other?**
In a cluster, services with the same namespace can directly access one another, whereas those with different namespaces access one another by using `<service-name>.<namespace-name>.svc.cluster.local`.

## 5. Feedback and Suggestion	

If you have any doubts or suggestions when using TKE products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- If you have any questions regarding CLS documentation, such as links, content, or APIs, please click **Send Feedback** on the right of the documentation page.
- If you have any questions about products, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).


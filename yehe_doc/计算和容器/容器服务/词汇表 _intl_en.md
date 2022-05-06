

### App

See [Application](https://intl.cloud.tencent.com/document/product/457/18559) for the definition.



### EKS

See [Elastic Kubernetes Service](https://intl.cloud.tencent.com/document/product/457/18559) for the definition.



### Service

- In TKE, a service refers to a microservice that consists of multiple pods with the same configuration and rules for accessing these pods.
- In Serverless cloud applications, services are top-level resources for instances.



### Image Repository

An image repository is used to store Docker images, which are used to deploy TKE.

### Ingress

An ingress is a collection of rules for routing external HTTP(S) traffic to a service.



### Node

A node is a CVM instance that has been registered with a cluster.

### Cluster

A cluster refers to the collection of cloud resources required for container running, including several CVMs, CLB instances, and other Tencent Cloud resources.



### ConfigMap

A ConfigMap is a collection of configurations that help manage different environments and services.



### Tencent Kubernetes Engine

Tencent Kubernetes Engine (TKE) is a container-oriented management service with high scalability and performance based on native Kubernetes. It is fully compatible with native Kubernetes APIs and provides extended Kubernetes plugins such as CBS and CLB. It offers containerized applications with a complete set of features ranging from efficient deployment and resource scheduling to service discovery and dynamic scaling. It also solves environment consistency issues during development, testing, and OPS, making it much easier to manage large-scale container clusters and helping users reduce costs and improve efficiency.



### Instance

- In Game Server Engine (GSE), an instance corresponds to a CVM instance, that is, a CVM provided by GSE. You can view the specific type of the instance in the [GSE](https://console.cloud.tencent.com/gse/asset) console.
- On the TI-ML platform, a new instance is generated each time a workflow runs. Such instances include historical instances, parameter instances, re-run instances, and scheduled instances.
- In TKE, an instance consists of one or more associated containers that share the same storage and network space.
- In BatchCompute, an instance corresponds to a CVM instance. You can specify one or more instances to execute the same task. An instance is the minimum unit for batch scheduling and execution.
- In Data Security Governance Center (DSGC), an instance refers to the unit of data assets on Tencent Cloud, which varies for different types of data assets. An instance is a database for databases and a bucket for Cloud Object Storage (COS).
- In Tencent Container Registry (TCR), an instance is a dedicated container image hosting service that you can purchase in a specified region. The backend services and core data storage of your instance are independent of instances of other users. In native Docker, an instance is equivalent to an independent Docker Registry service. You can also consider an instance as a private Docker Registry service that you can purchase and deploy in the cloud.



### Elastic Kubernetes Service

Elastic Kubernetes Service (EKS) is a TKE service mode that allows you to deploy workloads without purchasing any nodes. EKS is fully compatible with native Kubernetes, allowing you to purchase and manage resources natively. This service is billed based on the actual amount of resources used by containers. In addition, EKS can be extended to support Tencent Cloud services, such as storage and network products. Meanwhile, EKS ensures secure isolation of containers and is ready to use out-of-the-box.

### TKE

See [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457/18559) for the definition.



### Application

- In Smart Building Operating System (SBOS) and Smart Building Running System (SBRS), applications refer to system software and service programs in the building.
- In TcaplusDB, an application refers to an application unit, which corresponds to the game application. AppID is displayed on the configuration information page and is used as a connection parameter for the TcaplusDB SDK connection table.
- In TKE, an application refers to a complete application program consisting of one or more services, which can be quickly deployed by using templates.
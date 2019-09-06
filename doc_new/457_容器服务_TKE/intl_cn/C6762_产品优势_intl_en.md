## Orchestration Advantages
#### Kubernetes-based Service

TKE is developed on the basis of Kubernetes (K8s), a container cluster management system made open-source by Google. Leveraging the Docker technology, Kubernetes provides containerized applications with a complete set of features ranging from deployment and execution and resource scheduling to service discovery and dynamic scaling, making it much easier to manage large-scale container clusters.

### Benefits of Kubernetes

- Using elegant software engineering consisting of modularization and microservices, Kubernetes implements a modular design that allows you to customize network, storage, scheduling, monitoring, and log modules as needed through flexible plugins.
- The Kubernetes project community acts as an open-source platform for the implementation of container, network, and storage.

### TKE vs. Customer Self-built Container Service

| Advantage | Tencent Cloud TKE | Customer Self-built Container Service |
|---------|---------|---------|
| Ease of use | <b>Simplified cluster management </b><br>Thanks to TKE, you can simplify the management of large-scale clusters and management and OPS of distributed applications without having to use cluster management software or design fault-tolerant cluster architecture. Simply launch TKE and specify the tasks you want to run, and then TKE will take care of all of the cluster management tasks, allowing you to focus on developing Dockerized applications.| When using a self-built container management infrastructure, you usually need to go through complex management processes such as installing, operating, and scaling your own cluster management software as well as configuring management systems and monitoring solutions. |
| Flexible scalability | <b>Flexible cluster management and integration with CLB </b><br>TKE supports elastic cluster hosting, making it easy to schedule long-running applications and batch jobs to expand your business. It also integrates Load Balance and supports traffic distribution among multiple containers, enabling automated recovery of unhealthy containers and ensuring that the number of containers meets your needs for application support.| You need to determine how to manually deploy container services according to the business traffic and health status, which has poor availability and scalability. |
| Security and stability | <b>High isolation of resources and high availability of services </b><br>TKE resides in a dedicated Cloud Virtual Machine (CVM) instance with computing resources exclusive to the tenant. The cluster runs on a VPC and supports custom security groups and network ACLs. TKE uses a distributed service architecture for management to enable automated failure recovery and rapid data migration. Combined with distributed storage of stateful service backends, it guarantees high service availability and data security.| Due to kernel issues and imperfect namespaces of self-built container services, isolation at the tenant, device, and kernel module levels is rather poor. |
| High efficiency | <b>Fast image deployment and continuous business integration </b><br>TKE runs on a high-quality BGP network, enabling instant image download and upload, rapid launch of massive containers in seconds and improved container deployment efficiency. It can quickly build, test and package the submitted business code and deploy the integrated code to pre-release and production environments. | The efficiency of using images to create containers cannot be guaranteed as the network quality of self-built container services may fluctuate significantly. |
| Low cost | <b>Free of charge TKE services </b><br>TKE itself is free to use, so you can build your cluster manager by calling the API in the container free of charge. Paid cloud service resources such as Cloud Virtual Machine and Cloud Block Storage created to store and run the applications will be billed according to relevant fee structures. | You need to spend big money creating, installing, operating, maintaining, and scaling your own cluster management infrastructures. |

### TKE Monitoring vs. Self-built Container Monitoring
TKE monitoring collects and displays comprehensive statistics of around 30 metrics such as cluster, service, pod, and container, allowing you to check cluster health and create alarms accordingly. In addition, more metrics will be available soon.

| Advantage | TKE | Self-built Container Service |
|---------|---------|---------|
| Complete set of metrics | Approximately 30 metrics are available, including cluster, service, container, and pod. | Only a few metrics are available and in-house development is required. |
| Low construction cost | TKE monitoring is provided when a cluster is created. | Monitoring needs to be constructed manually and and is very expensive. |
| Low OPS cost | Metric OPS is performed by the platform with guaranteed data accuracy. | Metrics need to be maintained manually. |
| Low storage cost | The data of each metric in the past three months is retained free of charge. | Fees are charged based on the storage size. |
| High scalability | TKE continues to improve and add new metrics. | Developers are required to construct new metrics. |
| Alarming | Available | Unavailable |
| Troubleshooting | Container logs can be viewed in the console and WebShell can be used to quickly log in to containers for troubleshooting. | You need to manually log in to containers or servers for troubleshooting. |

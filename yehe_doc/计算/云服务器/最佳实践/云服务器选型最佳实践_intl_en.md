

This document describes how to select a CVM model that suits you best from the aspects of features and scenarios, and provides detailed instructions and best practices.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ee418b21975d0150edbba7927171d85f.png" style="width:60%"/>

## Region and Availability Zone
#### Regions
A region is the geographical location of the cloud computing resource you purchase. It directly determines the network conditions for accessing the resource.
Note that there are regional differences on network quality, compliance policy and image use limits. For example, switching between Windows and Linux is only available in the Chinese mainland.

#### Availability zones
Each region has one or more availability zones. The available CVM instance types may vary with availability zone in the same region. The resource interconnection may suffer different network latency between availability zones.

For more information on regions and availability zones, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/213/6091).

## Instance Types
Tencent Cloud provides various instance types. Each type supports multiple instance specifications. CVM types can be divided into x86, ARM, bare metal, heterogeneous computing (GPU/FPGA), and BatchCompute according to the architecture. They can also be classified into Standard, Computing, Memory Optimized, High I/O, Big Data according to features. This document takes the second classification method as detailed below.

<dx-accordion>
::: Standard
Standard instances provide a balanced performance. They are suitable for most applications, such as websites and application integration. Standard instances mainly fall into the following families:
- S and SA: the S family comes with the Intel processor, while the SA family comes with the AMD processor. The S family of the same generation and configuration boasts better single-core performance, while the SA family delivers higher cost-effectiveness.
- Standard Storage Optimized S5se: based on the latest virtualization technology SPDK, S5se instances optimize the storage protocol stack and improve the overall cloud disk performance. They are suitable for IO-intensive applications such as large databases and NoSQL databases.
- Standard Network Optimized SN3ne: SN3ne instances provide a private network throughput up to 6,000,000 pps, with performance nearly 8 times greater than the Standard S3 instances. They can support up to 25 Gbps of private network bandwidth, with performance 2.5 times greater than the Standard S3 instances. They are suitable for scenarios that require sending and receiving massive network packets, such as video on-screen comments, live video broadcasting, and gaming.

::: 
::: Computing
This family provides the highest single-core computing performance, making it suitable for compute-intensive applications such as batch processing, high performance computing, and dedicated game servers. It is also applicable to other compute-intensive services such as high-traffic Web frontend server and massively multiplayer online (MMO) game servers.
:::
::: Memory Optimized
This family features a large memory, with a CPU/RAM ratio of 1:8 and the lowest price per GB of memory among instance types. It is suitable for applications that require memory-intensive operations, searches, and computations, such as high-performance databases (MySQL and Redis) and distributed in-memory caching.
:::
::: High I/O
This family uses local disk as the data disk. It is equipped with the latest NVME SSD storage featuring high random IOPS, high throughput and low latency. It provides an ultra-high IOPS at a low cost, making it suitable for I/O intensive applications that require fast disk I/O operations and low latency, such as high-performance relational databases, and Elasticsearch.
<dx-alert infotype="explain" title="">
IT instances use local disk as the data disk, which may lose data (e.g., when the host crashes). If your application cannot guarantee data reliability, we recommend you choose an instance that can use cloud disks as the data disk.
</dx-alert>
:::
::: Big Data
This family is equipped with massive storage resources, features high throughput, and is suitable for throughput-intensive applications such as Hadoop distributed computing, massive log processing, distributed file systems, and large data warehouses.

<dx-alert infotype="explain" title="">
D instances use local disk as the data disk, which may lose data (e.g., when the host crashes). If your application cannot guarantee data reliability, we recommend you choose an instance that can use cloud disks as the data disk.
</dx-alert>
:::
::: Heterogeneous Computing
This family is equipped with heterogeneous hardware such as GPU and FPGA to deliver real-time, fast parallel computing and floating-point computing capabilities. It is suitable for high-performance applications such as deep learning, scientific computing, video encoding/decoding, and graphics workstations.
NVIDIA GPU instances use NVIDIA Tesla GPUs, including the current mainstream choice T4/V100, and the latest generation V100, to provide excellent general-purpose computing capability, making this the top choice for applications such as deep learning training/inference and scientific computing.
:::
::: Cloud Physical Server 2.0
Cloud Physical Machine (CPM) 2.0 is an elastic high-performing bare metal instance built on the latest virtualization technology of Tencent Cloud. It combines the elasticity of a virtual machine with the stability of a physical machine. It can be integrated seamlessly with all Tencent Cloud services such as networks and databases, and suitable for standard, high I/O, big data, and heterogeneous computing scenarios. CPM 2.0 supports third-party virtualization platforms and can help you build dedicated and isolated high-performance physical server clusters rapidly. With the nested virtualization technology, it also supports efficient and advanced hybrid cloud deployment with AnyStack.
:::
::: High-performance Computing Cluster
High-performance computing cluster (HPC) is a cloud computing cluster that uses CPM 2.0 as compute nodes and provides high-speed RDMA network connection. It can be widely used in large-scale computing scenarios such as automotive simulation, fluid dynamics, and molecular dynamics. It also provides high-performance heterogeneous resources to support scenarios including large-scale machine learning and training.
:::
</dx-accordion>

<br>
For more information about CVM instance types, see <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.


## Recommended Model for Common Use Cases
<table>
<tr>
<th style="width: 14%;">Use Case</th><th style="width: 19%;">Common Software</th>
<th style="width: 47%;">Description</th><th style="width: 20%;">Recommended Model</th>
</tr>
<tr>
<td>Web service</td>
<td>Nginx<br>Apache</td>
<td>The Web service generally covers personal website, blog, and large-scale ecommerce website. This use case requires a balance of compute, storage, and memory resources. We recommend <b>Standard</b> instances.</td>
<td>Standard S and SA</td>
</tr>
<tr>
<td>Middleware</td>
<td>Kafka<br> MQ</td>
<td>The message queue service requires relatively balanced compute and memory resources. We recommend <b>Standard</b> instances using cloud disk as storage.</td>
<td>Standard S<br>Computing C</td>
</tr>
<tr>
<td>Database</td>
<td>MySQL</td>
<td>The database business requires extremely high I/O performance. We recommend instances using SSD cloud disks and local disks. When selecting an instance using local disk, remember to back up data to avoid data loss.</td>
<td>High I/O IT<br>Memory Optimized M</td>
</tr>
<tr>
<td>Cache</td>
<td>Redis<br>Memcache</td>
<td>The cache business has a high requirement for memory and moderate requirement for computing performance. We recommend <b>Memory Optimized</b> instances for the high CPU/RAM ratio.</td>
<td>Memory Optimized M</td>
</tr>
<tr>
<td>Big data</td>
<td>Hadoop<br>ES</td>
<td>The big data business requires mass storage and moderate I/O throughput. We recommend <b>Big Data </b>instances. When selecting an instance using local disk, remember to back up data to avoid data loss.</td>
<td>Big Data D</td>
</tr>
<tr>
<td>High performance computing</td>
<td>StarCCM<br>WRF-Chem</td>
<td>The high performance computing business requires both the ultimate single-machine computing power and the efficient multi-machine scaling. We recommend <b>HPC</b> with the high-speed RDMA network connection or <b>Compute</b> instances.</td>
<td>HPC<br>Compute C</td>
</tr>
<tr>
<td>Virtualization</td>
<td>Kvm<br>OpenStack</td>
<td>The virtualization application requires the nested virtualization of a cloud server without incurring additional performance overhead while maintaining the virtualization capability like a physical machine. We recommend CPM 2.0 products.</td>
<td>HPC<br>CPM 2.0</td>
</tr>
<tr>
<td>Video rendering</td>
<td>Unity<br>UE4</td>
<td>The video rendering business requires supporting graphic and image processing APIs, such as DirectX and OpenGL. We recommend <b>GPU Rendering GN7vw</b> instances.</td>
<td>GPU Rendering GN7vw</td>
</tr>
<tr>
<td>AI-based computing</td>
<td>TensorFlow<br>CUDA</td>
<td>The AI-based computing business requires the parallel processing capability, high GPU computing power, and video memory.</td>
<td>GPU Computing<br>HPC</td>
</tr>
</table>



## Relevant Products
### Associated Tencent Cloud services
You can purchase other Tencent Cloud services to work with CVM instances as needed. This document takes building a website as an example to describe the associated Tencent Cloud services.
<img src="https://qcloudimg.tencent-cloud.cn/raw/593f4e137fc7959febc71a8982621a47.png" style="width:70%"/>

### Other Tencent Cloud services
You can also select other Tencent Cloud services to meet your specific requirements. For example, after deploying applications, you can use the following Tencent Cloud services to implement disaster recovery to ensure the system robustness and provide data security:
- **[Snapshot Overview](https://intl.cloud.tencent.com/document/product/362/31638)**
Snapshot provides a convenient and efficient data protection service, which is also a very important and effective data disaster recovery measure. Snapshots are recommended for business scenarios including daily data backup, quick data recovery, application of multiple replicas of production data, and quick environment deployment. Creating snapshots will incur a small fee, as detailed in [Snapshot Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415).
- **Tencent Cloud Observability Platform [Product Overview](https://intl.cloud.tencent.com/document/product/248/32799)**
Setting alarm rules for cloud resources is also vital to business operation. You can view comprehensive information such as resource utilization, application performance and operation status of the Tencent Cloud services on Tencent Cloud Observability Platform (TCOP). The platform also provides features such as multi-metric monitoring, custom alarms, cross-region and cross-project instance grouping, dashboards for visual monitoring, and Prometheus hosting. TCOP can help you detect and handle emergencies in Tencent Cloud services, thereby enhancing system stability, improving OPS efficiency, and reducing OPS costs.
- **[Tencent Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524)**
You can use the Tencent Cloud Load Balancer (CLB) service to protect your business from single points of failure. CLB virtualizes multiple CVM instances in the same region into a high-performance and high-availability application service pool by setting a virtual IP address (VIP) and then distributes the network requests from clients to the pool in the manner specified by the application.
CLB checks the health of the instances in the pool and automatically isolates unhealthy ones, thus resolving single points of failure issues and improving the overall service capabilities of the applications.


## References
- [Regions and AZs](https://intl.cloud.tencent.com/document/product/213/6091)
- [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518)




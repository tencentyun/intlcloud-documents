Please evaluate your business situations before using EMR:

## Selecting Model Specifications
EMR offers a wide variety of CVM instance models, including EMR Standard, EMR Compute, EMR High IO, EMR MEM-optimized, and EMR Big Data. If you need CPM models, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

You can choose the most appropriate model based on your business needs and budget.
- If you require low latency for offline computation, we recommend you to choose the model with a local disk.
- If you need to use the real-time database HBase, we recommend you to choose the EMR High IO model with a local SSD disk for optimal performance.

### Node Specification Recommendations
- **Master node**: A master node mainly performs cluster scheduling and task submission. It does not require high computing power; however, depending on the actual situation, it may require a larger memory. EMR Standard 4-core 8 GB, 4-core 16 GB, or higher-spec models are usually recommended.

- **Core node**: As a core node is used for computing and storage tasks, it has high requirements for CPU, memory, and disk. However, if your data is completely stored in COS, then the role of the core node is basically the same as that of a task node. In this case, a local disk is recommended to improve the I/O capability and get the computation results faster.

- **Task node**: As a task node is responsible for computation only and the data for computation comes from a core node or COS, its disk size does not need to be too large; however, it is recommended to select at least 500 GB for it to ensure the computation efficiency.

- **Common node**: Currently, the specification of a common node is EMR Standard 2-core 4 GB model with a local disk of 100 GB by default.

- **Router node**: A router node is mainly used to relieve the load of the master node and as a task submitter; therefore, it is recommended to select a model with larger memory, preferably not lower than the master node specification.

## Network and Security
To ensure the network security of the EMR cluster, it is placed in a VPC, and a security group policy is added to the VPC. In addition, to ensure that the web UI of Hadoop can be easily accessed, one of the master nodes is configured with a public IP which is billed by traffic. A router node has no public IPs by default. If you need one for it, you can bind it to an EIP in the [CVM Console](https://console.cloud.tencent.com/cvm/eip).

>
>- A public IP is enabled for a master node when a cluster is created, but you can disable it based on the actual conditions.
>- Enabling the public IP for the master node is mainly for SSH login and component viewing in the web UI.
>- A master node with a public IP enabled is billed by traffic with a bandwidth of up to 5 Mbps. Once the cluster is created, you can make adjustments to its network in the console.

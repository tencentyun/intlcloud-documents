Data Lake Accelerator Goose FileSystem (GooseFS) is a highly available, reliable, and elastic data lake acceleration service provided by Tencent Cloud. By using COS as the data lake storage base, it reduces the storage costs and offers a unified entry for computing applications in the data lake ecosystem, so as to accelerate the access of businesses such as big data analysis, machine learning, and AI. It uses a robust distributed cluster architecture to furnish a unified namespace and access protocol for upper-layer computing applications, making it easier for you to manage and transfer data across different storage systems.

## Product Features

GooseFS aims to offer a one-stop cache solution and has native strengths in leveraging data locality, high-speed cache, and unified storage access syntax. It plays a core role in the data lake ecosystem as a connector between computing and storage as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/340d0455880b295e1990fef8182275c7.png)

GooseFS has the following features:

1. Cache acceleration and data locality: GooseFS can be deployed together with compute nodes to improve the data locality. Its high-speed cache feature can improve the storage performance and increase the bandwidth of data write to COS.
2. Integrated storage syntax: GooseFS provides unified file system (UFS) syntax to support the storage syntax of multiple storage services, such as COS, Hadoop, S3, K8s CSI, and FUSE, making it suitable for various ecosystems and use cases.
3. Tencent Cloud ecosystem services: Log, authentication, and monitoring services are available to enable the same operations as in COS.
4. Namespace management capabilities: GooseFS comes with different cache read/write and TTL management policies for different businesses and under file systems.
6. Metadata table sensing: GooseFS Catalog can sense metadata table in big data scenarios to prefetch cache at the table level.


## Benefits

GooseFS has the following strengths in data lake scenarios:

### Data I/O performance

GooseFS enables a distributed shared cache near compute nodes, where upper-layer computing applications can transparently and efficiently cache the hot data that needs to be accessed frequently to accelerate the data I/O. It also has the metadata cache feature to make metadata operations in big data scenarios faster, such as file data query and file list display. Together with big data buckets, it can further expedite file renaming. In addition, it allows you to choose different storage media, including MEM, SSD, NVMe, and HDD, based on your business needs to balance the business costs and data access performance.

### Integrated storage

GooseFS provides a unified namespace that supports the storage syntax of not only COS but also many other storage services such as HDFS, K8s CSI, and FUSE. This furnishes a unified integrated storage solution for upper-layer businesses and simplifies the business Ops configuration. Integrated storage breaks the barriers between different data bases and makes it easier for upper-layer applications to manage and transfer data, thus improving the data usage efficiency. 

### Ecosystem affinity

GooseFS is fully compatible with the Tencent Cloud big data platform framework and can also be deployed on premises in a custom manner, showing an excellent ecosystem affinity. For example, you can use GooseFS in EMR to accelerate big data businesses and conveniently deploy it in CVM or self-built IDC. In addition, it supports transparent acceleration. If you have already activated COSN and CHDFS, you can simply modify the configurations to automatically accelerate COSN and CHDFS business access via GooseFS with no need to modify business code and access paths.

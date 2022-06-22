## Overview 

[Fluid](https://github.com/fluid-cloudnative/fluid) is an open-source Kubernetes-native distributed dataset orchestrator and accelerator for data-intensive applications, such as big data and AI. It is hosted by the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/sandbox-projects/) as a sandbox project. By defining the abstraction of dataset resources, it features:

- **Native support for dataset abstraction**: Implements the basic capabilities required for data-intensive applications to achieve efficient data access and reduce the cost of multidimensional management.
- **Cloud data prefetch and acceleration**: Fluid provides data prefetch and acceleration for cloud applications by using a distributed cache engine (GooseFS/Alluxio) with data observability, portability, and horizontal scalability.
- **Co-orchestration for data and applications**: During application and data scheduling on the cloud, it takes their characteristics and location into consideration to improve the performance.
- **Multi-namespace management support**: Allows you to create and manage datasets in different namespaces.
- **Heterogeneous data source management**: Unifies the access to underlying data from different sources (COS, HDFS, and Ceph), applicable to hybrid cloud use cases.

## Key Concepts

**Dataset**: A dataset is a set of logically related data that can be used by computing engines, such as Spark for big data and TensorFlow for AI. Smart data applications create core industry values. Managing datasets may require features in different dimensions, such as security, version management, and data acceleration.

**Runtime**: The execution engine that enforces dataset security and provides version management and data acceleration capabilities. It defines a set of APIs for dataset management and acceleration throughout the lifecycle.

**GooseFS Runtime**: It is a Java-based implementation of the execution engine developed by Tencent Cloud's COS team, supporting dataset management, caching, and COS. GooseFS is a Tencent Cloud product with dedicated product-level support, but its code is not open-source. Fluid enables dataset visualization, elastic scaling, and data migration by managing and scheduling GooseFS Runtime.

**Alluxio Runtime**: Based on open-source Alluxio, it is an implementation of the execution engine for dataset management and caching, supporting PVC, Ceph, and CPFS computing, thereby effectively supporting hybrid cloud use cases. Alluxio is an open-source scheme. In spite of the joint efforts of Tencent Cloud and the community to promote the stability and performance of its data caching, there will be a delay in timeliness and response. Fluid enables dataset visualization, elastic scaling, and data migration by managing and scheduling Alluxio Runtime.

|    -          | Alluxio                       | GooseFS                                 |
| ------------ | ----------------------------- | --------------------------------------- |
| Underlying storage types | PVC, Ceph, HDFS, CPFS, NFS | OSS, EMR, PVC, Ceph, HDFS, CPFS, NFS |
| Support     | Open-source community                      | Tencent Cloud products                              |

## Add-on Installation

### Prerequisite dependencies

- Kubernetes cluster (v1.14 or later)
- CSI support in the cluster

### Parameter configuration

During Helm deployment, all configuration items are included in `values.yaml`.
Some fields may need to be customized, as listed below:

| Parameter     | Description     | Default Value     |
| ------- | -------- | --------- |
| `workdir` | Backup address of the metadata in the cache engine | `/tmp`|
| `dataset.controller.image.repository` | Repository where the dataset controller image resides  | `ccr.ccs.tencentyun.com/fluid/dataset-controller` |
| `dataset.controller.image.tag`        | Dataset controller image version    | `"v0.6.0-0bfc552"` |
| `csi.registrar.image.repository`   | Repository where the CSI registrar image resides | `"ccr.ccs.tencentyun.com/fluid/csi-node-driver-registrar"` |
| `csi.registrar.image.tag`   | CSI registrar image version | `"v1.2.0"` |
| `csi.plugins.image.repository`   | Repository where the CSI plugins image resides | `"ccr.ccs.tencentyun.com/fluid/fluid-csi"` |
| `csi.plugins.image.tag`   | CSI plugins image version | `"v0.6.0-def5316"` |
| `csi.kubelet.rootDir`   | `kubelet root` folder | `"/var/lib/kubelet"` |
| `runtime.mountRoot`   | Root address of the FUSE mount in the cache engine | `"/var/lib/kubelet"` |
| `runtime.goosefs.enable`   | Enable GooseFS cache engine | `"true"` |
| `runtime.goosefs.init.image.repository`   | Repository where the initialized image of the GooseFS cache engine resides | `"ccr.ccs.tencentyun.com/fluid/init-users"` |
| `runtime.goosefs.init.image.tag`   | Version of the initialized image of the GooseFS cache engine | `"v0.6.0-0cd802e"` |
| `runtime.goosefs.controller.image.repository`   | Repository where the controller image of the GooseFS cache engine resides | `"ccr.ccs.tencentyun.com/fluid/goosefsruntime-controller"` |
| `runtime.goosefs.controller.image.tag`   | Version of the controller image of the GooseFS cache engine | `"v0.6.0-bbf4ea0"` |
| `runtime.goosefs.runtime.image.repository`   | Repository where the GooseFS cache engine image resides | `"ccr.ccs.tencentyun.com/fluid/goosefs"` |
| `runtime.goosefs.runtime.image.tag`   | Version of the GooseFS cache engine image | `"v1.1.10"` |
| `runtime.goosefs.fuse.image.repository`   | Repository where the FUSE add-on image of the GooseFS cache engine resides | `"ccr.ccs.tencentyun.com/fluid/goosefs-fuse"` |
| `runtime.goosefs.fuse.image.tag`   | Version of the FUSE add-on image of the GooseFS cache engine | `"v1.1.10"` |
| `runtime.alluxio.runtimeWorkers`   | Maximum number of the concurrent workers of the Alluxio cache engine controller | `"3"` |
| `runtime.alluxio.portRange`   | Alluxio cache engine add-on port range | `"20000-26000"` |
| `runtime.alluxio.enable`   | Enable Alluxio cache engine | `"true"` |
| `runtime.alluxio.init.image.repository`   | Repository where the initialization image of the Alluxio cache engine resides | `"ccr.ccs.tencentyun.com/fluid/init-users"` |
| `runtime.alluxio.init.image.tag`   | Version of the initialization image of the Alluxio cache engine | `"v0.6.0-def5316"` |
| `runtime.alluxio.controller.image.repository`   | Repository where the controller image of the Alluxio cache engine resides | `"ccr.ccs.tencentyun.com/fluid/alluxioruntime-controller"` |
| `runtime.alluxio.controller.image.tag`   | Version of the controller image of the Alluxio cache engine | `"v0.6.0-0cd802e"` |
| `runtime.alluxio.runtime.image.repository`   | Repository where the Alluxio cache engine image resides | `"ccr.ccs.tencentyun.com/alluxio/alluxio"` |
| `runtime.alluxio.runtime.image.tag`   | Version of the Alluxio cache engine image | `"release-2.5.0-2-SNAPSHOT-a05eadcff1"` |
| `runtime.alluxio.fuse.image.repository`   | Repository where the FUSE add-on image of the Alluxio cache engine resides | `"ccr.ccs.tencentyun.com/alluxio/alluxio-fuse"` |
| `runtime.alluxio.fuse.image.tag`   | Version of the FUSE add-on image of the Alluxio cache engine | `"release-2.5.0-2-SNAPSHOT-a05eadcff1"` |

## Best Practices

For more information, see the Fluid [documentation](https://github.com/fluid-cloudnative/fluid/blob/master/docs/zh/TOC.md).

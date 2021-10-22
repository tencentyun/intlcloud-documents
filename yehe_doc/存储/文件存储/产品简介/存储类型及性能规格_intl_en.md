CFS provides file systems with scalable storage, which can work with other Tencent Cloud services such as CVM, TKE, and BatchCompute. CFS offers four storage classes, including Standard, Standard Turbo, High-Performance, and High-Performance Turbo. You can select one to fit your business needs.

### Standard

Standard is a general file system that uses mixed media. It uses data tiers to accelerate reads/writes. In addition, by using three replicas and a high-availability (HA) failover system, it ensures data reliability and service high availability, making it suitable for scenarios that require small-scale general data storage.

### Standard Turbo

Standard Turbo is a parallel file system that uses mixed media and an asymmetric framework. The data nodes and metadata nodes are deployed independently. By allowing mounting with a private protocol, the performance of a single client can be like a storage cluster. In addition, underlying resources are isolated to ensure exclusive storage for the cluster. It also uses three replicas and hot data migration to ensure data reliability and service high availability, making it suitable for scenarios that require large-scale throughput and mixed loads.

### High-Performance

High-Performance is a general file system that uses NVMe only. It uses data tiers to provide high-performance storage. In addition, it uses three replicas and a HA failover system to ensure data reliability and service high availability, making it suitable for small-scale core businesses that are latency-sensitive.

### High-Performance Turbo

High-Performance Turbo is a parallel file system that uses NVMe only and an asymmetric framework. The data nodes and metadata nodes are deployed independently. By allowing mounting with a private protocol, the performance of a single client can be like a storage cluster. In addition, underlying resources are isolated to ensure exclusive storage for the cluster. It also uses three replicas and hot data migration to ensure data reliability and service high availability, making it suitable for scenarios that use large-scale small files.

<table> 
    <tr align="center">
        <td width="" >Product Type</td>
        <td width="21%" colspan="2">Standard</td>
        <td width="21%" colspan="2">High-Performance</td>
    <tr align="center">
        <td width="" >Product Name</td>
        <td width="20%" >Standard</td>
        <td width="20%" >Standard Turbo</td>
        <td width="20%" >High-Performance</td>
        <td width="20%">High-Performance Turbo </td>
    </tr>
    <tr align="center">
        <td>Positioning</td>
        <td>Cost-effective, suitable for small-scale general data storage</td>
        <td>High-throughput and large storage, suitable for businesses that require high throughput and mixed loads</td>
        <td>High-performance and low latency, suitable for small-scale core businesses that are latency-sensitive</td>
        <td>High-throughput and high IOPS, suitable for businesses that use large-scale small files</td>
    </tr>
    <tr align="center" >
        <td>Scenario</td>
        <td>Small-scale enterprise file sharing, web services, data backup/archive, and log storage</td>
        <td>High-performance and large-scale web services, media, image rendering, AI inference, OLAP services, and high-performance computation</td>
        <td>Small-scale CI/CD development and testing environments, high-performance Web services, OLTP databases, and high-performance file sharing</td>
        <td>High-performance and large-scale computation, AI training, databases, big data analysis, and OLAP services</td>
    </tr>
    <tr align="center" >
        <td>Storage capacity</td>
        <td>0−160 TiB</td>
        <td>40 TiB−100 PiB</td>
        <td>100 GiB−32 TiB</td>
        <td>20 TiB−100 PiB</td>
    </tr>
    <tr align="center" >
        <td>Bandwidth (MiB/s)</td>
        <td>Min {100 + 0.1 × Capacity in GiB , 300}</td>
				<td><nobr>Min{0.1 × Capacity in GiB , 100,000}</nobr></td>
        <td>Min{200 + 0.5 × Capacity in GiB , 2,048}</nobr></td>
        <td><nobr>Min{0.2 × Capacity in GiB , 100,000}</nobr></td>
    <tr align="center" >
        <td>Read IOPS</td>
        <td>Min{1800 + 8 × Capacity in GiB , 6,000}</td>
        <td><nobr>Min{2 × Capacity in GiB , 2 million}</nobr></td>
        <td>Min{4000 + 50 × Capacity in GiB , 100,000}</td>
        <td><nobr>Min{20 × Capacity in GiB , 10 million}</nobr></td>
    <tr align="center" >
        <td>Write IOPS</td>
        <td>Min{1800 + 8 × Capacity in GiB , 6,000} </td>
        <td>Min{1 × Capacity in GiB , 1 million}</td>
        <td>Min{4000 + 50 × Capacity in GiB , 100,000}</td>
        <td>Min{5 × Capacity in GiB , 3 million}</td>
    </tr>
    <tr align="center" >
        <td>OPS upper threshold</td>
        <td>Read/Write: 10,000/1,000</td>
        <td>Read/Write: 300,000/20,000</td>
        <td>Read/Write: 50,000/5,000</td>
        <td>Read/Write: 300,000/20,000</td>
    <tr align="center" >
        <td>Latency</td>
        <td>4K single-stream read:3 ms</br>4K single-stream write: 7 ms</td>
        <td>4K single-stream read: 0.2 ms</br>4K single-stream write: 3 ms</td>
        <td>4K single-stream read: 0.5 ms</br>4K single-stream write: 1.5 ms</td>
        <td>4K single-stream read: 0.2 ms</br>4K single-stream write: 1.5 ms</td>
    </tr>
    <tr align="center" >
        <td>Cost</td>
        <td>0.058 USD/GiB/month</td>
        <td>0.09 USD/GiB/month</td>
        <td>0.23 USD/GiB/month</td>
        <td>0.15 USD/GiB/month</td>
    </tr>
    <tr align="center" >
        <td>Supported protocol</td>
        <td>NFS/SMB</td>
        <td>POSIX/MPI</td>
        <td>NFS/SMB</td>
        <td>POSIX/MPI</td>
    </tr>
    <tr align="center" >
        <td>Expansion</td>
        <td>Auto</td>
        <td>Manual</td>
        <td>Auto</td>
        <td>Manual</td>
    </tr>
    <tr align="center" >
        <td>Supported OS</td>
        <td>Linux/Windows</td>
        <td>Linux</td>
        <td>Linux/Windows</td>
        <td>Linux</td>
    </tr>
</table>

## Description

- In the performance-related formulas, the capacities of Standard Turbo and High-Performance Turbo refer to the capacities purchased for the cluster. For Standard and High-Performance, the capacities refer to the storage that is actually used by the instances.
- The table above shows the capabilities of the file system. To reach the performance upper threshold, you usually need to perform multi-threaded reads/writes using multiple compute nodes.
- The performance benchmark is tested in interruption-free conditions. The results of mixed tests or other loads might vary.
- OPS suggests the file system’s ability to process metadata per second, which is not the same as IOPS.
- High-Performance is still in beta testing and will be rolled out around early October 2021.


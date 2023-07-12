CFS provides file systems with scalable storage, which can work with other Tencent Cloud services such as CVM, TKE, and BatchCompute. CFS offers the following storage classes, and you can select one based on your business needs.

## Storage Classes

### Standard

Standard is a highly cost-effective file system that uses mixed media and accelerates data reads/writes through a data tiering mechanism. Three replicas on three independent physical servers on different racks are provided to guarantee strong consistency and successful storage of every data entry written to the file system. Its access server features hot data migration to ensure data reliability and high service availability, making it suitable for scenarios that require small-scale general data storage.

### High-Performance

High-Performance is a low-latency file system that uses NVMe only and provides a high storage performance through a data tiering mechanism. Three replicas on three independent physical servers on different racks are provided to guarantee strong consistency and successful storage of every data entry written to the file system. Its access server features hot data migration to ensure data reliability and service high availability, making it suitable for small-scale core businesses that are latency-sensitive.

### Standard Turbo

Standard Turbo is a parallel file system that uses mixed media and an asymmetric framework. The data nodes and metadata nodes are deployed independently. By allowing mounting over a private protocol, the performance of a single client can be like a storage cluster. In addition, underlying resources are isolated to ensure exclusive storage for the cluster. Three replicas on three independent physical servers on different racks are provided to guarantee strong consistency and successful storage of every data entry written to the file system. Its access server features hot data migration to ensure data reliability and service high availability, making it suitable for businesses that require high throughput and mixed loads.

### High-Performance Turbo

High-Performance Turbo is a high-bandwidth, low-latency, parallel file system that uses NVMe only and an asymmetric framework. The data nodes and metadata nodes are deployed independently. By allowing mounting over a private protocol, the performance of a single client can be like a storage cluster. In addition, underlying resources are isolated to ensure exclusive storage for the cluster. Three replicas on three independent physical servers on different racks are provided to guarantee strong consistency and successful storage of every data entry written to the file system. Its access server features hot data migration to ensure data reliability and high service availability, making it suitable for scenarios that use large numbers of small files.

### High-Throughput

High-Throughput is a parallel file system that uses a layered framework. It provides more flexible bandwidth scaling and access over the SMB protocol, meeting the storage requirements for a small capacity and high bandwidth. Three replicas on three independent physical servers on different racks are provided to guarantee strong consistency and successful storage of every data entry written to the file system. Its access server features hot data migration to ensure data reliability and high service availability, making it suitable for read-intensive scenarios such as rendering, game battle server, and non-linear editing.

## Performance and Specifications

### General series

<table> 
    <tr align="center">
    <tr align="center">
        <th style="width: 17%;">Product Name</th>
        <th style="width: 41.5%;">Standard</th>
        <th style="width: 41.5%;">High-Performance</th>
    </tr>
    <tr align="center">
        <td>Positioning</td>
        <td>Cost-effective, suitable for small-scale general data storage</td>
        <td>High performance and low latency, suitable for small-scale latency-sensitive core businesses</td>
    </tr>
    <tr align="center" >
        <td>Scenario</td>
        <td>Small-scale enterprise file sharing, data backup/archive, and log storage</td>
        <td>Small-scale CI/CD development and testing environments, high-performance web services, OLTP databases, and high-performance file sharing</td>
    </tr>
    <tr align="center" >
        <td>Storage capacity</td>
        <td>0−160 TiB</td>
        <td>0−32 TiB</td>
    </tr>
    <tr align="center" >
        <td>Bandwidth (MiB/s)</td>
        <td>Min {100 + 0.1 × Capacity in GiB , 300}</td>
        <td>Min{200 + 0.2 × Capacity in GiB , 1,024}</nobr></td>
    <tr align="center" >
        <td>Read IOPS</td>
        <td>min{2000 + 8 × Size in GiB , 15,000}</td>
        <td>Min{2,500 + 30 × Size in GiB, 30,000}</td>
    <tr align="center" >
        <td>Write IOPS</td>
        <td>min{2000 + 8 × Size in GiB , 15,000}</td>
        <td>Min{2,500 + 30 × Size in GiB, 30,000}</td>
    </tr>
    <tr align="center" >
        <td>OPS upper threshold</td>
        <td>Read/Write: 10,000/1,000</td>
        <td>Read/Write: 30,000/3,000</td>
    <tr align="center" >
        <td>Latency</td>
        <td>4K single-stream read:3 ms</br>4K single-stream write: 7 ms</td>
        <td>4K single-stream read: 1 ms</br>4K single-stream write: 1.5 ms</td>
    </tr>
    <tr align="center" >
        <td>Cost</td>
        <td>0.058 USD/GiB/month</td>
        <td>0.23 USD/GiB/month</td>
    </tr>
    <tr align="center" >
        <td>Supported protocol</td>
        <td>NFS/SMB</td>
        <td>NFS</td>
    </tr>
    <tr align="center" >
        <td>Expansion</td>
        <td>Auto</td>
        <td>Auto</td>
    </tr>
    <tr align="center" >
        <td>Supported OS</td>
        <td>Linux/Windows</td>
        <td>Linux/Windows</td>
    </tr>
</table>




### Turbo series

<table> 
    <tr align="center">
        <th style="width: 17%;">Product Name</th>
        <th style="width: 41.5%;">Standard Turbo</th>
        <th style="width: 41.5%;">High-Performance Turbo</th>
    </tr>
    <tr align="center">
        <td>Positioning</td>
        <td>High-throughput and large storage, suitable for businesses that require high throughput and mixed loads</td>
        <td>High-throughput and high IOPS, suitable for businesses that use large-scale small files</td>
    </tr>
    <tr align="center" >
        <td>Scenario</td>
        <td>Non-linear media asset editing, image rendering, AI inferencing, OLAP business, and high-performance computing</td>
        <td>High-performance and large-scale computation, AI training, OLTP databases, big data analysis, and OLAP services</td>
    </tr>
    <tr align="center" >
        <td>Storage capacity</td>
        <td>40 TiB−100 PiB</td>
        <td>20 TiB−100 PiB</td>
    </tr>
    <tr align="center" >
        <td>Bandwidth (MiB/s)</td>
				<td><nobr>Min{0.1 × Capacity in GiB , 100,000}</nobr></td>
        <td><nobr>Min{0.2 × Capacity in GiB , 100,000}</nobr></td>
    <tr align="center" >
        <td>Read IOPS</td>
        <td><nobr>Min{2 × Capacity in GiB , 2 million}</nobr></td>
        <td><nobr>Min{20 × Capacity in GiB , 10 million}</nobr></td>
    <tr align="center" >
        <td>Write IOPS</td>
        <td>Min{1 × Capacity in GiB , 1 million}</td>
        <td>Min{5 × Capacity in GiB , 3 million}</td>
    </tr>
    <tr align="center" >
        <td>OPS upper threshold</td>
        <td>Read/Write: 300,000/20,000</td>
        <td>Read/Write: 300,000/20,000</td>
    <tr align="center" >
        <td>Latency</td>
        <td>4K single-stream read: 0.2 ms</br>4K single-stream write: 3 ms</td>
        <td>4K single-stream read: 0.2 ms</br>4K single-stream write: 1.5 ms</td>
    </tr>
    <tr align="center" >
        <td>Cost</td>
        <td>0.09 USD/GiB/month</td>
        <td>0.15 USD/GiB/month</td>
    </tr>
    <tr align="center" >
        <td>Supported protocol</td>
        <td>POSIX/MPI</td>
        <td>POSIX/MPI</td>
    </tr>
    <tr align="center" >
        <td>Expansion</td>
        <td>Manual</td>
        <td>Manual</td>
    </tr>
    <tr align="center" >
        <td>Supported OS</td>
        <td>Linux</td>
        <td>Linux</td>
    </tr>
</table>


### High-Throughput

<table> 
    <tr align="center">
        <th style="width: 17%;">Product Name</th>
        <th>High-Throughput</th>
    </tr>
    <tr align="center">
        <td>Positioning</td>
        <td>High throughput and large capacity, suitable for large-scale read-intensive businesses</td>
    </tr>
    <tr align="center" >
        <td>Scenario</td>
        <td>Read-intensive scenarios such as video rendering, game battle server, and non-linear editing</td>
    </tr>
    <tr align="center" >
        <td>Storage capacity</td>
        <td>0–1 PiB</td>
    </tr>
    <tr align="center" >
        <td>Bandwidth (MiB/s)</td>
        <td><nobr>0–200 GiB/s (dependent on the deployment workload)</nobr></td>
    <tr align="center" >
        <td>Read IOPS</td>
        <td><nobr>Min{2 × Capacity in GiB , 2 million}</nobr></td>
    <tr align="center" >
        <td>Write IOPS</td>
        <td>Min{1 × Capacity in GiB , 1 million}</td>
    </tr>
    <tr align="center" >
        <td>OPS upper threshold</td>
        <td>Read/Write: 300,000/20,000</td>
    <tr align="center" >
        <td>Latency</td>
        <td>4K single-stream read:5 ms</br>4K single-stream write: 10 ms</td>
    </tr>
    <tr align="center" >
        <td>Supported protocol</td>
        <td>SMB</td>
    </tr>
    <tr align="center" >
        <td>Expansion</td>
        <td>Auto</td>
    </tr>
    <tr align="center" >
        <td>Supported OS</td>
        <td>Windows</td>
    </tr>
</table>

## Notes

- In the performance-related formulas, the capacities of Standard Turbo and High-Performance Turbo refer to the capacities purchased for the cluster. For Standard and High-Performance, the capacities refer to the storage that is actually used by the instances.
- The table above shows the capabilities of the file system. To reach the performance upper threshold, you usually need to perform multi-threaded reads/writes using multiple compute nodes.
- The performance benchmark is tested in interruption-free conditions. The results of mixed tests or other loads might vary.
- OPS suggests the file system's ability to process metadata per second, which is not the same as IOPS.
- Currently, High-Throughput CFS is not available for purchase in the console. If you need to purchase it, [submit a ticket](https://console.tencentcloud.com/workorder/category) for application.



CFS introduces various file system types. The following table describes the features, advantages, and use cases of each type.

<table> 
    <tr align="center">
        <td width="" >Product Type</td>
        <td width="21%" colspan="2">Standard</td>
        <td width="21%" colspan="2">High-Performance</td>
    <tr align="center">
        <td width="" >Storage Class</td>
        <td width="21%" >Standard</td>
        <td width="21%" >Standard Turbo</td>
        <td width="21%" >High-Performance</td>
        <td width="21%">High-Performance Turbo </td>
    </tr>
    <tr align="center">
        <td>Positioning</td>
        <td>Cost-effective, suitable for most scenarios</td>
        <td>High OPS and high throughput, suitable for large and small files under high load</td>
        <td>High bandwidth, suitable for large files and high throughput scenarios</td>
        <td>High OPS and low latency, suitable for latency-sensitive businesses under high load</td>
    </tr>
    <tr align="center" >
        <td>Scenario</td>
        <td>Small-scale enterprise file sharing, web services, data backup/archive, and log storage</td>
        <td>High-performance and large-scale web services, media, image rendering, AI reference, OLAP services, and high-performance computation</td>
        <td>High-performance and large-scale web services, media, image rendering, and AI inference</td>
        <td>High-performance and large-scale computation, AI training, databases, big data analysis, and OLAP services</td>
    </tr>
    <tr align="center" >
        <td>Storage capacity</td>
        <td>0−160 TiB</td>
        <td>40 TiB−100 PiB</td>
        <td>0−10 PiB</td>
        <td>20 TiB−100 PiB</td>
    </tr>
    <tr align="center" >
        <td>Bandwidth (MiB/s)</td>
        <td>Min [100 + Storage usage in GiB x 0.1,300]</td>
        <td>Min [Storage usage in GiB x 0.1,102,400]</td>
        <td>Min [200 + Storage usage in GiB x 0.2,10,240]</td>
        <td>Min [Storage usage in GiB x 0.2,102,400]</td>
    </tr>
    <tr align="center" >
        <td>Latency</td>
        <td>4K single-stream read/write: 3 ms/7 ms</td>
        <td>4K single-stream read/write: 0.2 ms/3 ms</td>
        <td>4K single-stream read/write: 1 ms/1.5 ms</td>
        <td>4K single-stream read/write: 0.2 ms/1.5 ms</td>
    </tr>
    <tr align="center" >
        <td>OPS</td>
        <td>Read/Write: 10k+/1k+</td>
        <td>Read/Write (40T cluster): 150k/10k (linear growth)</td>
        <td>Read/Write: 10k+/1k+</td>
        <td>Read/Write (20T cluster): 150k/10k (linear growth)</td>
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

- The table above shows the capabilities of the file system. To reach the performance upper threshold, you usually need to perform multi-threaded reads/writes using multiple compute nodes.
- The High-Performance storage class is still in beta testing and thus is not available yet.

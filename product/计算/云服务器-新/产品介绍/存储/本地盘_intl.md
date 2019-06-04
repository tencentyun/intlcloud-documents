## Overview
A local disk is a storage device on the same physical server of CVM instance. It has high read/write IO and low latency.
Local disk is the local storage of the physical server that CVM instance is in. It is a storage space of the physical server. Currently, most of Tencent Cloud instance specifications support choosing local disks as system disks and data disks.

Local disks are prone to Single points of failure, so data redundancy at the application layer to ensure data availability is recommended. CVM instances that uses only local disks supports bandwidth upgrade, but not hardware (CPU, memory, and disk) upgrade.

## Use Cases
- **Distributed applications**: I/O-intensive applications such as NoSQL, MPP data warehouses, and distributed file systems have built-in distributed data redundancy capabilities. 
- **Logs of large online applications**: Such applications generate high volumes of log data which require high-performance storage but have relatively low requirement for storage reliability. 

## Lifecycle
The lifecycle of local disk is the same as that of the CVM instance. Therefore, local disks launch and terminate with CVM instances.

## Types of Local Disks
A local disk is the local storage of the physical server that CVM instance is in. There are two types of local disks: HDD and SSD.

### HDD Local Disk

<table class="typical">
    <tbody>
    <tr>
        <th>Specification</th>
        <th>Purchase Policy</th>
        <th>Performance</th>

    </tr>
    <tr>
        <td>System disk</td>
        <td>Fixed at 50 GB; unchangeable</td>
        <td rowspan="2">Peak throughput: 40-100 MB/s; IOPS: Up to 1,000</td>

    </tr>
    <tr>
        <td>Data disk</td>
        <td>HDD local disks of 10-1,600 GB (in increments of 10 GB) are supported, and the upper limit of HDD local disk size varies by hardware configuration. </td>
    </tr>
</tbody></table>

### SSD Local Disk
SSD local disk offers instance full-SSD data accessibility with low latency, high random IOPS, and high I/O throughput.
<table class="SSD">
    <tbody>
    <tr>
        <th>Specification</th>
        <th>Purchase Policy</th>
        <th>Performance</th>
    </tr>
    <tr>
        <td >System disk</td>
        <td>Fixed at 50 GB; unchangeable</td>
        <td rowspan="2">Peak throughput: 250 MB/s <br>Random write IOPS: Up to 10,000 (4 KB random write at a queue depth of 32) <br>Random read IOPS: Up to 75,000 (4 KB random read at a queue depth of 32) <br> Access delay: Below 3 ms
</td>

    </tr>
    <tr>
        <td>Data disk</td>
        <td>SSD local disks of 10-7,000 GB (in increments of 10 GB) are supported, and the upper limit of SSD local disk size varies by hardware configuration. </td>
    </tr>
</tbody></table>

##Purchase
A local disk can only be purchased together with a CVM instance. For more information on purchasing a CVM instance, see [Purchase and Launch an Instance](/doc/product/213/4855).

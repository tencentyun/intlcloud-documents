## Overview
A local disk is a storage device on the physical server where the CVM instance resides and features high read/write IO and low latency.
It is a storage space partitioned on the physical server. At present, you can choose to use local disks as system disks and data disks in most Tencent Cloud instance specifications.

As local disks are prone to single points of failure, you are recommended to perform data redundancy at the application layer to ensure data availability. A CVM instance that uses only cloud disks does not support hardware (CPU, memory, and disk) upgrade; instead, it only supports bandwidth upgrade.

##Scenarios
- **Distributed applications**: I/O-intensive applications such as NoSQL, MPP data warehouses, and distributed file systems have built-in distributed data redundancy capabilities. 
- **Logs of large online applications**: Such applications generate high volumes of log data which require high-performance storage but have relatively low requirement for storage reliability. 

## Lifecycle
The creation of a local disk is only subject to the CVM instance. Therefore, it is launched or terminated in line with the lifecycle of the CVM instance.

## Types
A local disk is a local storage space from the physical server where the CVM instance resides. HDD and SSD local disks are available options.

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
An SSD local disk provides full-SSD media data accessibility at the block level for the instance with low latency, high random IOPS, and high I/O throughput.
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

Cloud Block Storage (CBS) provides highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone and expandable disk for CVMs. CBS stores data at the data block level in a three-copy distributed mechanism to ensure data reliability. CBS is classified into five types: **Premium Cloud Disk*, **Balanced SSD**, **SSD**, **Enhanced SSD**, and **ulTra SSD**. Each type has unique performance and characteristics, and the price varies, making CBS suitable for different use cases.

## Notes
- Currently, Enhanced SSD and ulTra SSD are only available in certain availability zones. They will be supported in more availability zones.
- The performance of Enhanced SSD is only guaranteed when it's attached to S5, M5, and SA2 models created after August 1, 2020, and all later generation models.
- **ulTra SSD can only be purchased and used with the Standard Storage Optimized S5se CVM instance.**
- Enhanced SSD and ulTra SSD cannot be used as the system disk.
- Enhanced SSD and ulTra SSD cannot be encrypted.
- Enhanced SSD and ulTra SSD cannot be upgraded from other disk types.


## Overview
- **Premium Cloud Disk**
Tencent Cloud Premium Cloud Disk is a hybrid storage type. It adopts the Cache mechanism to provide a high-performance SSD-like storage, and employs a three-copy distributed mechanism to ensure data reliability. Premium Cloud Disk is suitable for small and medium applications with high requirements for data reliability and standard requirements for performance, such as Web/App servers, business logical processing, as well as small and medium sites.
- **Balanced SSD**
Balanced SSD is an entry-level all-flash block storage product. It's highly cost-effective and suitable for medium applications with high requirements for data reliability and standard requirements for performance, such as Web/App servers, business logical processing, KV services, as well as basic database services.
- **SSD**
SSD is an all-flash cloud disk using NVMe SSD as the storage media, and employs a three-copy distributed mechanism. It provides storage service with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for applications with high requirements for I/O performance.
- **Enhanced SSD**
Enhanced SSD is based on Tencent Cloud's latest storage engine, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data security up to 99.9999999%, making it suitable for I/O-intensive applications with high requirements for latency, such as large databases and NoSQL. Uniquely, the performance and capacity of Enhanced SSD cloud disks can be independently adjusted to meet your requirements.
- **ulTra SSD**
ulTra SSD is powered by Tencent Cloud's latest high-performance distributed storage engine, high-speed network infrastructure, and the latest storage hardware. It boasts long-term and stable performance with ultra low latency. It is suitable for I/O-intensive and throughput-intensive workloads that require ultra low latency, such as large databases (MySQL, HBase, Cassandra, etc.), key-value storage models (etcd, rocksdb, etc.), log search service (Elasticsearch, etc.), and real-time high-bandwidth businesses (video processing, live streaming, etc.). It performs well in key transaction workloads, core database services, large-scale OLTP services, video processing, and other scenarios. Uniquely, the performance and capacity of ulTra SSD cloud disks can be independently adjusted to meet your requirements.


## Performance metrics[](id:performance)
The table below compares the performances of the five CBS services.

<table>
<thead>
<tr>
<th>Metric</th>
<th>ulTra SSD</th>
<th>Enhanced SSD</th>
<th>SSD</th>
<th>Balanced SSD</th>
<th>Premium Cloud Disk</th>
</tr>
</thead>
<tbody><tr>
<td>Max size (GB)</td>
<td>32,000</td>
<td>32,000</td>
<td>32,000</td>
<td>32,000</td>
<td>32,000</td>
</tr>
<tr>
<td>Max IOPS</td>
<td>Up to 1,000,000 after stacking extra performance</td>
<td>Up to 1,00,000 after stacking extra performance</td>
<td>26,000</td>
<td>10,000</td>
<td>6000</td>
</tr>
<tr>
<td>Random IOPS performance</td>
<td><b>Baseline Performance</b>: Random IOPS = Min {4000 + Capacity (GiB) x 100, 50000}<br><b>Extra Performance</b>: Max IOPS = Min {Extra Performance Value x 128, 950000} <br></td>
<td><b>Baseline Performance</b>: Random IOPS = Min {1800 + Capacity (GiB) x 50, 50000}<br><b>Extra Performance</b>: Max IOPS = Min {Extra Performance Value x 128, 50000} <br>For details, see <a href="https://intl.cloud.tencent.com/document/product/362/39611">Enhanced SSD Performance</a></td>
<td>Random IOPS = Min {1800 + Capacity (GiB) x 30, 26000}</td>
<td>Random IOPS = Min {1800 + Capacity (GiB) x 15,10000}</td>
<td>Random IOPS = Min {1800 + Capacity (GiB) x 8, 6000}</td>
</tr>
<tr>
<td>Max throughput (MB/s)</td>
<td>Up to 4,000 MB/s with extra performance</td>
<td>Up to 1,000 MB/s with extra performance</td>
<td>260 MB/s</td>
<td>190 MB/s</td>
<td>150 MB/s</td>
</tr>
<tr>
<td>Throughput performance (MB/s)</td>
<td><b>Baseline Performance</b>: Throughput = Min {120 + Capacity (GiB) x 0.5, 350} <br><b>Extra Performance</b>: Throughput = Min {Extra Performance Value x 1, 3650}<br></td>
<td><b>Baseline Performance</b>: Throughput = Min {120 + Capacity (GiB) x 0.5, 350} <br><b>Extra Performance</b>: Throughput = Min {Extra Performance Value x 1, 650}<br>For details, see <a href="https://intl.cloud.tencent.com/document/product/362/39611">Enhanced SSD Performance</a></td>
<td>Throughput = Min {120 + Capacity (GiB) x 0.2, 260}</td>
<td>Throughput = Min {100 + Capacity (GiB) x 0.2, 190}</td>
<td>Throughput = Min {100 + Capacity (GiB) x 0.15, 150}</td>
</tr>
<tr>
<td>Single-path random read/write latency</td>
<td>0.1 - 0.5 ms</td>
<td>0.3 - 1 ms</td>
<td>0.5 - 3 ms</td>
<td>0.5 - 3 ms</td>
<td>0.8 - 5 ms</td>
</tr>
<tr>
<td>Note</td>
<td>ulTra SSD cloud disks can only be purchased with Standard Storage Optimized S5se instances as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/11518">Instance Types</a>.</td>
<td>
<ul style="margin:0px">
<li>The performance of Enhanced SSD is only guaranteed when it's attached to S5, M5, and SA2 models and all later generation models.</li>
<li>The max IOPS and max throughput performance of a single Enhanced SSD cloud disk are limited by the type of instance it is attached to. Currently, only when the Enhanced SSD cloud disk is attached to the latest generation instances (S6 and SA3), its maximum performance can be achieved. Note that the metric information on the achievable maximum storage performance for different instance types will be continuously updated.</li>
</ul>s
</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
</tr>
</tbody></table>


<dx-alert infotype="explain" title="">
- The main difference among cloud disks is the I/O performance.
- The max IOPS performance is tested out in 4 KiB I/O cases, and the max throughput is tested out at 256 KiB I/O cases. For specific test methods, see [Measuring cloud disk performance](https://intl.cloud.tencent.com/document/product/362/6741).
</dx-alert>



## Application Scenarios
**Enhanced SSD is more suitable for latency-sensitive or I/O-intensive scenarios**, including:
- High performance and high data reliability: Suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.
- Medium and large databases: Support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: Support NoSQL businesses such as HBase and Cassandra.
- Elasticsearch: Support low-latency ES storage.
- Video service: Suitable for applications with high requirements for storage bandwidth, such as audio/video encoding and decoding, live streaming and recording playback.
- Big data analysis: Suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.

**ulTra SSD is more suitable for latency-sensitive scenarios that require ultra low latency**, including:
- Key-value (KV) storage: Support rocksdb, etcd, etc. The KV storage service generally writes data to disk in the serial I/O mode, which requires ultra low latency. The single thread latency determines the overall system performance. ulTra SSD guarantees the latency as low as tens of microseconds, making it fit for core business systems with high requirements for data reliability and availability.
- Large databases: Support medium and large relational database applications that contain tables with millions of rows, such as MySQL, Oracle, SQL Server, and MongoDB.
- Large NoSQL: Support NoSQL businesses such as HBase and Cassandra.
- Elasticsearch: Support low-latency ES storage.
- Video service: Suitable for applications with high requirements for storage bandwidth, such as audio/video encoding and decoding, live streaming and recording playback.
- Core business systems: Suitable for I/O-intensive applications and other core business systems with high requirements for data reliability.
- Big data analysis: Suitable for data analysis, data mining, business intelligence, and other fields. Provide distributed processing capabilities for data at TB and PB levels.
- High performance and high data reliability: Suitable for high-load, mission-critical business systems. SSD provides three-copy data redundancy and is equipped with comprehensive capabilities for data backup, snapshots, and data restoration within seconds.

**SSD is applicable for applications with high and medium loads**, including:
- Medium databases: Medium and large relational database applications, such as MySQL.
- Image processing: Support data analysis and storage businesses, such as image processing.

**Balanced SSD is mainly used in the following data scenarios**:
Medium applications with high requirements for data reliability and standard requirements for performance, such as Web/App servers, business logical processing, KV services, as well as basic database services.

**Premium Cloud Disk is mainly suitable for the following data scenarios**:
- Small and medium databases and Web/App servers. Provide long-term and stable I/O performance.
- Scenarios that require balanced storage capacity and performance, such as enterprise office services.
- Core business testing and the front and back end debugging.

## Billing Description
For pricing details of cloud disks, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

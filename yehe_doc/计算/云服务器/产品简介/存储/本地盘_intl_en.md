## Local Disk Overview
A local disk resides on the same physical server as the CVM instance. A local disk has low read/write latency and high IO performance.
Local disks are a part of the local storage devices attached to the same physical server as the CVM instance they are attached to. Therefore, the reliability of the datastore on local disks depends on the reliability of the physical server, which puts the data at risk of a single point of failure.

> 
> - If the physical server that hosts your CVM instance experiences hardware faults, you are at risk of losing valuable data. To avoid this, you should ensure data reliability with redundancy applications. If you cannot plan for data redundancy, consider using [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) to improve data reliability.
> - You cannot upgrade the hardware (CPU, memory, storage) of a CVM instance with local disks. You can only upgrade its bandwidth.
> 

## Use Cases
- **Distributed application**: NoSQL, MPP data warehouses, distributed file systems, and other I/O intensive applications. These applications have their own distributed data redundancy. 
- **Logs for large online applications**: large online applications produce a large amount of log data, which requires high-performance storage but lower requirements for storage reliability. 

## Lifecycle
The lifecycles of local disks are the same as the lifecycle of the CVM instance to which they are attached. In other words, local disks start when the CVM instance starts and ends when the CVM instance shuts down.

## Type
Local disks are local storage devices attached to the same physical server as the CVM instance. There are two types of local disks, HDD local disks, and SSD local disks.

### HDD local disks

<table class="typical">
	<tbody>
	<tr>
		<th>Specification</th>
		<th>Remarks</th>
		<th>Performance metrics</th>
	</tr>
	<tr>
		<td>HDD local system disk</td>
		<td>50 GB per disk.</td>
		<td rowspan="2">Peak I/O throughput 40 MB/s - 100+ MB/s. IOPS ranges from hundreds to 1000.</td>
	</tr>
	<tr>
		<td>HDD local data disk</td>
		<td>From 10 GB to 1600 GB (in 10 GB increments). Different CVM specifications have different maximum HDD local disk capacities.</td>
	</tr>
</tbody></table>

### Local SSDs
Local SSDs are local storage on the physical machine where the CVM resides. They provide instances with full SSD block-level data access capability and low latency, high random IOPS, and high I/O throughput.
<table class="SSD">
	<tbody>
	<tr>
		<th>Specification</th>
		<th>Remarks</th>
		<th>Performance metrics</th>
	</tr>
	<tr>
		<td >SSD local system disk</td>
		<td>50 GB per disk.</td>
		<td rowspan="2">Peak I/O throughout 250 MB/s<br>Maximum random write IOPS 10000 (4K random write. QD = 32)<br>Access latency less than 3ms
</td>
	</tr>
	<tr>
		<td>SSD local data disk</td>
		<td>10 GB to 7000 GB (in 10 GB increments). Different CVM specifications have different maximum HDD local disk capacities.</td>
	</tr>
</tbody></table>

## Purchase
Local disks can only be purchased along with your CVM instances. For more information, refer to [Creating Instances](https://intl.cloud.tencent.com/document/product/213/4855).


Tencent Cloud provides a wide range of flexible and cost-effective data storage devices for CVM instances. The performance and price varies by the type of storage device, which is suitable for different scenarios.

## Storage Devices
Storage devices can be divided into the following categories by dimensions:
<table>
        <tbody>
		<tr>
            <th style="width: 5%;">Dimension</th>
            <th style="width:18%">Category</th>
            <th style="width: 100px;">Description</th>
        </tr>
        <tr>
            <td rowspan="3">Storage Medium</td>
            <td>HDD disk</td>
            <td>Uses hard disk drive as the storage medium. It features lower price and better read/write speed.</td>
        </tr>
				<tr>
				    <td>SSD disk</td>
					<td>Uses solid state drive as the storage medium. It features high-performing IOPS and read/write speed, with an IOPS and throughput up to 20 times and 16 times higher than those of HDD disk. It is more expensive than HDD disk.</td>
			    <tr>
            		<td rowspan="2">Application Scenarios</td>
            		<td>System disk</td>
            		<td>Used to store the collection of systems that control and schedule the operation of CVM. It uses images.</td>
        </tr>
				<tr>
				    <td>Data disk</td>
						<td>Used to store all the user data.</td>
						<tr>
						<td rowspan="3">Architecture</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/362">Cloud block storage</a></td>
            <td>Cloud block storage is an elastic, highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone scalable hard disk for CVM. It provides data storage at data block level and employs a 3-copy distributed mechanism to ensure data reliability.<br><font style="font-weight:bold">For CVM with cloud block storage, its hardware, disk and network can be adjusted.</font><br>
						</td>
        </tr>
				<tr>
				<td><a href="https://intl.cloud.tencent.com/document/product/213/5798">Local disk</a></td>
						<td>It is a local storage reserved on the physical machine where the CVM resides. It allows data access with low latency, but may have a single point of failure.<br>
						<font style="font-weight:bold">CVM with local disk does not support hardware upgrades (CPU, memory and disk), but bandwidth can be upgraded.</font>
						</td>
				<tr>
				<td><a href="https://intl.cloud.tencent.com/document/product/213/4961">COS</a></td>
						<td>COS is a data storage device on the Internet. It allows data retrieval from any location on CVM instance or the Internet, reducing the storage cost. It is not suitable to be used as a storage medium for low-latency and high-IO scenarios.
						</td>
				</tbody>
				</table>

## Block storage device mapping

Each instance has a system disk to ensure data operations, and more data disks can be mounted to an instance. An instance uses block storage device-mapping to map the storage devices to locations it can identify.
Block storage puts data into blocks in bytes and allows random access. Tencent Cloud supports two types of block storage devices: local disk and cloud disk.
![](https://mc.qcloudimg.com/static/img/7e8715ce6bba831c61d0cc807bec8ce9/device-mapping.png)
This figure shows how CBS maps the block storage device to the CVM: it maps `/dev/vda' to the system disk, and the two data disks to '/dev/vdb and /dev/vdc' respectively.
The CVM instance can automatically create block storage device mapping for local disks and cloud disks mounted to it.


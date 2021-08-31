Tencent Cloud provides a wide range of flexible and cost-effective data storage devices for CVM instances. The performance and price varies by the type of storage device, which is suitable for different scenarios.


## Storage Devices
Storage devices can be divided into the following categories by dimension:
<table>
        <tbody>
		<tr>
            <th style="width: 5%;">Dimension</th>
            <th style="width: 5%;" >Category</th>
            <th style="width: 20%;" >Description</th>
        </tr>
        <tr>
            <td rowspan="2">Storage Medium</td>
            <td>HDD disk</td>
            <td>Uses hard disk drive (HHD) as the storage medium. It features a low price and fast read/write speeds.</td>
        </tr>
				<tr>
				    <td>SSD disk</td>
					<td>Uses solid state drive (SSD) as the storage medium. It features excellent IOPS and read/write speeds, with an IOPS and throughput of up to 20 times and 16 times higher than those of the HDD disk. It is more expensive than the HDD disk.</td>
			    <tr>
            		<td rowspan="2">Use Cases</td>
            		<td>System disk</td>
            		<td>Used to store the collection of systems that control and schedule the operation of CVM. It uses images.</td>
        </tr>
				<tr>
				    <td>Data disk</td>
						<td>Used to store all user data.</td>
						<tr>
						<td rowspan="2">Architecture</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
            <td>Cloud Block Storage (CBS) is an elastic, highly available, highly reliable, low-cost, and customizable network block device that can be used as a standalone scalable disk for CVM. It provides data storage at a data block level and employs a 3-copy distributed mechanism to ensure data reliability.<br><font style="font-weight:bold">You can adjust the hardware, disk, and network of a CVM with CBS.</font><br>
						</td>
        </tr>
				<td><a href="https://intl.cloud.tencent.com/document/product/213/4961">Cloud Object Storage</a></td>
						<td>Cloud Object Storage (COS) is a data storage device on the Internet. It allows data retrieval from any location on the CVM instance or the Internet, reducing storage costs. It is unsuitable for low-latency and high-IO scenarios.
						</td>
				</tbody>
				</table>

## Block storage device mapping

Each instance has a system disk to ensure basic data operations, and may mount more data disks. An instance uses block storage device-mapping to map the storage devices to locations it can identify.
CBS puts data into blocks in bytes and allows random access. Tencent Cloud supports two types of CBS devices: local disk and cloud disk.
![](https://main.qcloudimg.com/raw/3815bb250f6178d67b8fe2be11a50bf8.svg)
This figure shows how CBS maps the block storage device to the CVM: it maps `/dev/vda` to the system disk and maps the two data disks to `/dev/vdb` and `/dev/vdc`, respectively.
The CVM instance can automatically create block storage device mapping for local disks and cloud disks mounted to itself.


## Metrics
The block storage devices provided by Tencent Cloud have different performances and prices according to their types. For more details, see [Cloud disk types](https://intl.cloud.tencent.com/document/product/362/31636). Because different applications have different workloads, if you do not provide enough I/O requests to fully utilize the cloud disk, full performance of the cloud disk may not be reached.
The following metrics are generally used to measure the performance of the cloud disk:
- IOPS: Read/write count per second. IOPS is determined by the underlying drive type of the storage device.
- Throughput: Read/written data volume per second, unit in MB/s.
- Latency: Time elapsed from sending an I/O operation to receiving an acknowledgement (in seconds).

## Test Example
FIO is a tool for testing disk performance. It is used to perform stress test and verification on hardware. We recommend you use libaio’s I/O engine to perform the test. Please install FIO and libaio.
>
- To avoid damaging important files in the system, do not perform FIO test on the system disk.
- We recommend that you perform FIO test on empty disks that do not store important data, and re-create the file system after completing the test. To avoid data corruption caused by corruption of the metadata of the underlying file system, please do not perform the test on the business data disk.
- Testing object recommendations:
 - When testing disk performance, we recommend you directly test raw disks (such as /dev/vdb). Please ensure that there is no data on the data disk, otherwise the original data will be destroyed.
 - When testing file system performance, we recommend you specify the specific file test (such as /data/file).
- You must ensure the /etc/fstab file configuration items do not contain the mounting configuration of the disk to be tested, otherwise CVM may fail to launch.

The testing formulas of different scenarios are basically the same. The `rw`, `iodepth`, and `bs` (block size) parameters are the only difference. The optimal `iodepth` for each workload is different, which depends specifically on the sensitivity of your applications to IOPS and latency.

Parameter description:

<table>
     <tr>
         <th nowrap="nowrap">Parameter name</th>   
		 <th>Description</th>
         <th nowrap="nowrap">Sample value</th> 
     </tr>
	 <tr>
         <td>bs</td>
		 <td>Block size per request. Values include 4k, 8k, 16k, and so on.</td>
         <td>4k</td>
     </tr>
	 <tr>
         <td>ioengine</td>
		 <td>I/O engine. We recommend you use Linux’s async I/O engine.</td>
         <td>libaio</td>
     </tr>
	 <tr>
         <td>iodepth</td>
		 <td>Queue depth of I/O requests.</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>direct</td>
		 <td>Specify direct mode.<li>True (1) indicates the O_DIRECT identifier is specified, ignoring the I/O cache, and writing data directly.</li><li>False (0) indicates the O_DIRECT identifier is not specified.</li> The default is True (1).</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>rw</td>
		 <td>Read and write mode. Values include sequential read (read), sequential write (write), random read (randread), random write (randwrite), hybrid random read and write (randrw), and hybrid sequential read and write (rw, readwrite).</td>
         <td>read</td>
     </tr>
	 <tr>
         <td>time_based</td>
		 <td>Specify the time mode used. As long as FIO runs based on the time, there is no need to set this parameter value.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>runtime</td>
		 <td>Specify the test duration, which is the FIO runtime.</td>
         <td>600</td>
     </tr>
	 <tr>
         <td>refill_buffers</td>
		 <td>FIO will refill the I/O buffer at every submission. The default setting is to fill and reuse the data only at the start.</td>
         <td>N/A</td>
     </tr>
         <td>norandommap</td>
		 <td>When performing random I/O, FIO overwrites every block of the file. If this parameter is given, new offset will be selected without viewing the I/O history.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>randrepeat</td>
		 <td>Whether the random sequence is repeatable. True (1) indicates the random sequence is repeatable, False (0) indicates the random sequence is not repeatable. The default is True (1).</td>
         <td>0</td>
     </tr>
         <td>group_reporting</td>
		 <td>When multiple jobs are concurrent, statistics for the entire group are printed.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>name</td>
		 <td>Name of the job.</td>
         <td>fio-read</td>
     </tr>
         <td>size</td>
		 <td>Address space of the I/O test.</td>
         <td>100GB</td>
     </tr>
	 <tr>
         <td>filename</td>
		 <td>Test object, which is the name of the disk to be tested.</td>
         <td>/dev/sdb</td>
     </tr>
</table>

Common use cases are as follows:
- **bs=4k iodepth=1**: Random read/write test, can reflect the latency performance of the hard disk.
Execute the following command to test the random read latency of the disk.
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-lat --size=10G -filename=/dev/vdb
```
Execute the following command to test the random write latency of the disk.
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-lat --size=10G -filename=/dev/vdb
```
Test random hybrid read-write latency performance of the SSD. This is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/57383658ddbfaf95ed1f9adb925e1bbf.png)

- **bs=128k iodepth = 32**: Sequential read/write test, can reflect the throughput performance of the disk.

Execute the following command to test the sequential read throughput bandwidth.
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=read -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-read-throughput --size=10G -filename=/dev/vdb
```

Execute the following command to test the sequential write throughput bandwidth.
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=write -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-write-throughput --size=10G -filename=/dev/vdb
```
Test the sequential read throughput performance of the SSD cloud disk. This is shown in the following figure:
 ![](https://main.qcloudimg.com/raw/b3985fa277ad837b7314e568541e62b1.png)
 - **bs=4k iodepth=32**: Random read/write test, can reflect the IOPS performance of the hard disk.
Execute the following command to test the random read IOPS of the disk.
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-iops --size=10G -filename=/dev/vdb
```
Execute the following command to test the random write IOPS of the disk.
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-iops --size=10G -filename=/dev/vdb
```
Test the random read IOPS performance of the SSD cloud disk. This is shown in the following figure:
  ![](//mccdn.qcloud.com/static/img/9a9621f1eaec3f630fbad75f8d3820ee/image.png)

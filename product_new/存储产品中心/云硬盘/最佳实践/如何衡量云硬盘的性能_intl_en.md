## Metrics
Tencent Cloud CBS devices have different performances and prices according to their types. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636). Because different applications have different workloads, if the number of I/O requests are low, the cloud disk may not play its full performance.
The following metrics are generally used to measure the performance of a cloud disk:
- IOPS: read/write count per second. IOPS is determined by the underlying drive type of the storage device.
- Throughput: read/written data volume per second, in MB/s.
- Latency: Time that has elapsed from sending an I/O operation to receiving an acknowledgement, in seconds.

## Testing Tool
FIO is a tool for testing disk performance. It is used to perform stress test and verification on hardware. This document uses FIO as an example.
We recommend that you use libaio’s I/O engine to perform the test. Please install FIO and libaio.
>
- **To avoid damaging important files in the system, do not perform FIO testing on the system disk.**
- **To avoid data corruption caused by corruption of the metadata of the underlying file system, do not perform the test on the business data disk.**
- Ensure the `/etc/fstab` file configuration items **do not contain** the mounting configuration of the disk to be tested. Otherwise, CVM may fail to launch.

## Recommended test objects
- We recommend that you perform FIO test on empty disks that do not store important data, and re-create the file system after completing the test..
- When testing disk performance, we recommend that you directly test raw data disks (such as /dev/vdb).
- When testing file system performance, we recommend that you specify the specific file (such as /data/file) for testing.


## Test Example
The testing formulas for different scenarios are basically the same, only the `rw`, `iodepth`, and `bs` (block size) parameters differ. For example, the optimal `iodepth` for each workload is different as it depends on the sensitivity of your application to the IOPS and latency.

Parameter description:

<table>
     <tr>
         <th nowrap="nowrap">Parameter</th>   
		 <th>Description</th>
         <th nowrap="nowrap">Sample value</th> 
     </tr>
	 <tr>
         <td>bs</td>
		 <td>Block size per request. Valid values include 4k, 8k, and 16k.</td>
         <td>4k</td>
     </tr>
	 <tr>
         <td>ioengine</td>
		 <td>I/O engine. We recommend that you use Linux’s async I/O engine.</td>
         <td>libaio</td>
     </tr>
	 <tr>
         <td>iodepth</td>
		 <td>Queue depth of an I/O request.</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>direct</td>
		 <td>Specifies direct mode.<li>True (1) indicates that the O_DIRECT identifier is specified, the I/O cache will be ignored, and data will be written directly.</li><li>False (0) indicates that the O_DIRECT identifier is not specified.</li> The default is True (1).</td>
         <td>1</td>
     </tr>
	 <tr>
         <td>rw</td>
		 <td>Read and write mode. Valid values include read, write, randread, randwrite, randrw, and rw, readwrite.</td>
         <td>read</td>
     </tr>
	 <tr>
         <td>time_based</td>
		 <td>Specifies that the time mode is used. As long as FIO runs based on the time, it is unnecessary to set this parameter.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>runtime</td>
		 <td>Specifies the test duration, which is the FIO runtime.</td>
         <td>600</td>
     </tr>
	 <tr>
         <td>refill_buffers</td>
		 <td>FIO will refill the I/O buffer at every submission. The default setting is to fill the I/O buffer only at the start and reuse the data.</td>
         <td>N/A</td>
     </tr>
         <td>norandommap</td>
		 <td>When performing random I/O operations, FIO overwrites every block of the file. If this parameter is set, a new offset will be selected without viewing the I/O history.</td>
         <td>N/A</td>
     </tr>
	 <tr>
         <td>randrepeat</td>
		 <td>Specifies whether the random sequence is repeatable. True (1) indicates that the random sequence is repeatable. False (0) indicates that the random sequence is not repeatable. The default value is True (1).</td>
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
         <td>100 GB</td>
     </tr>
	 <tr>
         <td>filename</td>
		 <td>Test object, which is the name of the disk to be tested.</td>
         <td>/dev/sdb</td>
     </tr>
</table>

Common use cases are as follows:
- **bs=4k iodepth=1**: random read/write test, which can reflect the latency performance of a disk.
Run the following command to test the random read latency of the disk:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-lat --size=10G -filename=/dev/vdb
```
Run the following command to test the random write latency of the disk:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-lat --size=10G -filename=/dev/vdb
```
Run the following command to test the random hybrid read and write latency performance of an SSD cloud disk:
```
fio --bs=4k --ioengine=libaio --iodpth=1 --direct=1 --rw=randrw --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting -rw --size=1G --filename=/dev/vdb 
```
The following figure shows the command output.
![](https://main.qcloudimg.com/raw/39ffdf41ca9bd28808792b35482fafd0.png)

- **bs=128k iodepth = 32**: sequential read/write test, which can reflect the throughput performance of a disk.
Run the following command to test the sequential read throughput bandwidth:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=read -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-read-throughput --size=10G -filename=/dev/vdb
```
Run the following command to test the sequential write throughput bandwidth:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=write -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-write-throughput --size=10G -filename=/dev/vdb
```
Run the following command to test the sequential read throughput performance of an SSD cloud disk:
```
fio --bs=128k --ioengine=libaio --iodpth=32 --direct=1 --rw=read --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting -rw --size=1G --filname=/dev/vdb
```
The following figure shows the command output.
![](https://main.qcloudimg.com/raw/f21de73d7c20d32396d43b11dd756c26.png)
 
- **bs=4k iodepth=32**: random read/write test, which can reflect the IOPS performance of a disk.
Run the following command to test the random read IOPS of the disk:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-iops --size=10G -filename=/dev/vdb
```
Run the following command to test the random write IOPS of the disk:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-iops --size=10G -filename=/dev/vdb
```
Test the random read IOPS performance of an SSD cloud disk. The following figure shows the command output.
![](https://main.qcloudimg.com/raw/b6aaf207adffdb85ba7da487b4fd2ce9.png)

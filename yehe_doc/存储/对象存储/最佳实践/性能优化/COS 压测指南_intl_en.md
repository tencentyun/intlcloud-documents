## COSBench Overview

COSBench is an open-source stress test tool developed by Intel for testing the performance of cloud object storage systems. As a cloud storage system compatible with S3 protocol, COSBench can be used to perform benchmark tests on the read/write performance of Tencent Cloud COS.


## System Environment

We recommend you run COSBench on CentOS 7.0 or later. If you run it on Ubuntu, unexpected issues may occur.


## Performance Factors

- **CPU cores**: A small number of CPU cores coupled with a large number of running workers is very likely to cause high overheads for context switching. Therefore, 32 or 64 cores are recommended for the test.
- **NIC**: The outbound traffic from the server is limited by the NIC. To test the traffic for large files, an NIC above 10 GbE is recommended.
- **Request network linkage**: Public network linkages vary in quality. Charges will incur for public network downstream traffic for downloads over the public network. Therefore, private network is recommended for access within the same region.
- **Test duration**: In order to get a reliable value, a longer test period is recommended.
- **Test environment**: The version of the JDK running on your program is also a key performance factor. For example, when testing on HTTPS, with an earlier JDK version, [GCM bugs](https://bugs.openjdk.java.net/browse/JDK-8201633) may occur for the encryption algorithm, as well as the locking issues for the random number generator.


## Directions

1. Download COSBench 0.4.2.c4.zip from [GitHub](https://github.com/intel-cloud/cosbench/releases) and decompress it on your server.
2. Install the COSBench dependency library and run the following command.
 - For CentOS, run the following command to install the dependencies:
```
sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
 - For Ubuntu, run the following command to install the dependencies:
```
sudo apt install nmap openjdk-8-jdk 
```
3. Edit the `s3-config-sample.xml` file and configure a test job. The test job is divided into the following five stages.
   1. init: Creates a bucket.
   2. prepare: Uses worker threads to PUT (upload) objects in specified size for read in the main stage.
   3. main: Uses worker threads to read and write objects for a specified period of time.
   4. cleanup: Deletes the created objects.
   5. dispose: Deletes the bucket.

 The sample configuration is as shown below:
```shell
<?xml version="1.0" encoding="UTF-8" ?>
<workload name="s3-50M-sample" description="sample benchmark for s3">

  <storage type="s3" config="accesskey=AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997xxxxxx;secretkey=YaWIuQmCSZ5ZMniUM6hiaLxHnxxxxxx;endpoint=http://cos.ap-beijing.myqcloud.com" />

  <workflow>

    <workstage name="init">
      <work type="init" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

    <workstage name="prepare">
      <work type="prepare" workers="100" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,1000);sizes=c(50)MB" />
    </workstage>

    <workstage name="main">
      <work name="main" workers="100" runtime="300">
        <operation type="read" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1,1000)" />
        <operation type="write" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1000,2000);sizes=c(50)MB" />
      </work>
    </workstage>

    <workstage name="cleanup">
      <work type="cleanup" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,2000)" />
    </workstage>

    <workstage name="dispose">
      <work type="dispose" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

  </workflow>

</workload>
```
**Parameter description**
<table>
<thead>
<tr><th>Parameter</th><th>Description</th></tr>
</thead>
<tbody>
<tr>
<td>accesskey, secretkey</td>
<td>Key information. Replace them with your own `SecretId` and `SecretKey`.</td>
</tr>
<tr>
<td>cprefix</td>
<td>Bucket name prefix, such as `examplebucket`.</td>
</tr>
<tr>
<td>containers</td>
<td>Value range for bucket names. A bucket name is made up of `cprefix` and `containers`, such as `examplebucket1` or `examplebucket2`. </td>
</tr>
<tr>
<td>csuffix</td>
<td>Your `APPID`. Note that `APPID` is prefixed with a <code>-</code>, such as `-1250000000`.</td>
</tr>
<tr>
<td>runtime</td>
<td>Duration of the stress test</td>
</tr>
<tr>
<td>ratio</td>
<td>Ratio of reads to writes</td>
</tr>
<tr>
<td>workers</td>
<td>Number of stress test threads</td>
</tr>
</tbody>
</table>
4. Edit the `cosbench-start.sh` file and add the following parameter to the Java startup command line to disable S3 MD5 verification.
```plaintext
-Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true
```
5. Start the COSBench service.
 - For CentOS, run the following command:
```plaintext
sudo bash start-all.sh
```
 - For Ubuntu, run the following command:
```plaintext
sudo bash start-driver.sh &
sudo bash start-controller.sh &
```
6. Run the following command to submit the job.
```plaintext
sudo bash cli.sh submit conf/s3-config-sample.xml
```
Check the test status at `http://ip:19088/controller/index.html` (replace the IP in this link with the IP of your own testing server).
![](https://main.qcloudimg.com/raw/77f1631fa15141332d123fb472bab7ac.png)
You can see the five stages as shown below:
![](https://main.qcloudimg.com/raw/3ccb5a60253ceb20c6da9292582c4355.png)
7. The following example shows the performance tests of uploads and downloads in a Tencent Cloud CVM instance with 32 cores and 17 Gbps private network bandwidth in Beijing region. The test includes the following two stages.
    1. prepare: 100 workers threads are run to upload 1,000 objects (50 MB each).
    2. main: 100 workers are run to read and write objects in parallel for 300 seconds.

 The test results after the above two stages are as shown below.
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)
8. Run the following command to stop the test.
```plaintext
sudo bash stop-all.sh
```

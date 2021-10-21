## COSBench Overview

COSBench is an open-source benchmark tool developed by Intel for testing the performance of cloud object storage systems. As a cloud storage system compatible with S3 protocol, COSBench can be used to perform benchmark tests on the read/write performance of Tencent Cloud COS.


## System Environment

It is recommended that you run COSBench in CentOS 7.0 or a later version. If you run it in Ubuntu, unexpected issues may occur.


## Performance Factors

- **CPU cores**: a small number of CPU cores coupled with a large number of running workers is very likely to cause high overheads for context switching. Therefore, 32 or 64 cores are recommended for the test.
- **NIC**: the outbound traffic from the server is limited. To test the traffic for large files, an NIC above 10 GB is recommended.
- **Network link**: public network links vary in quality. Charges will incur for public network downstream traffic for downloads over public network. Therefore, private network is recommended for access within the same region. 
- **Test duration**: in order to get a reliable value, we recommend a longer test period.
- **Test environment**: the version of the JDK running on your program is also a key performance factor. For example, when testing on HTTPS, with an earlier JDK version, [GCM bugs](https://bugs.openjdk.java.net/browse/JDK-8201633) may occur for the encryption algorithm, as well as the locking issues for the random number generator.




## Directions

1. Download COSBench 0.4.2.c4.zip at [COSBench GitHub](https://github.com/intel-cloud/cosbench/releases) and decompress it in your server.
2. Install the COSBench dependent library and run the following command.
 - For CentOS, run the following command to install the dependencies:
```
sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
 - For Ubuntu, run the following command to install the dependencies:
```
sudo apt install nmap openjdk-8-jdk 
```
3. Edit the file `s3-config-sample.xml` and configure a test job. The test job is divided into the following five stages.
   1. init: creates a bucket.
   2. prepare: uses parallel threads (or workers) to PUT (upload) objects with specified size to read in the main stage.
   3. main: uses parallel workers to read and write objects for a specified period of time.
   4. cleanup: deletes the created objects.
   5. dispose: deletes buckets.

The sample configuration is as shown below.

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

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
|    accesskey, secretkey    | Access key information, which you should replace with your own SecretId and SecretKey  |
|      cprefix         | Prefix of the bucket name, such as examplebucket            |
|  containers |  Value range for bucket names. A bucket name is made up of `cprefix` and `containers`, such as `examplebucket1` or `examplebucket2`.   |
|    csuffix          | User account APPID, which should be prefixed with the endash `-`, e.g. -1250000000      |
| runtime              |  COSBench running time                     |
| ratio                | Read/Write ratio                    |
| workers              | Number of workers                       |

4. Edit the file `cosbench-start.sh` and add the following parameter to the Java startup command line to disable S3 MD5 verification.
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
Check the test status at `http://ip:19088/controller/index.html` (replace “ip” in this link with the IP of your own testing server).
![](https://main.qcloudimg.com/raw/77f1631fa15141332d123fb472bab7ac.png)
You can see the five work stages as shown below.
![](https://main.qcloudimg.com/raw/3ccb5a60253ceb20c6da9292582c4355.png)
7. The following example shows the performance tests of the uploads and downloads of Tencent Cloud CVM with 32 cores and 17 Gbps private network bandwidth in Beijing region. The test includes the following two stages.
    1. prepare: 100 workers threads. 1,000 50 MB.objects are uploaded.
    2. main: 100 workers read and write objects in parallel for 300 seconds.

The test results after two stages above are as shown below.
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)

8. Run the following command to stop the test.
```plaintext
sudo bash stop-all.sh
```

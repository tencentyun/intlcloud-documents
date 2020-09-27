## COSBench

COSBench is an open-source benchmark tool developed by Intel to test cloud object storage systems. It can be used to perform benchmark tests on the read/write performance of COS as a cloud object storage system compatible with S3 protocol.


## System Environment

CentOS 7.0 or above.


## Performance Factors

- **CPU cores**: a small number of CPU cores, coupled with a large number of running workers, are likely to cause high overheads for context switching. Therefore, it is recommended to use 32 or 64 cores for the test.
- **NIC**: limits the outbound traffic from the server. To test the traffic for large files, it is recommended to use an NIC above 10 GB.
- **Network link**: public network links vary in quality, and charges will occur for public network downstream traffic in case of downloads over public network. Therefore, it is recommended to request access in the same region over private network.
- **Test duration**: it is recommended not to take a test too short for stable values.
- **Test environment**: the JDK version your program is running on is also a key performance factor. For example, with a low JDK version, the test on HTTPS may present [GCM bugs](https://bugs.openjdk.java.net/browse/JDK-8201633) for the encryption algorithm, as well as locking issues for the random number generator.




## Directions

1. Download the COSBench 0.4.2.c4 release from [GitHub](https://github.com/intel-cloud/cosbench/releases), and decompress it in your server.
2. Install the COSBench dependent library by running this command:
```
yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
3. Edit the file `s3-config-sample.xml` by configuring a test job which is divided into the following five stages:
 1. init: creates a bucket.
 1. prepare: uses parallel threads (or workers) to PUT (upload) objects of specified size to read in the next stage.
 1. main: parallel workers read and write for a specified period of time.
 1. cleanup: deletes created objects.
 1. dispose: deletes buckets.

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

**Parameters**

| Parameter | Description |
|-----------|----------------|
|    accesskey, secretkey    | Access key, which you should replace with your own SecretId and SecretKey  |
|      cprefix         | Name of the bucket, e.g. examplebucket            |
|    csuffix          | User account APPID, which should be prefixed with the symbol `-`, e.g. -1250000000      |
|     runtime        | Specifies how long the test should run     |
|     ratio       | The ratio of reads to writes          |
|   workers          |  Specifies the number of parallel threads for the test       |

4. Edit the file `cosbench-start.sh` by adding the following parameter to the Java launching line to disable S3 MD5 verification:
```plaintext
-Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true
```
5. Submit the job by running:
```plaintext
sh cli.sh submit conf/s3-config-sample.xml
```
Besides, check the test status at `http://ip:19088/controller/index.html` (replace “ip” in this link with the IP of your own testing server).
![](https://main.qcloudimg.com/raw/77f1631fa15141332d123fb472bab7ac.png)
Now you can see the five work stages as shown below:
![](https://main.qcloudimg.com/raw/3ccb5a60253ceb20c6da9292582c4355.png)
6. The following example tests the uploads and downloads to Tencent Cloud CVM with 32 cores and 17 Gbps private network bandwidth in Beijing region with the following two stages:
 1. prepare: 100 workers upload 1,000 objects of 50 MB.
 2. main: 100 workers read and write objects in parallel for 300 seconds.
The test results after the two stages above are as shown below:
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)

7. Stop the test by running:
```plaintext
sh stop-all.sh
```



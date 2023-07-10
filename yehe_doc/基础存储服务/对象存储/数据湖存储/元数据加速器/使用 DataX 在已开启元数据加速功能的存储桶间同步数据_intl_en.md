## Overview

DataX is an open-source offline data sync tool. It can efficiently sync data between various heterogeneous data sources, including MySQL, SQL Server, Oracle, PostgreSQL, HDFS, Hive, HBase, OTS, and ODPS.

COS buckets with metadata acceleration enabled can act as the HDFS service in the Hadoop system to provide Hadoop Compatible File System (HCFS) semantics-based access for your business.

This document describes how to use DataX to sync data between two buckets with metadata acceleration enabled.

## Environmental Dependencies

- [HADOOP-COS](https://github.com/tencentyun/hadoop-cos/releases) and the corresponding [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases).
- DataX version: [DataX 3.0](https://github.com/alibaba/DataX).

## Download and Installation

#### Downloading hadoop-cos

- Download [hadoop-cos](https://github.com/tencentyun/hadoop-cos/releases) and [cos_api-bundle](https://github.com/tencentyun/hadoop-cos/releases) of the corresponding version from GitHub.
- Download [chdfs-hadoop-plugin](https://github.com/tencentyun/chdfs-hadoop-plugin) from GitHub.

#### Downloading DataX package

Download [DataX](https://github.com/alibaba/DataX) from GitHub.

#### Installing hadoop-cos

After downloading hadoop-cos, copy `hadoop-cos-2.x.x-${version}.jar`, `cos_api-bundle-${version}.jar`, and `chdfs_hadoop_plugin_network-${version}.jar` to `plugin/reader/hdfsreader/libs/` and `plugin/writer/hdfswriter/libs/` in the extracted DataX path.

## How to Use

### Bucket configuration

Enter the bucket with metadata acceleration enabled, and configure the VPC where the DataX server runs in **HDFS Permission Configuration**.
>? The source and destination buckets should at least allow read and write requests in the VPC respectively.



### DataX configuration

#### 1. Modify the `datax.py` script

Open the `bin/datax.py` script in the DataX decompression directory, and modify the CLASS_PATH variable in the script as follows:

```plaintext
CLASS_PATH = ("%s/lib/*:%s/plugin/reader/hdfsreader/libs/*:%s/plugin/writer/hdfswriter/libs/*:.") % (DATAX_HOME, DATAX_HOME, DATAX_HOME)
```

#### 2. Configure `hdfsreader` and `hdfswriter` in the configuration JSON file

A sample JSON file is as shown below:
```json
{
  "job": {
  "setting": {
    "speed": {
      "byte": 10485760
    },
    "errorLimit": {
      "record": 0,
      "percentage": 0.02
    }
  },
  "content": [{
    "reader": {
      "name": "hdfsreader",
      "parameter": {
        "path": "/test/",
        "defaultFS": "cosn://examplebucket1-1250000000/",
        "column": ["*"],
        "fileType": "text",
        "encoding": "UTF-8",
        "hadoopConfig": {
          "fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
          "fs.cosn.trsf.fs.ofs.bucket.region": "ap-guangzhou",
          "fs.cosn.bucket.region": "ap-guangzhou",
          "fs.cosn.tmp.dir": "/tmp/hadoop_cos",
          "fs.cosn.trsf.fs.ofs.tmp.cache.dir": "/tmp/",
          "fs.cosn.userinfo.secretId": "COS_SECRETID",
          "fs.cosn.userinfo.secretKey": "COS_SECRETKEY",
          "fs.cosn.trsf.fs.ofs.user.appid": "1250000000"
        },
        "fieldDelimiter": ","
      }
    },
    "writer": {
      "name": "hdfswriter",
      "parameter": {
        "path": "/",
        "fileName": "hive.test",
        "defaultFS": "cosn://examplebucket2-1250000000/",
        "column": [
          {"name":"col1","type":"int"},
          {"name":"col2","type":"string"}
        ],
        "fileType": "text",
        "encoding": "UTF-8",
        "hadoopConfig": {
          "fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
          "fs.cosn.trsf.fs.ofs.bucket.region": "ap-guangzhou",
          "fs.cosn.bucket.region": "ap-guangzhou",
          "fs.cosn.tmp.dir": "/tmp/hadoop_cos",
          "fs.cosn.trsf.fs.ofs.tmp.cache.dir": "/tmp/",
          "fs.cosn.userinfo.secretId": "COS_SECRETID",
          "fs.cosn.userinfo.secretKey": "COS_SECRETKEY",
          "fs.cosn.trsf.fs.ofs.user.appid": "1250000000"
        },
        "fieldDelimiter": ",",
        "writeMode": "append"
      }
    }
  }]
 }
}
```

Notes:
- Configure `hadoopConfig` as required for cosn.
- Set `defaultFS` to the COSN path, such as `cosn://examplebucket-1250000000/`.
- Change `fs.cosn.userinfo.region` and `fs.cosn.trsf.fs.ofs.bucket.region` to the bucket region, such as `ap-guangzhou`. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- For `COS_SECRETID` and `COS_SECRETKEY`, use your own COS key information.
- Change `fs.ofs.user.appid` and `fs.cosn.trsf.fs.ofs.user.appid` to your `appid`.

>!
>`fs.cosn.trsf.fs.ofs.bucket.region` and `fs.cosn.trsf.fs.ofs.user.appid` have been removed from Hadoop-COS 8.1.7 and later. Therefore, note the version difference during use. For other configurations, see the [reader](https://github.com/alibaba/DataX/blob/master/hdfsreader/doc/hdfsreader.md) and [writer](https://github.com/alibaba/DataX/blob/master/hdfswriter/doc/hdfswriter.md) configuration items of HDFS.

### Migrating data

Save the configuration file as `hdfs_job.json` in the `job` directory and run the following command:

```bash
[root@172 /usr/local/service/datax]# python bin/datax.py job/hdfs_job.json 
```

The resulting output is as shown below:

```plaintext
2022-10-23 00:25:24.954 [job-0] INFO  JobContainer - 
         [total cpu info] => 
                averageCpu                     | maxDeltaCpu                    | minDeltaCpu                    
                -1.00%                         | -1.00%                         | -1.00%
                        
         [total gc info] => 
                 NAME                 | totalGCCount       | maxDeltaGCCount    | minDeltaGCCount    | totalGCTime        | maxDeltaGCTime     | minDeltaGCTime     
                 PS MarkSweep         | 1                  | 1                  | 1                  | 0.034s             | 0.034s             | 0.034s             
                 PS Scavenge          | 14                 | 14                 | 14                 | 0.059s             | 0.059s             | 0.059s             
2022-10-23 00:25:24.954 [job-0] INFO  JobContainer - PerfTrace not enable!
2022-10-23 00:25:24.954 [job-0] INFO  StandAloneJobContainerCommunicator - Total 1000003 records, 9322478 bytes | Speed 910.40KB/s, 100000 records/s | Error 0 records, 0 bytes |  All Task WaitWriterTime 1.000s |  All Task WaitReaderTime 6.259s | Percentage 100.00%
2022-10-23 00:25:24.955 [job-0] INFO  JobContainer - 
Job start time                    : 2022-10-23 00:25:12
Job end time                    : 2022-10-23 00:25:24
Job duration                    :                 12s
Average job traffic                    :          910.40 KB/s
Record write speed                    :         100000 records/s
Total number of read records                    :             1000003
Read/Write failure count                    :                   0
```

## Ranger and Kerberos Use Cases

In the Hadoop permission system, Kerberos and Ranger are responsible for authentication and authorization respectively. After Ranger and Kerberos are enabled, you can use DataX to connect buckets with metadata acceleration enabled in similar steps, but you need to perform additional operations and configurations.

1. A bucket with metadata acceleration enabled supports the COS Ranger service, which will be automatically installed when you purchase the Ranger and COS Ranger components in the EMR console. You can also install it by yourself as instructed in [CHDFS Ranger Permission System Solution](https://intl.cloud.tencent.com/document/product/1106/41973).
2. Copy `cosn-ranger-interface-1.x.x-${version}.jar` and `hadoop-ranger-client-for-hadoop-${version}.jar` to `plugin/reader/hdfsreader/libs/` and `plugin/writer/hdfswriter/libs/` in the extracted DataX path. Click [here](https://github.com/tencentyun/cos-ranger-service) to download them.
3. Enter the bucket with metadata acceleration enabled, select **Ranger authentication** for **HDFS Authentication Mode**, and configure the Ranger address (not the COS Ranger address).

4. Configure `hdfsreader` and `hdfswriter` in the JSON configuration file.
```json
{
  "job": {
  "setting": {
    "speed": {
      "byte": 10485760
    },
    "errorLimit": {
      "record": 0,
      "percentage": 0.02
    }
  },
  "content": [{
    "reader": {
      "name": "hdfsreader",
      "parameter": {
        "path": "/test/",
        "defaultFS": "cosn://examplebucket1-1250000000/",
        "column": ["*"],
        "fileType": "text",
        "encoding": "UTF-8",
        "hadoopConfig": {
          "fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
          "fs.cosn.trsf.fs.ofs.bucket.region": "ap-guangzhou",
          "fs.cosn.bucket.region": "ap-guangzhou",
          "fs.cosn.tmp.dir": "/tmp/hadoop_cos",
          "fs.cosn.trsf.fs.ofs.tmp.cache.dir": "/tmp/",
          "fs.cosn.trsf.fs.ofs.user.appid": "1250000000",
          "fs.cosn.credentials.provider": "org.apache.hadoop.fs.auth.RangerCredentialsProvider",
          "qcloud.object.storage.zk.address": "172.16.0.30:2181",
          "qcloud.object.storage.ranger.service.address": "172.16.0.30:9999",
          "qcloud.object.storage.kerberos.principal": "hadoop/172.16.0.30@EMR-5IUR9VWW"
        },
        "haveKerberos": "true",
        "kerberosKeytabFilePath": "/var/krb5kdc/emr.keytab",
        "kerberosPrincipal": "hadoop/172.16.0.30@EMR-5IUR9VWW",
        "fieldDelimiter": ","
      }
    },
    "writer": {
      "name": "hdfswriter",
      "parameter": {
        "path": "/",
        "fileName": "hive.test",
        "defaultFS": "cosn://examplebucket2-1250000000/",
        "column": [
          {"name":"col1","type":"int"},
          {"name":"col2","type":"string"}
        ],
        "fileType": "text",
        "encoding": "UTF-8",
        "hadoopConfig": {
          "fs.cosn.impl": "org.apache.hadoop.fs.CosFileSystem",
          "fs.cosn.trsf.fs.ofs.bucket.region": "ap-guangzhou",
          "fs.cosn.bucket.region": "ap-guangzhou",
          "fs.cosn.tmp.dir": "/tmp/hadoop_cos",
          "fs.cosn.trsf.fs.ofs.tmp.cache.dir": "/tmp/",
          "fs.cosn.trsf.fs.ofs.user.appid": "1250000000",
          "fs.cosn.credentials.provider": "org.apache.hadoop.fs.auth.RangerCredentialsProvider",
          "qcloud.object.storage.zk.address": "172.16.0.30:2181",
          "qcloud.object.storage.ranger.service.address": "172.16.0.30:9999",
          "qcloud.object.storage.kerberos.principal": "hadoop/172.16.0.30@EMR-5IUR9VWW"
        },
        "haveKerberos": "true",
        "kerberosKeytabFilePath": "/var/krb5kdc/emr.keytab",
        "kerberosPrincipal": "hadoop/172.16.0.30@EMR-5IUR9VWW",
        "fieldDelimiter": ",",
        "writeMode": "append"
      }
    }
  }]
 }
}
```

The new configuration items are as detailed below:

- Set `fs.cosn.credentials.provider` to `org.apache.hadoop.fs.auth.RangerCredentialsProvider` to use Ranger for authorization.
- Set `qcloud.object.storage.zk.address` to the ZooKeeper address.
- Set `qcloud.object.storage.ranger.service.address` to the COS Ranger address.
- Set `haveKerberos` to `true`.
- Set `qcloud.object.storage.kerberos.principal` and `kerberosPrincipal` to the Kerberos authentication principal name (which can be read from `core-site.xml` in the EMR environment with Kerberos enabled).
- Set `kerberosKeytabFilePath` to the absolute path of the `keytab` authentication file (which can be read from `ranger-admin-site.xml` in the EMR environment with Kerberos enabled).

## FAQs

### What should I do if the `java.io.IOException: Permission denied: no access groups bound to this mountPoint examplebucket2-1250000000, access denied` or `java.io.IOException: Permission denied: No access rules matched` error is reported?

Check whether the IP address or IP range of the server is set in the VPC network configuration in **HDFS Permission Configuration**; for example, the IP addresses of all nodes must be configured for EMR.

### What should I do if the `java. lang. RuntimeException: java. lang.ClassNotFoundException: Class org.apache.hadoop.fs.con.ranger.client.RangerQcloudObjectStorageClientImpl not found` error is reported?

Check whether `cosn-ranger-interface-1.x.x-${version}.jar` and `hadoop-ranger-client-for-hadoop-${version}.jar` have been copied to `plugin/reader/hdfsreader/libs/` and `plugin/writer/hdfswriter/libs/` in the extracted DataX path (click [here](https://github.com/tencentyun/cos-ranger-service) to download them).

### What should I do if the `java.io.IOException: Login failure for hadoop/_HOST@EMR-5IUR9VWW from keytab /var/krb5kdc/emr.keytab: javax.security.auth.login.LoginException: Unable to obtain password from user` error is reported?

Check whether `kerberosPrincipal` and `qcloud.object.storage.kerberos.principal` are mistakenly set to `hadoop/_HOST@EMR-5IUR9VWW` instead of `hadoop/172.16.0.30@EMR-5IUR9VWW`. As DataX cannot resolve a `_HOST` domain name, you need to replace `_HOST` with an IP. You can run the `klist -ket /var/krb5kdc/emr.keytab` command to find an appropriate principal.

### What should I do if the `java.io.IOException: init fs.cosn.ranger.plugin.client.impl failed` error is reported?

Check whether `qcloud.object.storage.kerberos.principal` is configured in `hadoopConfig` in the JSON file, and if not, you need to configure it.

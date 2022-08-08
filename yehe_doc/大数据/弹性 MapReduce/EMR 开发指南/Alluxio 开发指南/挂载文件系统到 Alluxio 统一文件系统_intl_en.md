## Background
Alluxio provides a unified namespace mechanism that allows other file systems to be mounted to the file system of Alluxio. In addition, it allows upper-layer applications to use the unified namespace to access data scattered across different systems.

### Mounting COS

**Sample: Mounting a COS bucket to an Alluxio directory**
```
bin/alluxio fs mount --option fs.cos.access.key=<COS_SECRET_ID> \
   --option fs.cos.secret.key=<COS_SECRET_KEY> \
   --option fs.cos.region=<COS_REGION> \
   --option fs.cos.app.id=<COS_APP_ID> \
   /cos cos://<COS_BUCKET>/
```
Configure the COS information in each `--option`.

| Configuration Item | Description |
|--|--|
|fs.cos.access.key | The COS secret ID |
|fs.cos.secret.key | The COS secret key |
|fs.cos.region | The COS region name, such as `ap-beijing` |
|fs.cos.app.id | Your `AppID` |
|COS_BUCKET | The COS bucket name **without the `AppID` suffix** |

This command mounts the COS directory specified by `cos://bucket/xxx` to the `/cos` directory in Alluxio.

### Mounting HDFS
**Sample: Mounting an HDFS directory to an Alluxio directory**
```
`bin/alluxio fs mount /hdfs hdfs://data` 
```
This command mounts the `/data` directory of HDFS to the `/hdfs` subdirectory of Alluxio.
After the mount is successful, the mounted content can be viewed by running the `alluxio fs ls` command.

### Mounting CHDFS
**Sample: Mounting CHDFS to Alluxio through `mount`**
>? This is supported only for EMR 2.5.0 or later + Alluxio 2.3.0 or later.
>
```
alluxio fs mount   \ 
--option alluxio.underfs.hdfs.configuration=/usr/local/service/hadoop/etc/hadoop/core-site.xml  \
/chdfs ofs://f4modr7kmvw-wMqw.chdfs.ap-chongqing.myqcloud.com
```

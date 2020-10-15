## Background

Alluxio provides a unified namespace mechanism that allows other file systems to be mounted to the file system of Alluxio. In addition, it allows upper-layer applications to use the unified namespace to access data scattered across different systems.

## Operations
```
bin/alluxio fs mount <alluxio-path> <source-path>
```

**Example 1. Mounting a COS bucket to an Alluxio directory**

```
bin/alluxio fs mount --option fs.cos.access.key=<COS_SECRET_ID> \
    --option fs.cos.secret.key=<COS_SECRET_KEY> \
    --option fs.cos.region=<COS_REGION> \
    --option fs.cos.app.id=<COS_APP_ID> \
    /cos cos://<COS_BUCKET>/
```

>!AppID is optional.
>

Configure the COS configuration information in --options.

| Configuration Item          | Description                                   |
| ----------------- | -------------------------------------- |
| fs.cos.access.key | COS scecretId                         |
| fs.cos.secret.key | COS secretKey                         |
| fs.cos.region     | COS region name such as `ap-beijing` |
| fs.cos.app.id     | User AppID                              |
| COS_BUCKET        | COS bucket name. **Name only without the AppID extension**                         |

This command mounts the COS directory (specified by `cos://bucket/xxx`) to the `/cos` directory in Alluxio. 

**Example 2. Mounting an HDFS directory to an Alluxio directory**
```
bin/alluxio fs mount /hdfs hdfs://data
```
This command mounts the `/data` directory of HDFS to the `/hdfs` subdirectory of Alluxio.

After the mount is successful, the mounted content can be viewed by running the `alluxio fs ls` command.

 **Example 3. Mounting an CHDFS directory to an Alluxio directory**
```
alluxio fs mount   \ 
 --option alluxio.underfs.hdfs.configuration=/usr/local/service/hadoop/etc/hadoop/core-site.xml  \
/chdfs ofs://f4modr7kmvw-wMqw.chdfs.ap-chongqing.myqcloud.com
```


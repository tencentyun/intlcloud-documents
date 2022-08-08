Authentication is not required when Alluxio users access data from COS, HDFS, or CHDFS in the existing unified namespace or access the data cached in Alluxio through Transparent-URI; that is, any user can get the data as long as they get the URI. In view of this, EMR-Alluxio improves authentication based on Ranger and COSRanger.

>? To configure the authentication feature, make sure that the cluster is integrated with the following components:
>- If only HDFS is mounted to Alluxio, you need to integrate the Ranger component.
>- If COS and CHDFS are mounted to Alluxio, you need to integrate the COSRanger component.

## Supported Versions
- Supported service component version: Alluxio v2.8.0.
- Product version: Hadoop 3.x Standard EMR 3.4.0.

## Configuring Authentication
### Prerequisite configuration
```
# Add the `ranger-hive-security.xml` configuration item in the Hive component
ranger.plugin.hive.urlauth.filesystem.schemes==hdfs:,file:,wasb:,adl:,alluxio:

# Add the `hive.properties` configuration item in the Presto component
hive.hdfs.authentication.type=NONE
hive.metastore.authentication.type=NONE
hive.hdfs.impersonation.enabled=true
hive.metastore.thrift.impersonation.enabled=true
```
>? The above prerequisite configuration items need to be configured based on the existing components in your cluster.

### HDFS authentication
Create a soft link to the Ranger configuration file as follows:
```
[hadoop@172 conf]$ pwd
/usr/local/service/alluxio/conf
[hadoop@172 conf]$ ln -s /usr/local/service/hadoop/etc/hadoop/ranger-hdfs-audit.xml
ranger-hdfs-audit.xml
[hadoop@172 conf]$ ln -s /usr/local/service/hadoop/etc/hadoop/ranger-hdfs-security.xml ranger-hdfs-security.xml
```

**Configure `alluxio-site.properties`**
We recommend you deliver the cluster configuration in the EMR console.
```
# Authentication switch (`false` by default)
alluxio.security.authorization.plugins.enabled=true
alluxio.security.authorization.plugin.name=ranger
alluxio.security.authorization.plugin.paths=/usr/local/service/alluxio/conf
alluxio.underfs.security.authorization.plugin.name=ranger
alluxio.underfs.security.authorization.plugin.paths=/usr/local/service/alluxio/conf
alluxio.master.security.impersonation.hadoop.users=*
alluxio.security.login.impersonation.username=_HDFS_USER_
```
>? You need to restart the Alluxio service after the delivery is completed.
>
### COS and CHDFS authentication

```
# Add the `core-site.xml` configuration item
fs.ofs.ranger.enable.flag=true
```

**Configure `alluxio-site.properties`**
We recommend you deliver the cluster configuration in the EMR console.
```
# Authentication switch (`false` by default)
# Authentication switch (`false` by default)
alluxio.security.authorization.plugins.enabled=true
alluxio.security.authorization.plugin.name=ranger
alluxio.security.authorization.plugin.paths=/usr/local/service/alluxio/conf
alluxio.underfs.security.authorization.plugin.name=ranger
alluxio.underfs.security.authorization.plugin.paths=/usr/local/service/alluxio/conf
alluxio.cos.qcloud.object.storage.ranger.service.config.dir=/usr/local/service/cosranger/conf
alluxio.master.security.impersonation.hadoop.users=*
alluxio.security.login.impersonation.username=_HDFS_USER_
# The number of retries is 5 by default.
alluxio.cos.qcloud.object.storage.permission.check.max.retry=5
```
>? You need to restart the Alluxio service after the delivery is completed.

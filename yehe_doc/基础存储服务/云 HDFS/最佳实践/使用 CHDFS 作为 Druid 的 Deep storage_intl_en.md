## Environment Dependencies

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).
- Druid version: Druid 0.12.1

## Download and Installation

#### Getting CHDFS JAR

Download [CHDFS JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).

#### Installing CHDFS JAR

Using CHDFS as Druid's deep storage requires `Druid-hdfs-extension`.
After downloading the CHDFS JAR, copy `chdfs_hadoop_plugin_network-1.7.jar` to the Druid installation path `extensions/druid-hdfs-storage` and `hadoop-dependencies/hadoop-client/2.x.x`.

## Directions

#### Modifying configuration

1. Modify the `conf/druid/_common/common.runtime.properties` file at the Druid installation path, add the `extension` of HDFS to `druid.extensions.loadList`, specify HDFS as Druid's deep storage, and enter the path of the CHDFS instance:
```plaintext
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=ofs://<mountpoint>/<druid-path>
```
2. In the `conf/druid/_common/` directory, create the HDFS configuration file `hdfs-site.xml` and enter the configuration information of the CHDFS instance:

<dx-codeblock>
::: xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at
    http://www.apache.org/licenses/LICENSE-2.0
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License. See accompanying LICENSE file.
-->
<!-- Put site-specific property overrides in this file. -->
<configuration>
 <property>
    <name>fs.AbstractFileSystem.ofs.impl</name>
    <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
 </property>
 <property>
    <name>fs.ofs.impl</name>
    <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
 </property>
 <!--Temporary directory of the local cache. For data read/write, data will be written to the local disk when the memory cache is insufficient. This path will be created automatically if it does not exist-->
 <property>
    <name>fs.ofs.tmp.cache.dir</name>
    <value>/data/chdfs_tmp_cache</value>
 </property>
 <!--You need to replace `appId` with your own `appid`, which can be obtained at https://console.cloud.tencent.com/cam/capi-->      
 <property>
    <name>fs.ofs.user.appid</name>
    <value>125000001</value>
 </property>
</configuration>
:::
</dx-codeblock>

The supported items of the above configuration are completely consistent with those as described at the CHDFS website. For more information, please see [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965).

#### Starting to use
Start the Druid processes in turn, and Druid data can be loaded into CHDFS.


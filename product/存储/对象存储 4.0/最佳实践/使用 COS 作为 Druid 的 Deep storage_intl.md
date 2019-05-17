## Environment Dependencies

[HADOOP-COS](https://github.com/tencentyun/hadoop-cos) and Hadoop-COS-Java-SDK (included in the dep directory of HADOOP-COS)

Druid version: Druid-0.12.1

## Download and Installation

### Obtain hadoop-cos 

Download [HADOOP-COS](https://github.com/tencentyun/hadoop-cos) from Github official platform.

### Install hadoop-cos
Druid-hdfs-extension is required if Druid uses COS for Deep Storage.
After downloading HADOOP-COS, copy hadoop-cos-2.xxjar and cos_hadoop_api-5.2.6.jar from the dep directory to extensions/druid-hdfs-storage and hadoop-dependencies/hadoop-client/2.x.x under druid's installation path.


## Directions
### Modify configuration

First, modify the file conf/druid/_common/common.runtime.properties under druid's installation path, add the extension of hdfs to druid.extensions.loadList, specify hdfs as druid's deep storage, and enter the path of cosn:

```
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=cosn://bucket-appid/<druid-path>
```

Create a hdfs configuration file hdfs-site.xml under the directory conf/druid/_common/, and enter COS's keys and other information:

```xml
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
        <name>fs.cosn.userinfo.secretId</name>
        <value>xxxxxxxxxxxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.cosn.userinfo.secretKey</name>
        <value>xxxxxxxxxxxxxxx</value>
    </property>
    <property>
        <name>fs.cosn.impl</name>
        <value>org.apache.hadoop.fs.CosFileSystem</value>
    </property>
    <property>
        <name>fs.cosn.userinfo.region</name>
        <value>ap-xxxx</value>
    </property>
    <property>
        <name>fs.cosn.tmp.dir</name>
        <value>/tmp/hadoop_cos</value>
    </property>
</configuration>
```

The supported items for the above configuration are exactly the same as those described in the document on the HADOOP-COS official website. For more information,see [HADOOP-COS official document](https://cloud.tencent.com/document/product/436/6884).

### Getting started

After the druid processes are started in turn, the Druid data can be loaded into the COS.


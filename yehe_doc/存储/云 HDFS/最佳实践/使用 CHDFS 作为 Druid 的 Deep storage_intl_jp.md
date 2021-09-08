## 環境の依存

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)。
- Druidバージョン：Druid-0.12.1。

### ダウンロードとインストール

#### CHDFS JARの取得

公式Githubで[CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)をダウンロードします。

#### CHDFS JARのインストール

DruidのDeep StorageとしてCHDFSを使用するには、Druid-hdfs-extensionによって実現する必要があります。
CHDFS JARをダウンロードした後、`chdfs_hadoop_plugin_network-1.7.jar`をDruidインストールパス`extensions/druid-hdfs-storage`および`hadoop-dependencies/hadoop-client/2.x.x`にコピーします。

## 使用方法

#### 設定の変更

1. Druidインストールパスの`conf/druid/_common/common.runtime.properties`ファイルを変更し、hdfsのextensionを`druid.extensions.loadList`に追加すると同時に、hdfsをDruidのdeep storageとして指定します。そして、パスはCHDFSのパスとして入力します。

```plaintext
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=ofs://<mountpoint>/<druid-path>
```

2. このディレクトリ`conf/druid/_common/`下に、hdfsの設定ファイルhdfs-site.xmlを新規作成し、CHDFSの設定情報などを入力します。
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
 <!--ローカルcacheの一時ディレクトリ。データの読み取りと書き込みの場合、メモリcacheが不足すると、ローカルディスクに書き込まれます。このパスが存在しない場合は、自動的に作成されます-->
 <property>
    <name>fs.ofs.tmp.cache.dir</name>
    <value>/data/chdfs_tmp_cache</value>
 </property>
 <!--appIdユーザーは、ご自身のappidに変更する必要があります。https://console.cloud.tencent.com/cam/capiから取得できます-->      
 <property>
    <name>fs.ofs.user.appid</name>
    <value>125000001</value>
 </property>
</configuration>
:::
</dx-codeblock>

上記の設定のサポート項目は、CHDFSの公式ウェブサイトの説明と全く同じです。詳細については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)ドキュメントをご参照ください。

#### 使用の開始
Druidプロセスを順次起動すると、DruidデータをCHDFSにロードできます。


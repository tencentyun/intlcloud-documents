## 環境への依存

[HADOOP-COS](https://github.com/tencentyun/hadoop-cos)とHadoop-COS-Java-SDK（HADOOP-COSのdepディレクトリに含まれる）。

Druidバージョン：Druid-0.12.1

## ダウンロードおよびインストール

### hadoop-cosの取得

公式のGithubで[HADOOP-COS](https://github.com/tencentyun/hadoop-cos)をダウンロードします。

### hadoop-cosのインストール
DruidがCOSをDeep Storageとして使用するには、Druid-hdfs-extensionを使用して実装する必要があります。
HADOOP-COSをダウンロードした後、depディレクトリ内のhadoop-cos-2.x.x.jarおよびcos_hadoop_api-5.2.6.jarをdruidインストールパスのextensions/druid-hdfs-storageおよびhadoop-dependencies/hadoop-client/2.x.xにコピーします。


## 使用方法
### 構成の変更

まず、druidインストールパスのconf/druid/_common/common.runtime.propertiesファイルを変更して、hdfsのextensionをdruid.extensions.loadListに追加する同時に、hdfsをdruidのdeep storageに指定します。パスはcosnのパスとして記入されます。

```
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=cosn://bucket-appid/<druid-path>
```

次に、conf/druid/_common/ディレクトリに新しいhdfs構成ファイルhdfs-site.xmlを作成し、COSの暗号鍵情報などを入力します。

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

上記の構成のサポート項目はHADOOP-COS公式Webサイトのドキュメントの説明と完全に一致しています。[HADOOP-COS公式サイトのドキュメント](https://cloud.tencent.com/document/product/436/6884)を参照してください。

### 使用開始

最後に、druidのプロセスを順に起動した後、DruidのデータをCOSにロードできるようになります。

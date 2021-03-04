## 환경 종속

- [HADOOP-COS](https://github.com/tencentyun/hadoop-cos)와 Hadoop-COS-Java-SDK(HADOOP-COS의 dep 디렉터리 안에 포함)
- Druid 버전: Druid-0.12.1.

## 다운로드 및 설치

#### HADOOP-COS 다운로드 

운영사 Github에서 [HADOOP-COS](https://github.com/tencentyun/hadoop-cos)를 다운로드하십시오.

#### HADOOP-COS 설치
Druid가 COS를 Deep Storage로 사용하려면 Druid-hdfs-extension이 필요합니다.
HADOOP-COS를 다운로드한 후 dep 디렉터리의 `hadoop-cos-2.x.x.jar` 버전을 Druid의 설치 경로인 `extensions/druid-hdfs-storage`와 `hadoop-dependencies/hadoop-client/2.x.x`에 복사합니다. Druid가 HDFS plugin을 사용하여 COS에 액세스하기 때문에 선택한 버전이 Druid의 HDFS plugin 버전과 일치해야 합니다.

## 사용 방법
### 수정 설정

1. Druid 설치 경로인 `conf/druid/_common/common.runtime.properties` 파일을 수정합니다. hdfs의 extension을 `druid.extensions.loadList`에 추가합니다. hdfs를 Druid의 deep storage로 지정하고 경로는 cosn 경로로 작성합니다.
```shell
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=cosn://bucket-appid/<druid-path>
```
2. `conf/druid/_common/` 디렉터리에 hdfs의 구성 파일 hdfs-site.xml을 새로 만들고 COS의 키 정보 등을 작성합니다.
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

위에서 설정한 지원 항목은 HADOOP-COS 공식 홈페이지의 문서 설명과 동일하며 자세한 내용은 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884) 문서를 참조하십시오.

#### 사용하기

Druid 프로세스에 따라 실행하면 Druid 데이터가 COS에 로딩됩니다.

## 환경 의존

[HADOOP-COS](https://github.com/tencentyun/hadoop-cos)와 Hadoop-COS-Java-SDK(HADOOP-COS의 dep 디렉터리에 포함됨)

Druid 버전: Druid-0.12.1

## 다운로드 및 설치

### hadoop-cos 획득 

공식 Github에서 [HADOOP-COS](https://github.com/tencentyun/hadoop-cos)를 다운로드합니다.

### hadoop-cos 설치
Druid는 COS를 Deep Storage로 사용하며 Druid-hdfs-extension을 빌려 구현됩니다.
HADOOP-COS를 다운로드한 후 dep 디렉터리 하의 hadoop-cos-2.x.x.jar 및 cos_hadoop_api-5.2.6.jar을 druid 설치 경로인 extensions/druid-hdfs-storage 및 hadoop-dependencies/hadoop-client/2.x.x에 복사합니다.


## 사용 방법
### 구성 수정

우선 druid 설치 경로 중의 conf/druid/_common/common.runtime.properties 파일을 수정한 후 hdfs의 extension을 druid.extensions.loadList에 추가합니다. 동시에 hdfs를 druid의 deep storage로 지정하며 경로는 cosn의 경로를 입력합니다.

```
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=cosn://bucket-appid/<druid-path>
```

다음 conf/druid/_common/ 이 디렉터리에 하나의 hdfs 구성 파일인 hdfs-site.xml을 새로 생성하고 COS의 키 정보 등을 입력합니다.

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

상기 구성의 지원 항목은 HADOOP-COS 공식 홈페이지의 문서에서 기술한 것과 완전하게 일치합니다. [HADOOP-COS 공식 홈페이지 문서](https://cloud.tencent.com/document/product/436/6884)를 참조하십시오.

### 시작 가이드

마지막으로 순서에 따라 druid의 진행 프로세스를 시작한 후 Druid의 데이터는 COS에 로딩될 수 있습니다.


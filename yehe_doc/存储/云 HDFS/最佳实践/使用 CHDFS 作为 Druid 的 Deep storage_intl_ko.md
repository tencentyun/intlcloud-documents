## 환경 종속

- [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin).
- Druid 버전: Druid-0.12.1.

## 다운로드 및 설치

#### CHDFS JAR 다운로드

운영사 Github에서 [CHDFS_JAR](https://github.com/tencentyun/chdfs-hadoop-plugin)을 다운로드하십시오.

#### CHDFS JAR 설치

CHDFS를 Druid의 Deep Storage로 사용하려면 Druid-hdfs-extension이 필요합니다.
CHDFS JAR을 다운로드한 후, `chdfs_hadoop_plugin_network-1.7.jar`을 Druid 설치 경로 `extensions/druid-hdfs-storage` 및 `hadoop-dependencies/hadoop-client/2.x.x`로 복사합니다. 

## 사용 방법

#### 설정 수정

1. Druid 설치 경로인 `conf/druid/_common/common.runtime.properties` 파일을 수정하고 hdfs의 extension을 `druid.extensions.loadList`에 추가합니다. hdfs를 Druid의 deep storage로 지정하고 경로는 CHDFS 경로로 작성합니다.

```plaintext
properties
druid.extensions.loadList=["druid-hdfs-storage"]
druid.storage.type=hdfs
druid.storage.storageDirectory=ofs://<mountpoint>/<druid-path>
```

2. `conf/druid/_common/` 디렉터리에 hdfs의 구성 파일 hdfs-site.xml을 새로 만들고 CHDFS의 설정 정보 등을 작성합니다.

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
    <name>fs.AbstractFileSystem.ofs.impl</name>
    <value>com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter</value>
 </property>
 <property>
    <name>fs.ofs.impl</name>
    <value>com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter</value>
 </property>
 <!--로컬 cache의 임시 디렉터리로, 데이터 읽기/쓰기의 경우 메모리 cache가 부족할 때는 로컬 디스크에 쓰기 하고 관련 경로가 없을 때는 자동 생성합니다.-->
 <property>
    <name>fs.ofs.tmp.cache.dir</name>
    <value>/data/chdfs_tmp_cache</value>
 </property>
 <!--appId 사용자는 본인 appid로 변경해야 하며，https://console.cloud.tencent.com/cam/capi에서 획득할 수 있습니다.-->      
 <property>
    <name>fs.ofs.user.appid</name>
    <value>125000001</value>
 </property>
</configuration>
```

위에서 설정한 지원 항목은 CHDFS 공식 홈페이지의 문서 설명과 동일하며 자세한 내용은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965)문서를 참고하십시오.

#### 사용하기
Druid 프로세스에 따라 실행하면 Druid 데이터가 CHDFS에 로딩됩니다.


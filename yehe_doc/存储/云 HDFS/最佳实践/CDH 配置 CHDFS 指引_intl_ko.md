## 소개

CDH(Cloudera's Distribution, including Apache Hadoop)는 업계에서 각광받는 Hadoop의 릴리스 버전입니다. 본 문서는 CDH 환경에서 Tencent Cloud CHDFS 서비스 사용법을 소개합니다. 이 기능을 통해 빅 데이터 컴퓨팅과 스토리지를 분리하여 효율적인 저비용 빅 데이터 솔루션을 제공합니다.

CHDFS 빅 데이터 모듈은 다음과 같은 상황을 지원합니다. 

| 모듈 이름 | CHDFS 빅 데이터 모듈 지원 현황 | 서비스 모듈 재시작 필요 여부                         |
| -------- | ------------------------ | ------------------------------------------ |
| Yarn     | 지원                    | NodeManager 재시작                             |
| Yarn     | 지원                    | NodeManager 재시작                             |
| Hive     | 지원                    | HiveServer 및 HiveMetastore 재시작             |
| Spark    | 지원                    | NodeManager 재시작                             |
| Sqoop    | 지원                    | NodeManager 재시작                             |
| Presto   | 지원                    | HiveServer, HiveMetastore, Presto 재시작 |
| Flink    | 지원                 | 필요 없음                                         |
| Impala   | 지원                    | 필요 없음                                         |
|  EMR   |  지원                      |       필요 없음                                        |
|자체구축 모듈  |  향후 지원                    |   없음                                         |
| HBase    | 권장하지 않음                    | 없음                                           |


## 버전 종속

본 문서에 종속된 모듈 버전은 다음과 같습니다.

- CDH 5.16.1
- Hadoop 2.6.0


## 사용 방법

### 스토리지 환경 설정

1. CDH 관리 페이지에 로그인합니다.
2. 시스템 메인 페이지에서 **설정**>**서비스 범위**>**고급**을 선택하여 코드 스니펫 고급 설정 페이지로 이동하면 다음 그림과 같이 표시됩니다.
   ![](https://main.qcloudimg.com/raw/09f053f2c0feaf4451d9bc4c70cb501d.png)
3. Cluster-wide Advanced Configuration Snippet(Safety Valve) for core-site.xml 코드 창에 CHDFS 설정을 입력합니다.

```
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
<value>/data/emr/hdfs/tmp/chdfs/</value>
</property>
<!--appId-->      
<property>
<name>fs.ofs.user.appid</name>
<value>1250000000</value>
</property>
```

다음은 CHDFS 필수 설정 항목(core-site.xml에 추가 필요)입니다. CHDFS의 기타 설정 항목은 [CHDFS 마운트](https://intl.cloud.tencent.com/document/product/1106/41965) 문서를 참고하십시오.

| CHDFS 설정 항목                   | 값                                               | 의미                                                         |
| ------------------------------ | ------------------------------------------------ | ------------------------------------------------------------ |
| fs.ofs.user.appid              | 1250000000                                       | 사용자 appid                                                   |
| fs.ofs.tmp.cache.dir           | /data/emr/hdfs/tmp/chdfs/                        | 로컬 cache 의 임시 디렉터리                                        |
| fs.ofs.impl                    | com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter | FileSystem에 대한 chdfs의 구현 클래스, com.qcloud.chdfs.fs.CHDFSHadoopFileSystemAdapter으로 고정 |
| fs.AbstractFileSystem.ofs.impl | com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter       |  AbstractFileSystem에 대한 chdfs의 구현 클래스, com.qcloud.chdfs.fs.CHDFSDelegateFSAdapter으로 고정 |

4. HDFS 서비스 작업을 진행하기 위해 클라이언트 배포 설정을 클릭하면 core-site.xml 설정이 클러스터 기기에 업데이트됩니다.
5. CHDFS 최신 SDK 패키지를 CDH HDFS 서비스의 jar 패키지 경로에 설치합니다. 다음 예시와 같이 실제 값에 따라 변경해 주십시오.

```
cp chdfs_hadoop_plugin_network-2.0.jar /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/hadoop-hdfs/
```

>!클러스터의 기기마다 동일한 위치에 SDK 패키지를 설치해야 합니다. 


<span id=1>

### 데이터 마이그레이션

Hadoop Distcp 툴을 사용하여 CDH HDFS 데이터를 CHDFS로 마이그레이션합니다. 자세한 내용은
[네이티브 HDFS 데이터 Tencent Cloud CHDFS로 마이그레이션](https://intl.cloud.tencent.com/document/product/1106/41970)을 참고하십시오. 

### 빅 데이터 세트로 CHDFS 사용

#### 1. MapReduce

**작업 순서**

(1) [데이터 마이그레이션](#1) 섹션에 따라 HDFS 관련 설정을 완료하고, CHDFS의 SDK jar 패키지를 HDFS의 해당 디렉터리에 넣습니다.
(2) CDH 시스템 메인 페이지에서 YARN을 찾아 NodeManager 서비스를 재시작합니다. TeraGen 명령어는 재시작할 필요가 없으나 TeraSort는 비즈니스 내부 로직으로 인해 NodeManger를 재시작해야 하므로, NodeManager 서비스를 일괄 재시작할 것을 권장합니다.

**예시**

Hadoop 표준 테스트의 TeraGen 및 TeraSort입니다.

```
hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar teragen -Dmapred.map.tasks=4 1099 cosn://examplebucket-1250000000/teragen_5/

hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar terasort  -Dmapred.map.tasks=4 cosn://examplebucket-1250000000/teragen_5/ cosn://examplebucket-1250000000/result14
```

>?`ofs://     schema` 뒷부분을 사용자 CHDFS의 마운트 포인트 경로로 변경하십시오.


#### 2. Hive

##### 2.1 MR 엔진

**작업 절차**

(1) [데이터 마이그레이션](#1) 섹션에 따라 HDFS 관련 설정을 완료하고, CHDFS의 SDK jar 패키지를 HDFS의 해당 디렉터리에 넣습니다.
(2) CDH 메인 페이지에서 HIVE 서비스를 찾아 Hiveserver2와 HiverMetastore 역할을 재시작합니다.

**예시**

사용자의 실제 작업 쿼리입니다. Hive 명령 라인을 실행하여 Location을 생성하고, 이를 CHDFS의 파티션 테이블로 사용하는 경우입니다.

```plaintext
CREATE TABLE `report.report_o2o_pid_credit_detail_grant_daily`(
  `cal_dt` string,
  `change_time` string,
  `merchant_id` bigint,
  `store_id` bigint,
  `store_name` string,
  `wid` string,
  `member_id` bigint,
  `meber_card` string,
  `nickname` string,
  `name` string,
  `gender` string,
  `birthday` string,
  `city` string,
  `mobile` string,
  `credit_grant` bigint,
  `change_reason` string,
  `available_point` bigint,
  `date_time` string,
  `channel_type` bigint,
  `point_flow_id` bigint)
PARTITIONED BY (
  `topicdate` string)
ROW FORMAT SERDE
  'org.apache.hadoop.hive.ql.io.orc.OrcSerde'
STORED AS INPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcInputFormat'
	OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.orc.OrcOutputFormat'
LOCATION
  'cosn://examplebucket-1250000000/user/hive/warehouse/report.db/report_o2o_pid_credit_detail_grant_daily'
TBLPROPERTIES (
  'last_modified_by'='work',
  'last_modified_time'='1589310646',
  'transient_lastDdlTime'='1589310646')
```

sql 쿼리 실행:

```
select count(1) from report.report_o2o_pid_credit_detail_grant_daily;
```

모니터링 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/28a566e5f08d7cbbeb4893b851565c01.png)

##### 2.2 Tez 엔진

Tez 엔진은 CHDFS의 jar 패키지를 Tez의 압축 패키지 내로 가져와야 합니다. 다음은 apache-tez.0.8.5를 예시로 한 설명입니다.

**작업 절차**

(1) CDH 클러스터에 설치한 tez 패키지를 찾은 후 압축을 해제합니다. /usr/local/service/tez/tez-0.8.5.tar.gz를 예로 들 수 있습니다.
(2) CHDFS의 jar 패키지를 압축 해제한 디렉터리에 넣고 다시 하나의 압축 패키지로 만듭니다.
(3) 새로 생성한 압축 패키지를 tez.lib.uris에서 지정한 경로(경로가 이미 있는 경우 변경 가능)에 업로드합니다.
(4) CDH 메인 페이지에서 HIVE를 찾아 hiveserver와 hivemetastore를 재시작합니다.

#### 3. Spark

**작업 절차**

(1) [데이터 마이그레이션](#1) 섹션에 따라 HDFS 관련 설정을 완료하고, CHDFS의 SDK jar 패키지를 HDFS의 해당 디렉터리에 넣습니다.
(2) NodeManager 서비스를 재시작합니다.

**예시**

CHDFS에서 Spark example word count 테스트를 진행합니다.

```
spark-submit  --class org.apache.spark.examples.JavaWordCount --executor-memory 4g --executor-cores 4  ./spark-examples-1.6.0-cdh5.16.1-hadoop2.6.0-cdh5.16.1.jar cosn://examplebucket-1250000000/wordcount
```

실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/5070c17e6db105f7b1d20c609f334b60.png)


#### 4. Sqoop

**작업 절차**

(1) [데이터 마이그레이션](#1) 섹션에 따라 HDFS 관련 설정을 완료하고, CHDFS의 SDK jar 패키지를 HDFS의 해당 디렉터리에 넣습니다.

(2) CHDFS의 SDK jar 패키지를 sqoop 디렉터리에 넣어야 합니다(예시: /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/sqoop/).

(3) NodeManager 서비스를 재시작합니다.

**예시**

MYSQL 테이블을 CHDFS로 내보냅니다. [관계형 데이터베이스 및 HDFS의 가져오기/내보내기](https://intl.cloud.tencent.com/document/product/1026/31157) 문서를 참고하여 테스트를 진행하십시오.

```
sqoop import --connect "jdbc:mysql://IP:PORT/mysql" --table sqoop_test --username root --password 123  --target-dir cosn://examplebucket-1250000000/sqoop_test
```

실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/3b27f8417460e8edfa7f8f11cbef3f4f.png)


#### 5. Presto

**작업 절차**

(1) [데이터 마이그레이션](#1) 섹션에 따라 HDFS 관련 설정을 완료하고, CHDFS의 SDK jar 패키지를 HDFS의 해당 디렉터리에 넣습니다.
(2) CHDFS의 SDK jar 패키지는 presto 디렉터리에 넣어야 합니다(예시: /usr/local/services/cos_presto/plugin/hive-hadoop2).
(3) presto는 hadoop common의 gson-2.*.*.jar를 로딩할 수 없으므로 gson-2.*.*.jar 또한 presto 디렉터리에 넣어야 합니다(예시: /usr/local/services/cos_presto/plugin/hive-hadoop2, CHDFS만 gson에 종속됨).
(4) HiveServer, HiveMetaStore, Presto 서비스를 재시작합니다.

**예시**

HIVE에서 Location이 CHDFS인 테이블 쿼리를 생성합니다.

```
select * from chdfs_test_table where bucket is not null limit 1;
```

>?chdfs_test_table은 location이 ofs scheme인 테이블입니다. 

쿼리 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/c5dc086fefbc32ad116e91524e7102ad.png)

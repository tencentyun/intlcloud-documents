## 소개

CDH(Cloudera's Distribution, including Apache Hadoop)는 업계에서 유명한 Hadoop 릴리스 버전입니다. 본 문서는 CDH 환경에서 COSN 스토리지 서비스를 사용하여 빅 데이터 계산과 스토리지 분리로 효율적이고 저렴한 빅 데이터 솔루션을 구현하는 방법에 대한 내용입니다.

>?COSN은 Hadoop-COS 파일 시스템의 약칭입니다.

COSN 빅 데이터 모듈은 다음 시나리오를 지원합니다.

| 모듈 이름 | COSN 빅 데이터 모듈이 지원하는 시나리오 | 서비스 모듈 재시작 필요 여부                         |
| -------- | ----------------------- | -------------------------------------------- |
| Yarn     | 지원                    | NodeManager 재시작                             |
| Yarn     | 지원                    | NodeManager 재시작                             |
| Hive     | 지원                    | HiveServer, HiveMetastore 재시작             |
| Spark    | 지원                    | NodeManager 재시작                             |
| Sqoop    | 지원                    | NodeManager 재시작                             |
| Presto   | 지원                    | HiveServer, HiveMetastore, Presto 재시작 |
| Flink    | 지원                    | 필요 없음                                           |
| Impala   | 지원하지 않음                  | 필요 없음                                           |
| HBase    | 권장하지 않음                  | 필요 없음                                           |


## 버전 종속

본 문서에서 종속된 모듈 버전은 다음과 같습니다.

- CDH 5.16.1
- Hadoop 2.6.0


## 사용 방법

### 스토리지 환경 설정

1. CDH 관리 페이지에 로그인합니다.
2. 시스템 홈페이지에서 **설정** > **서비스 범위** > **고급**을 선택하여 코드 대역 고급 설정 페이지로 이동하면 아래 그림과 같이 표시됩니다.
   ![](https://main.qcloudimg.com/raw/ee096f8e123efd393e1c8a610dd06ff2.png)
3. Cluster-wide Advanced Configuration Snippet(Safety Valve) for core-site.xml 코드 박스에 COSN 설정을 입력합니다.

```
<property>
<name>fs.cosn.userinfo.secretId</name>
<value>AK***</value>
</property>
<property>
<name>fs.cosn.userinfo.secretKey</name>
<value></value>
</property>
<property>
<name>fs.cosn.impl</name>
<value>org.apache.hadoop.fs.CosFileSystem</value>
</property>
<property>
<name>fs.AbstractFileSystem.cosn.impl</name>
<value>org.apache.hadoop.fs.CosN</value>
</property>
<property>
<name>fs.cosn.bucket.region</name>
<value>ap-shanghai</value>
</property>
```

다음은 COSN의 필수 설정 페이지(core-site.xml에 추가 필요)이며 COSN의 기타 설정 사항은 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884) 문서를 참조하십시오.

| COSN 설정 페이지                     | 값                                 | 의미                                                         |
| ------------------------------- | ---------------------------------- | ------------------------------------------------------------ |
| fs.cosn.userinfo.secretId       | AKxxxx                             | 계정 API 키 정보                                          |
| fs.cosn.userinfo.secretKey      | Wpxxxx                             | 계정 API 키 정보                                          |
| fs.cosn.bucket.region           | ap-shanghai                        | 사용자 버킷이 속한 리전                                           |
| fs.cosn.impl                    | org.apache.hadoop.fs.CosFileSystem | FileSystem에 대한 cosn 구현 클래스, org.apache.hadoop.fs.CosFileSystem로 고정 |
| fs.AbstractFileSystem.cosn.impl | org.apache.hadoop.fs.CosN          | AbstractFileSystem에 대한 cosn 구현 클래스, org.apache.hadoop.fs.Cosn으로 고정 |

4. HDFS 서비스 작업을 진행하기 위해 클라이언트 배포 설정을 클릭하면 core-site.xml 설정이 클러스터 기기에 업데이트됩니다.
5. COSN의 최신 SDK 패키지를 CDH HDFS 서비스의 jar 패키지 경로에 설치합니다. 실제 값에 따라 바뀌며 다음 예시처럼 보여집니다.

```
cp hadoop-cos-2.7.3-shaded.jar /opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/hadoop-hdfs/
```

>! 클러스터의 기기마다 동일한 위치에 SDK 패키지 설치가 필요합니다.


<span id=1>

### 데이터 마이그레이션

Hadoop Distcp 툴을 이용해 CDH HDFS를 COSN에 데이터 마이그레이션합니다. 자세한 내용은 [Hadoop 파일 시스템과 COS 간의 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/436/34076)을 참조하십시오.

### 빅 데이터 패키지의 COSN 사용하기

#### 1. MapReduce

**작업 순서**

(1) [데이터 마이그레이션](#1) 절에 따라 HDFS 관련 설정을 하고 COSN SDK jar 패키지를 HDFS에 상응하는 디렉터리에 설치합니다.
(2) CDH 시스템 홈페이지에서 YARN을 찾아 NodeManager 서비스를 재시작하십시오. TeraGen 명령어는 재시작할 필요가 없지만 TeraSort는 비즈니스 내부 로직으로 인해 NodeManger를 재시작해야 하므로 일괄적으로 NodeManager 서비스를 재시작하기를 권고합니다.

**예시**

다음은 Hadoop을 기준으로 테스트 중인 TeraGen과 TeraSort의 예시입니다.

```
hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar teragen  -Dmapred.job.maps=500  -Dfs.cosn.upload.buffer=mapped_disk -Dfs.cosn.upload.buffer.size=-1 1099 cosn://examplebucket-1250000000/terasortv1/1k-input

hadoop jar ./hadoop-mapreduce-examples-2.7.3.jar terasort -Dmapred.max.split.size=134217728 -Dmapred.min.split.size=134217728 -Dfs.cosn.read.ahead.block.size=4194304 -Dfs.cosn.read.ahead.queue.size=32 cosn://examplebucket-1250000000/terasortv1/1k-input  cosn://examplebucket-1250000000/terasortv1/1k-output
```

>?`cosn://    schema` 뒤를 사용자 빅 데이터 비즈니스 버킷 경로로 바꾸십시오.

#### 2. Hive

##### 2.1 MR 엔진

**작업 순서**

(1) [데이터 마이그레이션](#1) 절에 따라 HDFS 관련 설정을 하고 COSN SDK jar 패키지를 HDFS에 상응하는 디렉터리에 설치합니다.
(2) CDH 홈페이지에서 HIVE 서비스를 찾아 Hiveserver2와 HiverMetastore 역할을 재시작하십시오.

**예시**

사용자의 실제 비즈니스를 조회하는 경우 Hive 명령 라인을 실행하여 CHDFS 파티션 테이블로 사용되는 Location을 생성합니다.

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

sql 쿼리를 실행합니다.

```
select count(1) from report.report_o2o_pid_credit_detail_grant_daily;
```

모니터링 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/28a566e5f08d7cbbeb4893b851565c01.png)

##### 2.2 Tez 엔진

Tez 엔진은 COSN jar 패키지를 Tez의 압축 패키지로 가져와야 합니다. 다음은 apache-tez.0.8.5을 예시로 한 설명입니다.

**작업 순서**

(1) CDH 클러스터에 설치한 tez 패키지를 찾은 후 압축을 해제합니다. /usr/local/service/tez/tez-0.8.5.tar.gz를 예로 들 수 있습니다.
(2) COSN jar 패키지를 압축 해제한 디렉터리로 가져온 후 다시 압축하여 압축 패키지로 내보냅니다.
(3) 새로 압축한 패키지를 tez.lib.uris로 지정한 경로에 업로드합니다(이전 경로가 존재하는 경우 변경할 수 있습니다).
(4) CDH 홈페이지에서 HIVE를 찾아 hiveserver와 hivemetastore를 재시작합니다.

#### 3. Spark

**작업 순서**

(1) [데이터 마이그레이션](#1) 절에 따라 HDFS 관련 설정을 하고 COSN SDK jar 패키지를 HDFS에 상응하는 디렉터리에 설치합니다.
(2) NodeManager 서비스를 재시작합니다.

**예시**

COSN으로 진행하는 Spark example word count 테스트 예시입니다.

```
spark-submit  --class org.apache.spark.examples.JavaWordCount --executor-memory 4g --executor-cores 4  ./spark-examples-1.6.0-cdh5.16.1-hadoop2.6.0-cdh5.16.1.jar cosn://examplebucket-1250000000/wordcount
```

실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/90e847c279f948af89ac670e43cd0b31.png)


#### 4. Sqoop

**작업 순서**

(1) [데이터 마이그레이션](#1) 절에 따라 HDFS 관련 설정을 하고 COSN SDK jar 패키지를 HDFS에 상응하는 디렉터리에 설치합니다.

(2) COSN SDK jar 패키지는 sqoop 디렉터리에 있어야 합니다(/opt/cloudera/parcels/CDH-5.16.1-1.cdh5.16.1.p0.3/lib/sqoop/를 예시로 들 수 있습니다).

(3) NodeManager 서비스를 재시작합니다.

**예시**

MYSQL 테이블을 COSN에 내보내는 경우 [관계형 데이터베이스와 HDFS 가져오기 및 내보내기](https://intl.cloud.tencent.com/document/product/1026/31157) 문서를 참조하여 테스트를 진행하십시오.

```
sqoop import --connect "jdbc:mysql://IP:PORT/mysql" --table sqoop_test --username root --password 123**  --target-dir cosn://examplebucket-1250000000/sqoop_test
```

실행 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/4164c207304ba75eb8be42045f7f1394.png)


#### 5. Presto

**작업 순서**

(1) [데이터 마이그레이션](#1) 절에 따라 HDFS 관련 설정을 하고 COSN SDK jar 패키지를 HDFS에 상응하는 디렉터리에 설치합니다.
(2) COSN SDK jar 패키지는 presto 디렉터리에 속해야 합니다(예시, /usr/local/services/cos_presto/plugin/hive-hadoop2).
(3) presto가 hadoop common의 gson-2.*.*.jar에 로딩하지 못하므로 gson-2.*.*.jar는 presto 디렉터리에 속해야 합니다(/usr/local/services/cos_presto/plugin/hive-hadoop2를 예시로 들 수 있으며 CHDFS는 gson에 종속됩니다).
(4) HiveServer, HiveMetaStore, Presto 서비스를 재시작합니다.

**예시**

HIVE로 Location을 생성한 COSN 테이블을 조회하는 예시입니다.

```
select * from cosn_test_table where bucket is not null limit 1;
```

>?cosn_test_table은 cosn scheme이 location인 테이블입니다.

조회 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/b83d2aaf490edebbe3d9cc936c5bcce3.png)

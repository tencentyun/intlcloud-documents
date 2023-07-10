## 개요

[CosN 툴](https://intl.cloud.tencent.com/document/product/436/6884)은 Tencent Cloud COS(Cloud Object Storage)가 제공하는 표준 Hadoop 파일 시스템을 기반으로 구현되었으며, Hadoop, Spark 및 Tez와 같은 빅 데이터 컴퓨팅 프레임워크를 COS에 통합하는 기능을 지원합니다. 사용자는 Hadoop 파일 시스템 인터페이스의 CosN 플러그인을 사용하여 COS에 저장된 데이터를 읽고 쓸 수 있습니다. CosN 툴을 사용하여 COS에 액세스하는 기존 사용자를 위해 GooseFS는 클라이언트 경로 매핑 방법을 제공하여 사용자가 현재 Hive table 정의를 수정하지 않고도 CosN scheme을 사용하여 GooseFS에 액세스할 수 있도록 합니다. 해당 특성은 사용자로 하여금 기존 테이블 정의를 수정하지 않는 전제 하에 편리하게 GooseFS의 기능과 성능을 비교 테스트 할 수 있도록 합니다.

CosN Schema와 GooseFS Schema의 매핑 설명은 아래와 같습니다.

만약 Namespace warehouse 에 상응하는 UFS 경로가 `cosn://examplebucket-1250000000/data/warehouse/`라면，CosN에서 GooseFS의 경로 매핑 관계는 다음과 같습니다.
```plaintext
cosn://examplebucket-1250000000/data/warehouse -> /warehouse/
cosn://examplebucket-1250000000/data/warehouse/folder/test.txt ->/warehouse/folder/test.txt
```
GooseFS에서 CosN의 경로 매핑 관계는 다음과 같습니다.
```plaintext
/warehouse ->cosn://examplebucket-1250000000/data/warehouse/
/warehouse/ -> cosn://examplebucket-1250000000/data/warehouse/
/warehouse/folder/test.txt -> cosn://examplebucket-1250000000/data/warehouse/folder/test.txt
```
 
CosN Scheme은 GooseFS 기능에 액세스하여, 클라이언트 측에서 GooseFS 경로와 기본 파일 시스템의 CosN 경로 간의 매핑 관계를 유지하고, CosN 경로의 요청을 GooseFS의 요청으로 변환합니다. 매핑 관계는 주기적으로 갱신되며, GooseFS 설정 파일 goosefs-site.properties 중의 설정 항목 goosefs.client.namespace.refresh.interval을 수정하여 갱신 주기를 조정할 수 있으며, 기본값은 60초입니다.

>! 액세스한 CosN 경로를 GooseFS 경로로 변환할 수 없는 경우, 해당 Hadoop API 호출에서 이상 경고가 발생합니다.
>

## 작업 예시

해당 예시에서는 Hadoop 명령 라인 및 Hive에서 Schema gfs:// 및 Schema cosn://을 사용하여 GooseFS에 액세스하는 방법을 보여줍니다. 작업 과정은 다음과 같습니다.

### 1. 데이터 및 컴퓨팅 클러스터 준비

- [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하여 테스트용 버킷을 생성 합니다.
- [폴더 생성](https://intl.cloud.tencent.com/document/product/436/13329) 문서를 참고하여 버킷의 루트 경로 아래에 ml-100k라는 폴더를 생성합니다.
- [Grouplens](https://grouplens.org/datasets/movielens/100k/)에서 ml-100k 데이터 세트를 다운로드하고 u.user 파일을 `<버킷 루트 경로>/ml-100k`에 업로드합니다.
- EMR 가이드 문서를 참고하여 하나의 EMR 클러스터를 구매하고 HIVE 컴포넌트를 설정하십시오.

### 2. 환경 설정

i. GooseFS 클라이언트측 jar 패키지(goosefs-1.0.0-client.jar)를 share/hadoop/common/lib/ 디렉터리에 넣습니다.
```plaintext
 cp goosefs-1.0.0-client.jar  hadoop/share/hadoop/common/lib/
```
 >! 설정 변경 및 jar 패키지 추가는 클러스터의 모든 노드에 동기화되어야 합니다.
 >
ii. Hadoop 구성 파일 etc/ hadoop/ core-site.xml을 수정합니다. GooseFS의 구현 클래스를 지정합니다.
```plaintext
<property>
  <name>fs.AbstractFileSystem.gfs.impl</name>
  <value>com.qcloud.cos.goosefs.hadoop.GooseFileSystem</value>
</property>
<property>
  <name>fs.gfs.impl</name>
  <value>com.qcloud.cos.goosefs.hadoop.FileSystem</value>
</property>
```
iii. 다음 Hadoop 명령어를 실행하여 gfs:// Scheme을 통해 GooseFS에 액세스할 수 있는지 확인합니다. 여기서 &lt;MASTER_IP>는 Master 노드의 IP입니다.
```plaintext
hadoop fs -ls gfs://<MASTER_IP>:9200/
```
iv. Hive가 GooseFS Client 패키지에 로딩될 수 있도록, GooseFS의 클라이언트측 jar 패키지를 Hive의 auxlib 디렉터리에 넣습니다.
```plaintext
cp goosefs-1.0.0-client.jar  hive/auxlib/
```
v. 다음 명령을 실행하여 UFS Scheme이 CosN인 Namespace를 생성하고 Namespace를 나열합니다. 이 명령어의 examplebucket-1250000000을 사용자의 COS 버킷으로 바꾸고 SecretId와 SecretKey를 사용자의 키 정보로 바꿀 수 있습니다.
```plaintext
goosefs ns create ml-100k cosn://examplebucket-1250000000/ml-100k  --secret fs.cosn.userinfo.secretId=SecretId --secret fs.cosn.userinfo.secretKey=SecretKey--attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.credentials.provider=org.apache.hadoop.fs.auth.SimpleCredentialProvider
goosefs ns ls
```

### 3. GooseFS Schema 테이블 생성 및 데이터 조회

아래 명령을 통해 실행합니다.

```plaintext
create database goosefs_test;

use goosefs_test;
CREATE TABLE u_user_gfs (
userid INT,
age INT,
gender CHAR(1),
occupation STRING,
zipcode STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE
LOCATION 'gfs://<MASTER_IP>:<MASTER_PORT>/ml-100k';

select sum(age) from u_user_gfs;
```


### 4. CosN Schema 테이블 생성 및 데이터 조회

아래 명령을 통해 실행합니다.

```plaintext
CREATE TABLE u_user_cosn (
userid INT,
age INT,
gender CHAR(1),
occupation STRING,
zipcode STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '|'
STORED AS TEXTFILE
LOCATION 'cosn://examplebucket-1250000000/ml-100k';

select sum(age) from u_user_cosn;
```

### 5. CosN을 수정하여 GooseFS 호환 구현

hadoop/etc/hadoop/core-site.xml 수정

```plaintext
 <property>
        <name>fs.AbstractFileSystem.cosn.impl</name>
        <value>com.qcloud.cos.goosefs.hadoop.CosN</value>
    </property>
    <property>
        <name>fs.cosn.impl</name>
        <value>com.qcloud.cos.goosefs.hadoop.CosNFileSystem</value>
    </property>
```

Hadoop 명령어를 실행합니다. 경로를 GooseFS의 경로로 변환할 수 없는 경우 명령 출력에 오류 메시지가 포함됩니다.

```plaintext
hadoop fs -ls  cosn://examplebucket-1250000000/ml-100k/

Found 1 items
-rw-rw-rw-   0 hadoop hadoop      22628 2021-07-02 15:27 cosn://examplebucket-1250000000/ml-100k/u.user
 
hadoop fs -ls cosn://examplebucket-1250000000/unknow-path
ls: Failed to convert ufs path cosn://examplebucket-1250000000/unknow-path to GooseFs path, check if namespace mounted 
```

다시 Hive를 실행하여 구문 조회.

```plaintext
select sum(age) from u_user_cosn;
```


본 문서는 주로 GooseFS 빠른 배포, 디버깅 관련 가이드를 제공합니다. 또한 로컬 기기에 GooseFS를 배포하고 COS를 원격 스토리지로 만드는 가이드를 제공합니다. 자세한 순서는 다음과 같습니다.


## 전제 조건

 GooseFS 사용 전 다음 작업을 준비해야 합니다.

1. COS 서비스에 버킷을 생성해 원격 스토리지로 만듭니다. 작업 가이드에 대한 자세한 내용은 [COS 시작하기](https://intl.cloud.tencent.com/document/product/436/32955)를 참조하십시오.
2. [Java 8 버전 이상](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)을 설치하십시오.
3. SSH를 통한 LocalHost 연결과 원격 로그인이 가능하도록 [SSH](https://www.ssh.com/ssh/)을 설치하십시오.

## GooseFS 다운로드 및 설정

1. 공식 홈페이지 라이브러리에서 GooseFS 설치 패키지를 로컬에 다운로드합니다.
2. 다음 명령어에 따라 설치 패키지의 압축을 해제합니다.
```plaintext
tar -zxvf goosefs-1.0.0-bin.tar.gz
cd goosefs-1.0.0
```
3. 압축 해제 후, GooseFS 설치 패키지의 소스 파일과 Java 바이너리 파일 모두 goosefs-1.0.0 폴더에 저장됩니다. 본 가이드는 `${GOOSEFS_HOME}`을 참조합니다.
4. `${GOOSEFS_HOME}/conf`의 디렉터리에 `conf/goosefs-site.properties`의 구성 파일을 생성하여 내장된 구성 템플릿을 사용할 수 있습니다.
```plaintext
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
5. 구성 파일 `conf/goosefs-site.properties`에서 goosefs.master.hostname을 `localhost`로 설정합니다.
```plaintext
$ echo"goosefs.master.hostname=localhost">> conf/goosefs-site.properties
```

## GooseFS 활성화 

1. GooseFS 활성화 전 GooseFS가 로컬 환경에서 정확히 실행될 수 있도록 시스템 환경 검사를 진행합니다.
```plaintext
$ goosefs validateEnv local
```
 >? 해당 명령어를 사용하여 GooseFS의 실행 상황을 조회합니다.
 >
2. GooseFS 활성화 전 GooseFS의 포맷화를 진행하여, 해당 명령어가 GooseFS의 로그와 `worker` 스토리지 디렉터리의 내용을 삭제합니다.
```plaintext
$ goosefs format
```
3. 다음 명령어를 사용하여 GooseFS를 활성화할 수 있으며, 시스템 기본 설정에서 GooseFS가 Master와 Worker를 하나씩 실행합니다.
```plaintext
$ ./bin/goosefs-start.sh local SudoMount
```
해당 명령어 실행을 완료한 후 http://localhost:9201과 http://localhost:9204에 액세스하여 Master와 Worker의 실행 상태를 각각 조회할 수 있습니다.

## GooseFS를 사용하여 COS 마운트
1. Namespace를 생성하여 COS를 마운트합니다.

```plaintext
$ goosefs ns create myNamespace cosn://bucketName-125xxxxxx/ 3TB
--option fs.cosn.userinfo.secretId=AKIDxxxxxxxxxxxxxx \
--option fs.cosn.userinfo.secretKey=xxxxxxxxxxxxxxxxx \
--option fs.cosn.bucket.region=ap-guangzhou \
```

>! Namespace 생성 시 반드시 –-option 매개변수와 Hadoop-COS(COSN)의 모든 필수 매개변수를 지정해야 합니다. 필수 매개변수에 대한 자세한 내용은 [Hadoop 툴](https://intl.cloud.tencent.com/document/product/436/6884)을 참조하십시오. Namespace 생성 시 읽기/쓰기 정책(rPolicy/wPolicy)을 지정하지 않은 경우, 구성 파일에서 지정한 read/write type이나 기본값(CACHE/CACHE_THROUGH)을 사용합니다.
>
2. 다음 명령어와 같이, 마운트 성공 후 ls 명령어를 통해 클러스터에서 생성한 모든 namespace를 열거할 수 있습니다.
```plaintext
$ goosefs ns list
namespace	      mountPoint	       ufsPath                     	 creationTime                wPolicy      	rPolicy	     TTL	   ttlAction
myNamespace    /myNamespace   cosn://bucketName-125xxxxxx/3TB  03-11-2021 11:43:06:239      CACHE_THROUGH   CACHE        -1      DELETE
```
3. 지정한 namespace의 세부 정보만 이해하려면 다음 명령어를 통해 구현할 수 있습니다.
```plaintext
$ goosefs ns stat myNamespace

NamespaceStatus{name=myNamespace, path=/myNamespace, ttlTime=-1, ttlAction=DELETE, ufsPath=cosn://bucketName-125xxxxxx/3TB, creationTimeMs=1615434186076, lastModificationTimeMs=1615436308143, lastAccessTimeMs=1615436308143, persistenceState=PERSISTED, mountPoint=true, mountId=4948824396519771065, acl=user::rwx,group::rwx,other::rwx, defaultAcl=, owner=user1, group=user1, mode=511, writePolicy=CACHE_THROUGH, readPolicy=CACHE}
```

메타데이터에서 기록한 정보에는 다음과 같은 내용이 포함됩니다.

| 번호 | 매개변수                   | 설명 |
| ---- | ---------------------- | ----- |
| 1    | name                   | namespace 이름 |
| 2    | path                   | GooseFS에서 namespace의 경로 |
| 3    | ttlTime                | namespace 디렉터리와 파일의 ttl 주기 |
| 4    | ttlAction              | namespace 디렉터리와 파일의 ttl 처리 작업에는 FREE와 DELETE 두 가지 처리 작업이 있습니다. 기본값: FREE |
| 5    | ufsPath                | ufs에서 namespace의 마운트 경로 |
| 6    | creationTimeMs         | namespace 생성 시간. 단위: 밀리초 |
| 7    | lastModificationTimeMs | namespace 디렉터리와 파일의 최종 수정 시간. 단위: 밀리초 |
| 8    | persistenceState       | namespace의 지속 상태 |
| 9    | mountPoint             | namespace의 마운트 포인트가 하나인지 여부. 값은 항상 true |
| 10   | mountId                | namespace 마운트 포인트 id |
| 11   | acl                    | namespace의 액세스 제어 리스트 |
| 12   | defaultAcl             | namespace의 기본 액세스 제어 리스트 |
| 13   | owner                  | namespace의 owner |
| 14   | group                  | namespace의 owner가 속한 group |
| 15   | mode                   | namespace의 POSIX 권한 |
| 16   | writePolicy            | namespace의 쓰기 정책 |
| 17   | readPolicy             | namespace의 읽기 정책 |


## GooseFS를 사용하여 Table 데이터 프리패치

1. GooseFS는 Hive Table의 데이터를 GooseFS로 프리패치할 수 있습니다. 프리패치 전에 관련 DB를 GooseFS에 연결해야 하며, 관련 명령어는 다음과 같습니다.

```plaintext
$ goosefs table attachdb --db test_db hive thrift://
172.16.16.22:7004 test_for_demo
```

>! 명령어의 thrift는 실제 Hive Metastore 주소를 입력해야 합니다.
>
2. DB 추가 후 ls 명령어를 통해 현재 연결 중인 DB와 Table 정보를 조회할 수 있습니다.
```plaintext
$ goosefs table ls test_db web_page

OWNER: hadoop
DBNAME.TABLENAME: testdb.web_page (
   wp_web_page_sk bigint,
   wp_web_page_id string,
   wp_rec_start_date string,
   wp_rec_end_date string,
   wp_creation_date_sk bigint,
   wp_access_date_sk bigint,
   wp_autogen_flag string,
   wp_customer_sk bigint,
   wp_url string,
   wp_type string,
   wp_char_count int,
   wp_link_count int,
   wp_image_count int,
   wp_max_ad_count int,
)
PARTITIONED BY (
)
LOCATION (
   gfs://172.16.16.22:9200/myNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://172.16.16.22:9200/myNamespace/3000/web_page
   }
)
```
3. load 명령어를 통해 Table 데이터를 프리패치합니다.
```plaintext
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```

Table 데이터 프리패치는 비동기 작업으로 작업 ID 하나를 반환합니다. goosefs job stat &lt;Job Id> 명령어를 통해 프리패치 작업의 진행률을 조회할 수 있습니다. "COMPLETED" 상태가 되면 전체 프리패치 과정이 완료되었음을 의미합니다.

## GooseFS를 사용하여 파일 업로드와 다운로드 작업 실행

1. GooseFS는 대부분의 파일 시스템 작업 명령어를 지원하며, 다음 명령어를 통해 현재 지원하는 명령어 리스트를 조회할 수 있습니다.
```plaintext
$ goosefs fs
```
2. `ls` 명령어를 통해 GooseFS 파일을 열거합니다. 다음 예시에서 어떻게 루트 디렉터리의 모든 파일을 열거하는지 확인하십시오.
```plaintext
$ goosefs fs ls /
```
3. `copyFromLocal` 명령어를 통해 데이터를 로컬에서 GooseFS로 복사할 수 있습니다.

```plaintext
$ goosefs fs copyFromLocal LICENSE /LICENSE
Copied LICENSE to /LICENSE
$ goosefs fs ls /LICENSE
-rw-r--r--  hadoop         supergroup               20798       NOT_PERSISTED 03-26-2021 16:49:37:215   0% /LICENSE
```

4. `cat` 명령어를 통해 파일 내용을 조회할 수 있습니다.
```plaintext
$ goosefs fs cat /LICENSE                                                                         
Apache License
Version 2.0, January 2004
http://www.apache.org/licenses/
TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION
...
```
5. GooseFS는 로컬 디스크를 하부 시스템으로 사용하며, 기본 시스템 경로는 `./underFSStorage`입니다. `persist` 명령어를 통해 로컬 파일 시스템에 파일을 지속 저장할 수 있습니다.
```plaintext
$ goosefs fs persist /LICENSE
persisted file /LICENSE with size 26847
```

## GooseFS를 사용하여 신속하게 파일 업로드/다운로드

1. CFS 상태를 검사하여 파일이 캐시되었는지 확인합니다. 파일 상태가 `PERSISTED`인 경우 파일이 메모리에 저장된 것을 의미하며, 파일 상태가 `NOT_PERSISTED`인 경우 파일이 메모리에 없음을 의미합니다.

```plaintext
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 NOT_PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
```

2. 파일에 단어 'tencent'가 몇 개 있는지 통계를 낸 후 작업 소요 시간을 계산합니다.

```plaintext
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m22.857s
user	0m7.557s
sys	0m1.181s
```

3. 해당 데이터 캐시를 메모리에 저장하여 조회 속도를 효과적으로 향상시킬 수 있습니다. 자세한 예시는 다음과 같습니다.

```plaintext
$ goosefs fs ls /data/cos/sample_tweets_150m.csv
-r-x------ staff  staff 157046046 PERSISTED 01-09-2018 16:35:01:002   0% /data/cos/sample_tweets_150m.csv
$ time goosefs fs cat /data/s3/sample_tweets_150m.csv | grep-c kitten
889
real	0m1.917s
user	0m2.306s
sys	    0m0.243s
```

시스템 프로세스 딜레이가 1.181s에서 0.243s로 감소되어 10배 향상된 것을 알 수 있습니다.

## GooseFS 비활성화

다음과 같은 명령어를 통해 GooseFS를 비활성화할 수 있습니다.

```plaintext
$ ./bin/goosefs-stop.sh local
```


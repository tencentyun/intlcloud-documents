## Table 관리 기능 개요

GooseFS Table 관리 능력을 통해 구조화 데이터를 관리합니다. SparkSQL, Hive, Presto 등 상위 컴퓨팅 애플리케이션에게 데이터베이스 테이블 관리 능력을 제공하고, 현재 Hive MetaStore 연결을 기본 지원합니다. Table 관리 능력은 각종 SQL 엔진이 지정한 데이터 내용을 읽게 하여 효과적으로 빅 데이터 시나리오에서 데이터의 액세스 효율을 높입니다. 

![](https://main.qcloudimg.com/raw/c3616ae043e36bc5ea462fa960e20fbb.png)          

GooseFS Table 관리 능력은 아래 특성을 지원합니다. 

- 메타데이터 레이어의 기술 능력. GooseFS Catalog는 원격 메타데이터 서비스 (Hive MetaStore)의 메타데이터 캐시 서비스를 제공하며, SparkSQL, Hive, SQL Presto 등 SQL 엔진을 쿼리할 때, GooseFS Catalog의 메타데이터 캐시 서비스에 따라, 읽어오는 데이터의 크기, 타깃 데이터의 위치 및 데이터 구조를 확인할 수 있으며, Hive MetaStore와 동일한 능력을 갖고 있습니다. 
- 테이블 레벨 데이터 프리캐싱 능력. GooseFS Catalog는 데이터 테이블과 데이터 스토리지 경로의 대응 관계를 감지할 수 있어 Table 레벨 및 Table Partition 레벨의 캐시 프리패치 능력을 제공하고, 사용자가 사전에 테이블 구조에 따라 데이터를 캐시하여 액세스 성능을 대폭 향상 시킵니다. 
- 크로스 스토리지의 통합 메타데이터 서비스. GooseFS Catalog를 통해 상위 컴퓨팅 애플리케이션을 실행하면 각각 다른 기본 스토리지 시스템에 액세스 가속 능력을 동시에 제공할 수 있습니다. GooseFS Catalog는 스토리지 서비스간의 통합 메타데이터 쿼리 능력을 제공하여 하나의 GooseFS 클라이언트가 Catalog 기능을 활성화하기만 하면 각각 다른 스토리지 시스템을 확인할 수 있습니다. 예: HDFS, COS, CHDFS의 데이터. 

## GooseFS Table 의 관리 기능 사용

GooseFS Table 관리 기능은 goosefs table 명령어 집합을 통해 구현되며, DB의 바인딩과 바인딩 해제, DB 정보 조회, 테이블 정보 조회, 데이터 로딩, 데이터 제거 등 기능을 제공합니다. GooseFS Table 관리 명령어 집합은 아래와 같습니다.

```plaintext
$ goosefs table
Usage: goosefs table [generic options]
	 [attachdb [-o|--option <key=value>] [--db <goosefs db name>] [--ignore-sync-errors] <udb type> <udb connection uri> <udb db name>]
	 [detachdb <db name>]                                      
	 [free <dbName> <tableName> [-p|--partition <partitionSpec>]]
	 [load <dbName> <tableName> [-g|--greedy] [--replication <num>] [-p|--partition <partitionSpec>]]
	 [ls [<db name> [<table name>]]]                           
	 [stat <dbName> <tableName>]                               
	 [sync <db name>]                                          
```

상기 명령어 집합의 각 명령어의 기능 설명은 아래와 같습니다. 

- attachdb: 데이터베이스 마운트. 하나의 원격 데이터베이스를 GooseFS에 바인딩하며 현재 Hive MetaStore만 지원합니다. 
- detachdb: 데이터베이스 언마운트. GooseFS에 바인딩된 데이터베이스의 바인딩을 해제합니다. 
- free: 지정 DB.Table의 데이터 캐시 삭제. Partition 세분성을 지원합니다. 
- load: 지정 DB.Table의 데이터 캐시. partition 세분성을 지원하며 replication을 통한 캐시의 복사본 수량 설정을 지원합니다. 
- 1s: 지정 DB 혹은 DB.Table의 메타데이터 정보를 나열합니다. 
- stat: 지정 DB.Table의 파일 수량, 크기, 캐시 백분율을 조회합니다. 
- sync: 지정 DB의 내용을 동기화합니다. 
- transform: 지정 DB에 연결된 Table을 새로운 Table로 전환합니다. 
- transformStatus: Table 전환의 진행 상황을 확인합니다. 

### 1. DB 마운트

지정 Table 데이터를 GooseFS 이전으로 프리패치하며 해당하는 DB를 GooseFS에 마운트해야 합니다. 아래 예시는 지정 주소 metastore_host:port의 데이터베이스 goosefs_db_demo를 GooseFS에 마운트 하고, GooseFS 내 해당 DB 이름을 test_db로 설정하는 것을 설명합니다.

```plaintext
$ goosefs table attachdb --db test_db hive thrift://metastore_host:port goosefs_db_demo

response of attachdb
```

>! metastore_host:port는 연결 가능한 임의의 합법 Hive MetaStore 주소로 변경할 수 있습니다. 
>

### 2. Table 정보 확인

데이터베이스 바인딩 후 ls 명령어를 통해 마운트된 DB와 Table 정보를 확인할 수 있습니다. 아래 예시는 test_db의 web_page 테이블 정보를 확인하는 방법을 설명합니다. 

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
   gfs://metastore_host:port/myiNamespace/3000/web_page
)
PARTITION LIST (
   {
   partitionName: web_page
   location: gfs://metastore_host:port/myNamespace/3000/web_page
   }
)
```


### 3. Table의 데이터 프리패치

Table 프리패치 명령어 전달 후 백그라운드에서 비동기화 작업을 전달하고, GooseFS는 작업 실행 후 하나의 작업 ID를 반환합니다. ‘job stat <ID>’ 명령어를 통해 작업의 실행 상태를 확인할 수 있으며 ‘table stat’ 명령어를 통해 프리패치의 백분율을 확인할 수 있습니다. 프리패치 명령어는 아래와 같습니다. 

```plaintext
$ goosefs table load test_db web_page
Asynchronous job submitted successfully, jobId: 1615966078836
```


### 4. Table 프리패치 상황 확인

‘job stat’ 명령어를 통해 Table 프리패치 작업의 진행률을 확인할 수 있습니다. COMPLETED 상태가 되면, 전체 프리패치 프로세스가 완료된 것이며, FAILED 상태일 경우  master.log 파일에서 로그 기록을 확인하여 프리패치 오류 원인을 진단할 수 있습니다. 

```plaintext
$ goosefs job stat 1615966078836
COMPLETED
```

Table 프리패치 완료 후 stat 명령어를 통해 지정 Table의 현황을 확인할 수 있습니다.

```plaintext
$ goosefs table stat test_db web_page
detail
```


### 5. Table 릴리스

아래 명령어를 통해 GooseFS에서 지정 Table 데이터 캐시를 릴리스할 수 있습니다. 

```plaintext
$ goosefs table ls test_db web_page
detail
```


### 6. DB 언마운트

아래 명령어를 통해 GooseFS에서 지정 DB를 언마운트 할 수 있습니다. 

```plaintext
$ goosefs table detachdb test_db
detail
```

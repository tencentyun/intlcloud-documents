## Oceanus 개요  

Oceanus는 빅 데이터 생태계의 강력한 실시간 분석 도구입니다. 이를 통해 웹사이트 클릭스트림 분석, 이커머스 정밀 타켓팅 추천, IoT 등 다양한 애플리케이션을 단 몇 분 만에 쉽게 구축할 수 있습니다. Oceanus는 Apache Flink를 기반으로 개발되었으며 완전 관리형 클라우드 서비스를 제공하므로 인프라의 Ops에 대해 걱정할 필요가 없습니다. 또한 클라우드의 데이터 소스에 연결하여 완전한 지원 서비스를 받을 수 있습니다.

Oceanus는 SQL 분석 문을 작성하고, 사용자 정의 JAR 패키지를 업로드 및 실행하고, 작업을 관리할 수 있는 편리한 콘솔과 함께 제공됩니다. Flink 기술을 기반으로 PB 수준의 데이터 세트에서 1초 미만의 처리 대기 시간을 달성할 수 있습니다.

이 문서에서는 Oceanus를 COS에 연결하는 방법에 대해 설명합니다. 현재 Oceanus는 전용 클러스터 모드에서 사용할 수 있으며, 여기에서 다양한 작업을 실행하고 자신의 클러스터에서 관련 리소스를 관리할 수 있습니다.

## 준비 작업

#### Oceanus 클러스터 생성

[Oceanus 콘솔](https://console.cloud.tencent.com/oceanus/workspace)에 로그인하여 Oceanus 클러스터를 생성합니다.

#### COS 버킷 생성

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. **버킷 생성**을 클릭하여 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)의 안내에 따라 버킷을 생성합니다.
>? COS에 데이터를 쓸 때 Oceanus 작업은 COS와 동일한 리전에서 실행되어야 합니다.
>

## 실행 순서

[Oceanus 콘솔](https://console.cloud.tencent.com/oceanus/overview)로 이동하여 SQL 작업을 생성하고 COS와 동일한 리전의 클러스터를 선택합니다.

#### 1. Source 생성

```sql
CREATE TABLE `random_source` ( 
  f_sequence INT, 
  f_random INT, 
  f_random_str VARCHAR 
  ) WITH ( 
  'connector' = 'datagen', 
  'rows-per-second'='10',                  -- 초당 생성된 데이터 행 수
  'fields.f_sequence.kind'='random',       -- 랜덤 숫자
  'fields.f_sequence.min'='1',             -- 최소 순차 번호
  'fields.f_sequence.max'='10',            -- 최대 순차 번호
  'fields.f_random.kind'='random',         -- 랜덤 숫자
  'fields.f_random.min'='1',               -- 최소 랜덤 숫자
  'fields.f_random.max'='100',             -- 최대 랜덤 숫자
  'fields.f_random_str.length'='10'        -- 랜덤 문자열 길이
);
```

>? 여기서는 내장 connector 'datagen'이 선택되었습니다. 실제 비즈니스 요구 사항에 따라 데이터 소스를 선택하십시오.
>

#### 2. Sink 생성

```sql
-- <bucket name> 및 <folder name>을 실제 버킷 및 폴더 이름으로 바꿉니다.
CREATE TABLE `cos_sink` (
  f_sequence INT, 
  f_random INT, 
  f_random_str VARCHAR
) PARTITIONED BY (f_sequence) WITH (
    'connector' = 'filesystem',
    'path'='cosn://<bucket name>/<folder name>/',                 --- 데이터가 기록될 디렉터리 경로
    'format' = 'json',                                       --- 기록된 데이터의 형식
    'sink.rolling-policy.file-size' = '128MB',               --- 최대 파일 크기
    'sink.rolling-policy.rollover-interval' = '30 min',      --- 최대 파일 쓰기 시간
    'sink.partition-commit.delay' = '1 s',                   --- 파티션 커밋 지연
    'sink.partition-commit.policy.kind' = 'success-file'     --- 파티션 커밋 방법
);
```

>? Sink의 WITH 매개변수에 대한 자세한 내용은 Filesystem (HDFS/COS)을 참고하십시오.
>

#### 3. 비즈니스 로직 구성

```sql
INSERT INTO `cos_sink`
SELECT * FROM `random_source`;
```

>! 이는 예시용이며 실제 비즈니스 목적이 없습니다.
>

#### 4. 작업 매개변수 설정

**내장 Connector**로 `flink-connector-cos`를 선택하고 **고급 매개변수**에서 COS URL을 다음과 같이 구성합니다.

```shell
fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
fs.cosn.credentials.provider: org.apache.flink.fs.cos.OceanusCOSCredentialsProvider
fs.cosn.bucket.region: <COS 리전>
fs.cosn.userinfo.appid: <COS 사용자 appid>
```

작업은 다음과 같이 구성됩니다.

- `<COS region>`을 ap-guangzhou와 같은 실제 COS 리전으로 바꿉니다.
- `<COS user appid>`를 실제 APPID로 바꿉니다. 이는 [계정 센터](https://console.cloud.tencent.com/developer)에서 볼 수 있습니다. 

>? 작업 매개변수 설정에 대한 자세한 내용은 Filesystem (HDFS/COS)을 참고하십시오.
>

#### 5. 작업 시작

**저장 > 구문 확인 > 초안 릴리스**를 클릭하고 SQL 작업이 시작될 때까지 기다렸다가 해당 COS 디렉터리로 이동하여 작성된 데이터를 확인합니다.

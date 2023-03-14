## 통합 네임스페이스 기능 개요

GooseFS 통합 네임스페이스(NameSpace) 기능은 투명한 네이밍 메커니즘을 통해 다양한 기본 스토리지 시스템 액세스 시맨틱을 통합하여 사용자에게 데이터 관리에 대한 통합된 인터랙티브 뷰를 제공합니다.

GooseFS는 이 기능을 활용하여 로컬 파일 시스템, Tencent Cloud Object Storage(COS), Tencent Cloud HDFS(CHDFS)와 같은 다양한 기본 스토리지 시스템과 연결 및 통신하며, 상위 계층 비즈니스를 위한 통합 액세스 API 및 파일 프로토콜을 제공합니다. 이러한 방식으로 비즈니스 측은 다양한 기본 스토리지 시스템에 저장된 데이터에 액세스하기 위해 GooseFS에서 제공하는 액세스 API만 호출하면 됩니다.

![](https://main.qcloudimg.com/raw/6ef8e2899bbd704f7c05c7d0526624b1.png)

상기 이미지는 통합 네임스페이스의 작동 원리를 보여줍니다. GooseFS의 네임스페이스 생성 명령인 create ns를 사용하여 COS 및 CHDFS의 지정된 파일 디렉터리를 GooseFS에 마운트한 다음 gfs:// 통합 schema를 사용하여 데이터에 액세스할 수 있습니다. 자세한 설명은 다음과 같습니다.

- COS는 총 3개의 버킷(bucket-1, bucket-2, bucket-3)이 있으며 Bucket-1에는 BU_A와 BU_B라는 2개의 디렉터리가 있습니다. bucket-1, bucket-2는 모두 GooseFS에 마운트되어 있습니다.
- Cloud HDFS에는 BU_E, BU_F, BU_G, BU_H의 4개의 디렉터리가 있으며 BU_H를 제외한 모든 디렉터리는 GooseFS에 마운트됩니다.
- GooseFS의 파일 작업에서 두 ​​디렉터리 BU_A, BU_E에 gfs://의 통합 schema로 액세스하면 정상적으로 액세스할 수 있으며, 파일은 GooseFS의 로컬 파일 시스템에 캐싱됩니다.
-  기본 파일 시스템(COS, Cloud HDFS)에 저장된 2개의 디렉터리 BU_A와 BU_E는 GooseFS에 마운트되어 있으며, 파일이 GooseFS에 캐싱되어 있다면 gfs://의 통합 schema로 액세스할 수 있습니다(예: hadoop fs ls gfs://BU_A ). 각 원격 파일 시스템의 네임스페이스를 통해 액세스할 수도 있습니다(예: hadoop fs ls cosn://bucket-1/BU_A ).
- 파일이 GooseFS에 캐시되지 않은 경우, 파일이 GooseFS의 로컬 파일 시스템에 캐시되지 않기 때문에 통합 스키마 gfs://를 통해 액세스할 수 없지만 여전히 기본 스토리지 시스템의 네임스페이스를 통해 액세스할 수 있습니다.

## 통합 네임스페이스 기능 사용

ns 작업을 통해 GooseFS에 네임스페이스를 생성하고, 기본 스토리지 시스템을 GooseFS에 매핑할 수 있습니다. 현재 지원되는 기본 스토리지 시스템에는 COS, CHDFS, 로컬 HDFS 등이 있습니다. 네임스페이스 생성 작업은 Linux 파일 시스템에서 파일 볼륨을 디스크를 마운트하는 절차와 유사합니다. 생성된 네임스페이스를 사용하여 GooseFS는 통일적인 액세스 의미 체계를 가진 파일 시스템을 클라이언트에 제공할 수 있습니다. GooseFS 네임스페이스에 대한 현재 작동 지침 세트는 다음과 같습니다.

```plaintext
$ goosefs ns
Usage: goosefs ns [generic options]
         [create <namespace> <CosN/Chdfs path> <--wPolicy <1-6>> <--rPolicy <1-5>> [--readonly] [--shared] [--secret fs.cosn.userinfo.secretId=<AKIDxxxxxxx>] [--secret fs.cosn.userinfo.secretKey=<xxxxxxxxxx>] [--attribute fs.ofs.userinfo.appid=1200000000][--attribute fs.cosn.bucket.region=<ap-xxx>/fs.cosn.bucket.endpoint_suffix=<cos.ap-xxx.myqcloud.com>]]
         [delete <namespace>]                                      
         [help [<command>]]                                        
         [ls [-r|--sort=option|--timestamp=option]]                
         [setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>]
         [setTtl [--action delete|free] <namespace> <time to live>]
         [stat <namespace>]                                        
         [unsetPolicy <namespace>]                                 
         [unsetTtl <namespace>] 
```
>!
>- 비즈니스 보안 향상을 위해 영구 키 대신 서브 계정 키 또는 임시 키를 사용하는 것이 좋습니다. 서브 계정 승인 시 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 준수하여 예상치 못한 데이터 유출을 방지하시기 바랍니다.
>- 영구 키를 사용해야 하는 경우 사용 보안을 향상시키기 위해 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)에 따라 허용된 작업, 리소스 범위 및 액세스 IP와 같은 조건을 포함한 권한 범위를 영구 키에 제한하는 것이 좋습니다.

상기 명령어 집합의 각 명령어의 기능 설명은 아래와 같습니다. 

| 명령        | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| create      | 네임스페이스를 생성하고 원격 스토리지 시스템 UFS를 네임스페이스에 매핑하는 데 사용됩니다. 네임스페이스를 생성할 때 캐시 읽기 및 쓰기 정책 설정을 지원합니다. 인증된 키 정보(secretId, secretKey)를 전달해야 합니다. |
| delete      | 지정한 네임스페이스를 삭제하는 데 사용됩니다.                                       |
| ls          | 마운트 포인트, UFS 경로, 생성 시간, 캐시 정책, TTL 정보 등 지정된 네임스페이스의 세부 정보를 나열하는 데 사용됩니다. |
| setPolicy   | 지정한 네임스페이스의 캐시 정책을 설정하는 데 사용됩니다.                             |
| setTtl      | 지정한 네임스페이스의 TTL를 설정하는 데 사용됩니다.                                 |
| stat        | 마운트 포인트, UFS 경로, 생성 시간, 캐시 정책, TTL 정보, 영속화 상태, 사용자 그룹, ACL, 마지막 액세스 시간, 수정 시간 등과 같은 지정된 네임스페이스에 대한 설명 정보 제공에 사용됩니다. |
| unsetPolicy | 지정한 네임스페이스의 캐시 정책을 재설정하는 데 사용됩니다.                             |
| unsetTtl    | 지정한 네임스페이스의 TTL를 재설정하는 데 사용됩니다.                                 |

### 네임스페이스 생성 및 삭제
GooseFS를 통해 네임스페이스 작업을 생성하면 자주 액세스하는 핫 데이터를 원격 스토리지 시스템에서 로컬 고성능 스토리지 노드로 캐시할 수 있어, 로컬 컴퓨팅 서비스에 고성능 데이터 액세스 기능을 제공합니다. 다음은 COS의 example-bucket 버킷, 버킷의 example-prefix 디렉터리 및 Cloud HDFS 파일 시스템이 각각 test_cos, test_cos_prefix, test_chdfs 등 네임스페이스에 매핑됨을 보여줍니다.

```plaintext
# COS 버킷 example-bucket을 test_cos 네임스페이스에 매핑
$ goosefs ns create test_cos cosn://example-bucket-1250000000/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com 

# COS 버킷 example-bucket의 example-prefix 디렉터리를 test_cos_prefix 네임스페이스에 매핑
$ goosefs ns create test_cos_prefix cosn://example-bucket-1250000000/example-prefix/ --wPolicy 1 --rPolicy 1 --secret fs.cosn.userinfo.secretId=AKIDxxxxxxx --secret fs.cosn.userinfo.secretKey=xxxxxxxxxx --attribute fs.cosn.bucket.region=ap-guangzhou --attribute fs.cosn.bucket.endpoint_suffix=cos.ap-guangzhou.myqcloud.com

# 클라우드 HDFS 파일 시스템 f4ma0l3qabc-Xy3을 test_chdfs 네임스페이스에 매핑
$ goosefs ns create test_chdfs ofs://f4ma0l3qabc-Xy3/ --wPolicy 1 --rPolicy 1 --attribute fs.ofs.userinfo.appid=1250000000
```

생성 완료 후, goosefs fs ls 명령을 통해 디렉터리 세부 사항을 조회할 수 있습니다.
```plaintext
$ goosefs fs ls /test_cos
```

네임스페이스를 사용하지 않을 경우 delete 명령을 통해 삭제할 수 있습니다.

```plaintext
$ goosefs ns delete test_cos
Delete the namespace: test_cos
```

### 캐시 정책 설정
사용자는 setPolicy 및 unsetPolicy를 통해 지정된 네임스페이스의 캐시 정책을 설정할 수 있습니다. 캐싱 정책을 설정하기 위한 명령어 집합은 다음과 같습니다.
```plaintext
$goosefs ns setPolicy [--wPolicy <1-6>] [--rPolicy <1-5>] <namespace>
```
각 매개변수의 의미는 다음과 같습니다.
- wPolicy: 캐시 쓰기 정책. 6가지 캐시 쓰기 정책을 지원합니다.
- rPolicy: 캐시 읽기 정책. 5가지 캐시 읽기 정책을 지원합니다.
- namespace: 지정된 네임스페이스.

현재 GooseFS에서 지원하는 캐시 읽기 및 쓰기 정책은 다음과 같습니다.

**캐시 쓰기 정책**

| 정책 이름      | 동작                                                         | 해당 Write_Type | 데이터 보안성 | 쓰기 효율 |
| :------------ | :---------------------------------- | :--------- | :-----  | :-----  |
| MUST_CACHE(1) | 데이터는 GooseFS에만 저장되며 원격 스토리지 시스템에는 기록하지 않습니다. | MUST_CACHE | 없음     | 높음     |
| TRY_CACHE(2) | 캐시에 공간이 있으면 GooseFS에 기록하고, 캐시에 공간이 없으면 기본 스토리지에 기록합니다. | TRY_CACHE | 없음 | 중간 |
| CACHE_THROUGH (3) | 가능한 한 많은 데이터를 캐싱하면서 동시에 원격 스토리지 시스템에 기록합니다.                    | CACHE_THROUGH | 있음       | 낮음    |
| THROUGH (4)       | GooseFS에 데이터를 저장하지 않고 원격 스토리지 시스템에 직접 기록합니다.                   | THROUGH | 있음       | 중간     |
| ASYNC_THROUGH(5) | 데이터는 GooseFS에 기록되고 원격 스토리지 시스템에 비동기적으로 새로고침합니다.                 | ASYNC_THROUGH | 약함     | 높음     |

>? Write_Type: 사용자가 SDK 또는 API를 호출하여 GooseFS에 데이터를 쓸 때 지정하는 파일 캐싱 정책을 말하며, 이는 단일 파일에 적용됩니다.
> 

**캐시 읽기 정책**

| 정책 이름                      | 동작                                                         | 메타데이터 동기화 | 해당 Read_Type | 데이터 일관성 | 읽기 효율                  | 데이터 캐시 여부 |
| :---------------------------- | :----------------------------------------------------------- | :--------- | ------------- | :--------- | :---------------------- | :----------- |
| NO_CACHE(1)                 | 데이터를 캐시하지 않고 원격 스토리지 시스템에서 직접 데이터를 읽습니다.                     | NO         | NO_CACHE      | 높음     | 낮음                      | NO           |
| CACHE(2)                    | <li>메타데이터 액세스 동작: 캐시가 히트되면 메타데이터는 Master를 따르며, 메타데이터는 언더 스토리지부터 능동적으로 동기화되지 않습니다. </li><li>데이터 스트림 액세스 동작: 데이터 스트림의 ReadType은 CACHE 정책을 사용합니다. </li> | Once       | CACHE         | 낮음     | 히트: 높음<br/>미스: 낮음 | YES           |
| CACHE_PROMOTE(3)            | <li>메타데이터 액세스 동작: CACHE 모드와 동일합니다. </li><li>데이터 스트림 액세스 동작: 데이터 스트림의 ReadType은 CACHE_PROMOTE 정책을 사용합니다. </li> | Once       | CACHE_PROMOTE | 낮음     | 히트: 높음<br/>미스: 낮음 | YES           |
| CACHE_CONSISTENT_PROMOTE(4) | <li>메타데이터 동작: 각 읽기 작업 전에 원격 스토리지 시스템 UFS의 메타데이터가 동기화됩니다. UFS가 없으면 Not Exists 예외가 발생합니다. </li><li>데이터 스트림 액세스 동작: 데이터 스트림의 ReadType은 CACHE_PROMOTE 정책을 사용하고 히트 후에는 가장 핫한 캐시 미디어에 캐시됩니다. </li> | Always     | CACHE         | 높음    | 히트: 중간<br/>미스: 낮음 | YES           |
| CACHE_CONSISTENT(5)         | <li>메타데이터 동작: CACHE_CONSISTENT_PROMOTE와 동일합니다. </li><li>데이터 스트림 액세스 동작: 데이터 스트림의 ReadType은 CACHE 정책을 사용합니다. 즉, CACHE 히트 시 다른 미디어 레이어에서 데이터를 이동하지 않습니다. </li> | Always     | CACHE_PROMOTE | 높음     | 히트: 중간<br/>미스: 낮음 | YES           |

>? Read_Type: 사용자가 SDK 또는 API를 호출하여 GooseFS에서 데이터를 읽을 때 지정하는 파일 캐싱 정책을 말하며, 이는 단일 파일에 적용됩니다.
>  

현재 빅 데이터 비즈니스 사례와 결합하여 다음과 같은 캐시 읽기/쓰기 정책 조합을 권장합니다.

| 캐시 쓰기 정책                      | 캐시 읽기 정책                                                         | 정책 조합 성능 |
| :---------------------------- | :----------------------------------------------------------- | :--------- |
|CACHE_THROUGH(3)|CACHE_CONSISTENT(5)|캐시 및 원격 스토리지 시스템 데이터 일관성 높음.|
|CACHE_THROUGH(3)|CACHE(2)|쓰기 일관성 높음, 읽기 최종 일관성.|
|ASYNC_THROUGH(5)|CACHE_CONSISTENT(5)|쓰기 최종 일관성, 읽기 일관성 높음.|
|ASYNC_THROUGH(5)|CACHE(2)|읽기/쓰기 최종 일관성.|
|MUST_CACHE(1)|CACHE(2)|캐시에서만 데이터 쓰기함.|

다음 예시는 지정된 네임스페이스 test_cos의 캐시 읽기/쓰기 정책이 CACHE_THROUGH 및 CACHE_CONSISTENT로 설정되어있습니다.
```plaintext
$ goosefs ns setPolicy --wPolicy 3 --rPolicy 5 test_cos
```

>!네임스페이스 생성 시 캐시 정책을 지정하는 것 외에도 사용자는 파일을 읽기/쓰기할 때 지정된 파일에 대해 ReadType 또는 Write_Type을 설정하거나 properties 프로파일을 통해 전역 캐시 정책을 설정할 수도 있습니다. 여러 정책이 동시에 존재하는 경우 우선순위는 사용자 정의 우선순위 >  Namespace 읽기/쓰기 정책 > 프로파일의 전역 캐시 정책 설정입니다. 이 중 읽기 정책의 경우 사용자 정의 ReadType과 Namespace의 DirReadPolicy 조합이 적용됩니다. 즉, 데이터 스트림 읽기 정책은 사용자 정의 ReadType을 채택하고 메타데이터는 Namespace 정책을 채택합니다. 
>
> 예를 들어 GooseFS에 COSN 네임스페이스가 있고 읽기 정책이 CACHE_CONSISTENT인 경우 이 네임스페이스에 test.txt 파일이 있다고 가정합니다. 클라이언트가 test.txt를 읽을 때 ReadType을 CACHE_PROMOTE로 지정하면, 전체 읽기 동작은 메타데이터와 CACHE_PROMOTE를 동기화합니다.
> 

unsetPolicy 명령을 사용하여 읽기 및 쓰기 캐싱 정책을 재설정할 수 있습니다. 다음은 test_cos 네임스페이스의 캐시 읽기/쓰기 정책 재설정 관련 내용입니다.
```plaintext
$ goosefs ns unsetPolicy test_cos
```


### TTL 설정

TTL은 GooseFS의 로컬 노드에 캐시된 데이터를 관리하는 데 사용되며, TTL 매개변수를 설정하면 캐시 데이터가 지정된 시간 후에 지정된 작업을 수행할 수 있습니다. 예: delete 또는 free 작업. 현재 TTL 설정 작업 지침은 다음과 같습니다.

```plaintext
$ goosefs ns setTtl [--action delete|free] <namespace> <time to live>
```

각 매개변수의 의미는 다음과 같습니다.
- action: 캐시 시간이 만료된 후 수행되는 작업으로, 현재 delete 및 free 두 가지 작업을 지원합니다. delete 작업은 캐시 및 UFS의 데이터를 삭제하고, free 작업은 캐시의 데이터만 삭제합니다.
- namespace: 지정된 네임스페이스.
- time to live: 데이터 캐시 시간(단위: 밀리초).

다음 예시는 지정된 네임스페이스 test_cos의 정책이 60초 후에 삭제되도록 설정되었음을 보여줍니다.

```plaintext
$ goosefs ns setTtl --action free test_cos 60000
```

## 메타데이터 정보 관리

이 섹션에서는 GooseFS가 메타데이터 동기화, 업데이트 등 메타데이터를 관리하는 방법을 소개합니다. GooseFS는 사용자에게 통합된 네임스페이스 기능을 제공합니다. 사용자는 통합된 gfs:// 경로를 통해 다른 기본 스토리지 시스템의 파일에 액세스할 수 있으며, 기본 스토리지 시스템의 경로만 지정하면 됩니다. 메타데이터 정보의 일관성을 보장하기 위해, GooseFS에서 데이터를 읽고 쓸 때 GooseFS를 통합 데이터 액세스 레이어로 사용할 것을 권장합니다.

### 메타데이터 동기화 개요

conf/goosefs-site.properties 프로파일에서 메타데이터 동기화 주기를 수정하여 메타데이터 동기화 주기를 관리할 수 있으며, 설정 매개변수는 다음과 같습니다.

```plaintext
goosefs.user.file.metadata.sync.interval=<INTERVAL>
```

동기화 주기는 다음 3가지 입력 매개변수를 지원합니다.

- 입력 매개변수 값이 -1일 경우: 처음 GooseFS에 로딩된 후 메타데이터 업데이트하지 않음.
- 입력 매개변수 값이 0일 경우: GooseFS가 각 읽기 및 쓰기 작업 후에 메타데이터를 업데이트함.
- 입력 매개변수 값이 양의 정수일 경우: GooseFS가 지정된 시간 간격으로 메타데이터를 주기적으로 업데이트함.

노드 수량, GooseFS 클러스터와 기본 스토리지의 I/O 간격, 기본 스토리지 유형을 종합적으로 고려하여 적절한 동기화 기간을 선택할 수 있습니다. 일반적인 경우는 다음과 같습니다.

- GooseFS 클러스터 노드 수가 많을수록 메타데이터 동기화 딜레이가 길어집니다.
- GooseFS 클러스터와 기본 스토리지 시스템 간의 거리가 멀수록, 메타데이터 동기화 딜레이가 길어집니다.
- 기본 스토리지 시스템이 메타데이터 동기화 딜레이에 미치는 영향은 주로 시스템 요청의 QPS 부하에 따라 결정됩니다. QPS 부하가 클수록 동기화 딜레이가 짧아집니다.

### 메타데이터 동기화 관리 방법

#### 설정 방법

1. 명령 라인을 통해 설정합니다.
명령 라인을 통해 메타데이터 정보의 동기화 기간을 설정할 수 있습니다.
```plaintext
goosefs fs ls -R -Dgoosefs.user.file.metadata.sync.interval=0 <path to sync>
```
2. 프로파일을 통해 설정합니다.
대규모 Goosefs 클러스터의 경우, goosefs-site.properties 프로파일을 통해 클러스터 내 Master 노드의 메타데이터 정보 동기화 주기를 일괄 설정할 수 있으며, 다른 노드의 동기화 주기는 기본적으로 주기값에 따라 실행됩니다.
```plaintext
goosefs.user.file.metadata.sync.interval=1m
```

>! 많은 서비스는 디렉터리에 따라 데이터 용도 구별을 선택하고, 각각의 디렉터리 데이터 액세스 빈도는 완전히 동일하지는 않습니다. 메타데이터 동기화 주기는 디렉터리별로 다른 주기값을 설정할 수 있으며, 디렉터리가 자주 변경되는 일부 디렉터리의 경우, 디렉터리의 메타데이터 동기화 주기를 더 짧게(예: 5분) 설정할 수 있습니다. 변화가 극도로 적거나 변화가 없는 디렉터리는 동기화 주기를 -1로 설정하여 GooseFS가 디렉터리의 메타데이터를 자동으로 동기화하지 않도록 할 수 있습니다.
>

#### 권장 설정

서비스 액세스 모드에 따라 다른 메타데이터 동기화 기간을 설정할 수 있습니다.

<table>
   <tr>
      <td colspan=2>액세스 모드</td>
      <td>메타데이터 동기화 주기</td>
      <td>설명</td>
   </tr>
   <tr>
      <td colspan=2>모든 파일 요청은 GooseFS를 통과합니다.</td>
      <td>-1</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan=2>대부분의 파일 요청은 GooseFS를 통과합니다.</td>
      <td>HDFS를 UFS로 사용합니다.</td>
      <td>핫 업데이트 또는 경로별 업데이트 사용을 권장합니다.</td>
      <td>HDFS가 매우 자주 업데이트되는 경우, 업데이트 주기를 -1로 설정할 것을 권장합니다. 업데이트가 금지됩니다.</td>
   </tr>
   <tr>
      <td>COS를 UFS로 사용합니다.</td>
      <td>경로에 따라 업데이트 주기를 설정할 것을 권장합니다.</td>
      <td rowspan=3>각 디렉터리에 다른 업데이트 주기를 설정하면, 메타데이터 동기화의 부담을 완화할 수 있습니다.</td>
   </tr>
   <tr>
      <td rowspan=2>파일 업로드 요청은 일반적으로 GooseFS를 거치지 않습니다.</td>
      <td>HDFS를 UFS로 사용합니다.</td>
      <td>경로에 따라 업데이트 주기를 설정할 것을 권장합니다.</td>
   </tr>
   <tr>
      <td>COS를 UFS로 사용합니다.</td>
      <td>경로에 따라 업데이트 주기를 설정할 것을 권장합니다.</td>
   </tr>
</table>

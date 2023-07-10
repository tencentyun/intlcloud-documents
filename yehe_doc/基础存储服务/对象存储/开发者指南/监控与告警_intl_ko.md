## 개요

COS의 읽기/쓰기 요청량, 트래픽 등의 데이터는 [Cloud Monitor](https://www.tencentcloud.com/document/product/248)를 기반으로 통계 및 표시합니다. COS 콘솔 또는 클라우드 모니터링의 [콘솔](https://console.cloud.tencent.com/monitor)에서 COS의 읽기/쓰기 요청량, 트래픽 등 자세한 모니터링 데이터를 확인할 수 있습니다.

>?
>- 본 문서는 COS 콘솔에서 통계를 얻는 방법을 설명합니다. Cloud Monitor API를 호출하여 더 자세한 데이터를 얻을 수 있습니다. 자세한 내용은 [Cloud Monitor](https://www.tencentcloud.com/document/product/248) 제품 문서를 참고하십시오.
>- 현재 CM에 보고된 모든 메트릭은 모든 COS 리전을 지원합니다. 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.

## 기본 기능

Cloud Monitor는 COS에 다음과 같은 게이트를 제공하여 모니터링과 알람 기능을 구현합니다.

| 모듈       | 설명                                     | 주요 기능                                                     |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| 모니터링 개요   | 제품의 현재 상태 표시                       | 전체 현황, 알람 현황, 전체 모니터링 정보 목록 제공                     |
| 알람 관리   | 알람 관리 및 설정 지원                       | COS에 신규 추가된 알람 정책, 사용자 정의 정보, 트리거 조건 템플릿 지원       |
| 모니터링 플랫폼   | 트래픽 모니터링 및 사용자 정의한 모니터링 지표 데이터 조회 | 사용자 전체 대역폭 정보 조회, 사전에 모니터링 지표 및 보고 데이터 사용자 정의 |
| 클라우드 서비스 모니터링 | COS의 버킷 모니터링 도표 조회            | 현재 각 버킷의 읽기/쓰기 요청량, 트래픽 등 모니터링 도표 및 데이터 조회       |

## 시나리오

- **일상 관리 시나리오**: Cloud Monitor 콘솔에 로그인하여 COS의 실행 상태를 실시간으로 확인합니다.
- **이상 경고 처리 시나리오**: 모니터링 데이터가 알람 임계값에 도달하는 경우, 알람 정보를 발송하여 사용자가 빠르게 이상 경고 알림을 수신하고 원인을 찾아 즉시 처리할 수 있도록 합니다.

## 콘솔에서 설정 및 조회

[Cloud Monitor 콘솔](https://console.cloud.tencent.com/monitor)을 통해 COS에 알람 정책을 생성하고, 모니터링 지표가 설정값에 이르면 알람을 수신합니다. 작업 관련 가이드는 [모니터링 알람 설정](https://intl.cloud.tencent.com/document/product/436/39104)을 참고하십시오.

모니터링 데이터를 조회하려면, **클라우드 서비스 모니터링 > [COS](https://console.cloud.tencent.com/monitor/product/COS)** 페이지에서 모든 버킷의 모니터링 데이터, 상태, 알람 정책 수를 확인할 수 있습니다. 또한, COS 콘솔에서도 조회할 수 있으며, 작업 가이드는 [데이터 개요 조회](https://intl.cloud.tencent.com/document/product/436/36542) 및 [데이터 모니터링 조회](https://intl.cloud.tencent.com/document/product/436/31634)를 참고하십시오.

## 인터페이스로 호출

호출 인터페이스를 통해 COS의 모니터링 데이터를 조회할 수 있으며, COS의 모니터링 항목은 다음과 같습니다. COS의 모니터링 인터페이스에 대한 자세한 내용은 [COS 모니터링 지표](https://intl.cloud.tencent.com/document/product/248/37269) 문서를 참고하십시오.

## 모니터링 지표

> ?COS는 범용 리전을 사용합니다. 따라서 버킷이 어떤 리전에 소속되어 있든 COS 모니터링 지표 데이터 풀링 시, Region은 항상 '광저우' 리전으로 선택하십시오.
> - [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=monitor&Version=2018-07-24&Action=DescribeBaseMetrics)를 사용해 데이터 풀링 시, Region 필드는 항상 '화남 리전(광저우)'으로 선택하십시오.
> - SDK를 사용해 데이터 풀링 시, Region 필드는 항상 'ap-guangzhou'로 입력하십시오.

### 요청 관련

| 지표 이름(영어)           | 지표 이름(한글)               | 지표의 의미                                                     | 단위 | 차원          |
| -------------------- | ------------------------ | ------------------------------------------------------------ | ---- | ------------- |
| StdReadRequests      | 스탠다드 스토리지 읽기 요청           | 스탠다드 스토리지 유형의 읽기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| StdWriteRequests     | 스탠다드 스토리지 쓰기 요청           | 스탠다드 스토리지 유형의 쓰기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨  | 회   | appid, bucket |
| IaReadRequests       | 스탠다드IA 스토리지 읽기 요청           | 스탠다드IA 스토리지 유형의 읽기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| IaWriteRequests      | 스탠다드IA 스토리지 쓰기 요청           | 스탠다드IA 스토리지 쓰기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| DeepArcReadRequests  | DEEP ARCHIVE 읽기 요청       | DEEP ARCHIVE 유형의 읽기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| DeepArcWriteRequests | DEEP ARCHIVE 쓰기 요청       | DEEP ARCHIVE 유형의 쓰기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| ItReadRequests       | INTELLIGENT TIERING 읽기 요청       | INTELLIGENT TIERING 유형의 읽기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| ItWriteRequests      | INTELLIGENT TIERING 쓰기 요청       | INTELLIGENT TIERING 유형의 쓰기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| TotalRequests        | 총 요청 수                 | 모든 스토리지 유형의 총 읽기/쓰기 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| GetRequests          | GET 관련 총 요청 수           | 모든 스토리지 유형의 GET 관련 총 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |
| PutRequests          | PUT 관련 총 요청 수           | 모든 스토리지 유형의 PUT 관련 총 요청 횟수. 요청 횟수는 요청 명령 발송 횟수에 따라 계산됨 | 회   | appid, bucket |

### 스토리지 관련

| 지표 이름(영어)                   | 지표 이름(한글)                        | 단위 | 차원          |
| ---------------------------- | --------------------------------- | ---- | ------------- |
| StdStorage                   | 스탠다드 스토리지 - 스토리지 용량                 | MB   | appid, bucket |
| SiaStorage                   | 스탠다드IA 스토리지 - 스토리지 용량                 | MB   | appid, bucket |
| ItFreqStorage                | INTELLIGENT TIERING - 고빈도 레이어 스토리지 용량       | MB   | appid, bucket |
| ItInfreqStorage              | INTELLIGENT TIERING - 저빈도 레이어 스토리지 용량       | MB   | appid, bucket |
| ArcStorage                   | ARCHIVE - 스토리지 용량                 | MB   | appid, bucket |
| DeepArcStorage               | DEEP ARCHIVE - 스토리지 용량             | MB   | appid, bucket |
| StdObjectNumber              | 스탠다드 스토리지 - 객체 수                 | 개   | appid, bucket |
| IaObjectNumber               | 스탠다드IA 스토리지 - 객체 수                 | 개   | appid, bucket |
| ItFreqObjectNumber           | INTELLIGENT TIERING_고빈도 레이어 객체 수       | 개   | appid, bucket |
| ItInfreqObjectNumber         | INTELLIGENT TIERING_저빈도 레이어 객체 수       | 개   | appid, bucket |
| ArcObjectNumber              | ARCHIVE 객체 수                  | 개   | appid, bucket |
| DeepArcObjectNumber          | DEEP ARCHIVE 객체 수              | 개   | appid, bucket |
| StdMultipartNumber           | 스탠다드 스토리지 - 파일 조각 수               | 개   | appid, bucket |
| IaMultipartNumber            | 스탠다드IA 스토리지 - 파일 조각 수               | 개   | appid, bucket |
| ItFrequentMultipartNumber    | INTELLIGENT TIERING - 고빈도 파일 조각 수           | 개   | appid, bucket |
| ArcMultipartNumber           | ARCHIVE - 파일 조각 수               | 개   | appid, bucket |
| DeepArcMultipartNumber       | DEEP ARCHIVE - 파일 조각 수           | 개   | appid, bucket |

### 트래픽 관련

| 지표 이름(영어)                    | 지표 이름(한글)           | 지표의 의미                                                 | 단위 | 차원          |
| ----------------------------- | -------------------- | -------------------------------------------------------- | ---- | ------------- |
| InternetTraffic           | 공인 네트워크 다운스트림 트래픽         | 인터넷을 통해 데이터를 COS에서 클라이언트로 다운로드할 때 발생하는 트래픽              | B    | appid, bucket |
| InternetTrafficUp             | 공인 네트워크 업스트림 트래픽         | 인터넷을 통해 데이터를 클라이언트에서 COS로 업로드할 때 발생하는 트래픽              | B    | appid, bucket |
| InternalTraffic          | 내부 네트워크 다운스트림 트래픽         | Tencent Cloud 내부 네트워크를 통해 데이터를 COS에서 클라이언트로 다운로드할 때 발생하는 트래픽          | B    | appid, bucket |
| InternalTrafficUp             | 내부 네트워크 업스트림 트래픽         | Tencent Cloud 내부 네트워크를 통해 데이터를 클라이언트에서 COS로 업로드할 때 발생하는 트래픽          | B    | appid, bucket |
| CdnOriginTraffic              | CDN Origin-pull 트래픽         | 데이터를 COS에서 Tencent Cloud CDN 엣지 노드로 전송할 때 발생하는 트래픽           | B    | appid, bucket |
| InboundTraffic                | 공인 네트워크, 내부 네트워크 업로드 총 트래픽 | 인터넷 및 Tencent Cloud 내부 네트워크를 통해 데이터를 클라이언트에서 COS로 업로드할 때 발생하는 트래픽  | B    | appid, bucket |
| CrossRegionReplicationTraffic | 리전 간 복제 트래픽       | 데이터를 한 리전의 버킷에서 다른 리전의 버킷으로 전송할 때 발생하는 트래픽 | B    | appid, bucket |

### 반환 코드 관련

| 지표 이름(영어)      | 지표 이름(한글)     | 지표의 의미                                        | 단위 | 차원          |
| --------------- | -------------- | ----------------------------------------------- | ---- | ------------- |
| 2xxResponse     | 2xx 상태 코드     | 2xx 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 3xxResponse     | 3xx 상태 코드     | 3xx 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 4xxResponse     | 4xx 상태 코드     | 4xx 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 5xxResponse     | 5xx 상태 코드     | 5xx 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 2xxResponseRate | 2xx 상태 코드 비율 | 총 요청 횟수 중 2xx 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 3xxResponseRate | 3xx 상태 코드 비율 | 총 요청 횟수 중 3xx 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 4xxResponseRate | 4xx 상태 코드 비율 | 총 요청 횟수 중 4xx 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 5xxResponseRate | 5xx 상태 코드 비율 | 총 요청 횟수 중 5xx 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 400Response     | 400 상태 코드     | 400 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 403Response     | 403 상태 코드     | 403 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 404Response     | 404 상태 코드     | 404 상태 코드가 반환된 요청 횟수                     | 회   | appid, bucket |
| 400ResponseRate | 400 상태 코드 비율 | 총 요청 횟수 중 400 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 403ResponseRate | 403 상태 코드 비율 | 총 요청 횟수 중 403 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 404ResponseRate | 404 상태 코드 비율 | 총 요청 횟수 중 404 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 500ResponseRate | 500 상태 코드 비율 | 총 요청 횟수 중 500 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 501ResponseRate | 501 상태 코드 비율 | 총 요청 횟수 중 501 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 502ResponseRate | 502 상태 코드 비율 | 총 요청 횟수 중 502 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |
| 503ResponseRate | 503 상태 코드 비율 | 총 요청 횟수 중 503 상태 코드가 반환된 요청 횟수의 비율 | %    | appid, bucket |

> ?
> 1. 3xx, 4xx, 5xx 상태 코드에 관한 자세한 내용은 [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오.
> 2. 각 지표의 통계 단위(Period)는 모두 상이합니다. [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 인터페이스를 통해 각 지표가 지원하는 통계 단위를 확인할 수 있습니다.

### 데이터 읽기 관련

| 지표 이름(영어)   | 지표 이름(한글)     | 지표의 의미                                                     | 단위 | 차원          |
| ------------ | -------------- | ------------------------------------------------------------ | ---- | ------------- |
| StdRetrieval | 표준 데이터 읽기량 | 표준 데이터를 읽을 때 발생하는 트래픽. 스탠다드 스토리지의 공인 네트워크 다운스트림 트래픽, 내부 네트워크 다운스트림 트래픽, CDN Origin-pull 트래픽의 총합 | B    | appid, bucket |
| IaRetrieval  | 스탠다드IA 데이터 읽기량 | 스탠다드IA 데이터를 읽을 때 발생하는 트래픽. 스탠다드IA 스토리지의 공인 네트워크 다운스트림 트래픽, 내부 네트워크 다운스트림 트래픽, CDN Origin-pull 트래픽의 총합 | B    | appid, bucket |


### 데이터 처리 클래스

API를 호출하여 CI(Cloud Infinite)의 모니터링 데이터를 볼 수 있으며, CI의 모니터링 API에 대한 자세한 내용은 CI 모니터링 지표 문서를 참고하십시오.



## 각 차원의 해당 매개변수 개요

| 매개변수 이름                        | 차원 이름 | 차원 설명                | 포맷                                               |
| ------------------------------- | -------- | ----------------------- | -------------------------------------------------- |
| &Instances.N.Dimensions.0.Name  | appid    | 루트 계정 APPID의 차원 이름 | String 유형의 차원 이름 입력: appid                     |
| &Instances.N.Dimensions.0.Value | appid    | 루트 계정의 구체적인 APPID      | 루트 계정 APPID 입력. 예: 1250000000                 |
| &Instances.N.Dimensions.1.Name  | bucket   | 버킷 차원 이름          | String 유형의 차원 이름 입력: bucket                    |
| &Instances.N.Dimensions.1.Value | bucket   | 버킷의 구체적인 이름          | 버킷의 구체적인 이름 입력. 예: examplebucket-1250000000 |



## 입력 매개변수 설명

COS 모니터링 데이터를 조회합니다. 입력 매개변수 값은 다음과 같습니다.

&Namespace=QCE/COS
&Instances.N.Dimensions.0.Name=appid
&Instances.N.Dimensions.0.Value=루트 계정의 APPID
&Instances.N.Dimensions.1.Name=bucket
&Instances.N.Dimensions.1.Value=버킷 이름 


## 모니터링 설명

- **모니터링 간격**: Cloud Monitor는 실시간, 최근 24시간, 최근 7일, 사용자 정의 날짜 등 여러 가지 통계 구간에 따라 모니터링 데이터를 제공하며, 시간은 1분, 5분, 1시간, 1일로 세분화됩니다.
- **데이터 스토리지**: 1분 단위 모니터링 데이터, 15일 저장 / 5분 단위 모니터링 데이터, 31일 저장 / 1시간 단위 모니터링 데이터, 93일 저장 / 1일 단위 모니터링 데이터, 186일 저장을 지원합니다.
- **알람 표시**: Cloud Monitor는 COS의 모니터링 데이터를 통합하여 보기 쉬운 도표 형태로 표시합니다. 제품에 미리 정의된 알람 지표에 따라 알람을 보낼 수 있어 사용자가 전체적인 운영 상태를 파악할 수 있습니다.
- **알람 설정**: 모니터링 지표 임계값을 설정하고, 모니터링 데이터가 알람 조건을 충족하면 Cloud Monitor가 즉시 알람 정보를 관련 그룹에 전송합니다. 자세한 내용은 [Alarm Overview](https://www.tencentcloud.com/document/product/248/6126) 및 [모니터링 알람 설정](https://intl.cloud.tencent.com/document/product/436/39104)을 참고하십시오.





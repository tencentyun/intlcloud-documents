## 개요

COS의 읽기/쓰기 요청량, 트래픽 등의 데이터는 [클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248)을 기반으로 통계 및 표시합니다. COS 콘솔 또는 클라우드 모니터링의 [콘솔](https://console.cloud.tencent.com/monitor)에서 COS의 읽기/쓰기 요청량, 트래픽 등 자세한 모니터링 데이터를 확인할 수 있습니다.

>?본 문서는 COS 콘솔에서 통계 데이터를 획득하는 시나리오를 소개합니다. 데이터 인터페이스를 사용하여 더 자세한 정보를 얻으려면 클라우드 모니터링 인터페이스를 사용하십시오. 자세한 내용은 [클라우드 모니터링](https://intl.cloud.tencent.com/document/product/248) 제품 문서를 참조하십시오.

## 기본 기능

클라우드 모니터링은 COS에 다음과 같은 게이트를 제공하여 모니터링과 알람 기능을 구현합니다.

| 모듈       | 설명                                     | 주요 기능                                                     |
| ---------- | ---------------------------------------- | ------------------------------------------------------------ |
| 모니터링 개요   | 제품의 현재 상태 표시                       | 전체 현황, 알람 현황, 전체 모니터링 정보 목록 제공                     |
| 알람 관리   | 알람 관리 및 설정 지원                       | COS에 신규 추가된 알람 정책, 사용자 정의 정보, 트리거 조건 템플릿 지원       |
| 모니터링 플랫폼   | 트래픽 모니터링 및 사용자 정의한 모니터링 지표 데이터 조회 | 사용자 전체 대역폭 정보 조회, 사전에 모니터링 지표 및 보고 데이터 사용자 정의 |
| 클라우드 서비스 모니터링 | COS의 버킷 모니터링 도표 조회            | 현재 각 버킷의 읽기/쓰기 요청량, 트래픽 등 모니터링 도표 및 데이터 조회       |

## 사용 시나리오

- **일상 관리 시나리오**: 클라우드 모니터링 콘솔에 로그인하여 COS의 실행 상태를 실시간으로 확인합니다.
- **이상 경고 처리 시나리오**: 모니터링 데이터가 알람 임계값에 도달하는 경우, 알람 정보를 발송하여 사용자가 빠르게 이상 경고 알림을 수신하고 원인을 찾아 즉시 처리할 수 있도록 합니다.

## 콘솔에서 설정 및 조회

[클라우드 모니터링 콘솔](https://console.cloud.tencent.com/monitor)을 통해 COS에 알람 정책을 생성하고, 모니터링 지표가 설정값에 이르면 알람을 수신합니다. 작업 관련 가이드는 [모니터링 알람 설정](https://intl.cloud.tencent.com/document/product/436/39104)을 참조하십시오.

모니터링 데이터를 조회하려면, [클라우드 서비스 모니터링]>[COS](https://console.cloud.tencent.com/monitor/product/COS) 페이지에서 모든 버킷의 모니터링 데이터, 상태, 알람 정책 수를 확인할 수 있습니다. 또한, COS 콘솔에서도 조회할 수 있으며, 작업 가이드는 [데이터 개요 조회](https://intl.cloud.tencent.com/document/product/436/36542) 및 [데이터 모니터링 조회](https://intl.cloud.tencent.com/document/product/436/31634)를 참조하십시오.

## 인터페이스로 호출

호출 인터페이스를 통해 COS의 모니터링 데이터를 조회할 수 있으며, COS의 모니터링 항목은 다음과 같습니다.

#### 스토리지 관련

| 지표 이름(metricName) | 의미              | 단위 |
| ---------------------- | ----------------- | ---- |
| std_storage            | 표준 스토리지-스토리지 용량 | MB   |
| sia_storage            | 표준IA 스토리지-스토리지 용량 | MB   |
| nel_storage            | 니어라인 스토리지-스토리지 용량 | MB   |
| arc_storage            | CAS-스토리지 용량 | MB   |

#### 트래픽 관련

| 지표 이름(metricName) | 의미         | 단위 |
| ---------------------- | ------------ | ---- |
| internet_traffic       | 공인 네트워크 트래픽     | B    |
| internal_traffic       | 내부 네트워크 트래픽     | B    |
| cdn_origin_traffic     | CDN Origin-pull 트래픽 | B    |
| inbound_traffic        | 업로드 트래픽     | B    |

#### 데이터 읽기 관련

| 지표 이름(metricName) | 의미         | 단위 |
| ---------------------- | ------------ | ---- |
| std_retrieval          | 표준 데이터 읽기 | B    |
| sia_retrieval          | 표준IA 데이터 읽기 | B    |
| nel_retrieval          | 니어라인 데이터 읽기 | B    |

#### 요청 관련

| 지표 이름(metricName) | 의미           | 단위 |
| ---------------------- | -------------- | ---- |
| std_read_requests      | 표준 스토리지 읽기 요청 | 회 |
| std_write_requests     | 표준 스토리지 쓰기 요청 | 회 |
| ia_read_requests       | 표준IA 스토리지 읽기 요청 | 회 |
| ia_write_requests      | 표준IA 스토리지 쓰기 요청 | 회 |
| nl_read_requests       | 니어라인 스토리지 읽기 요청 | 회 |
| nl_write_requests      | 니어라인 스토리지 쓰기 요청 | 회 |

#### 반환 코드 관련

| 지표 이름(metricName) | 의미       | 단위 |
| ---------------------- | ---------- | ---- |
| 2xx_response           | 2xx 상태 코드 | 회 |
| 3xx_response           | 3xx 상태 코드 | 회 |
| 4xx_response           | 4xx 상태 코드 | 회 |
| 5xx_response           | 5xx 상태 코드 | 회 |

## 모니터링 설명

- **모니터링 간격**: 클라우드 모니터링은 실시간, 최근 24시간, 최근 7일, 사용자 정의 날짜 등 여러 가지 통계 구간에 따라 모니터링 데이터를 제공하며, 시간은 1분, 5분, 1시간, 1일로 세분화됩니다.
- **데이터 스토리지**: 1분 단위 모니터링 데이터, 15일 저장 / 5분 단위 모니터링 데이터, 31일 저장 / 1시간 단위 모니터링 데이터, 93일 저장 / 1일 단위 모니터링 데이터, 186일 저장을 지원합니다.
- **알람 표시**: 클라우드 모니터링은 COS의 모니터링 데이터를 통합하여 보기 쉬운 도표 형태로 표시합니다. 제품에 미리 정의된 알람 지표에 따라 알람을 보낼 수 있어 사용자가 전체적인 운영 상태를 파악할 수 있습니다.
- **알람 설정**: 모니터링 지표 임계값을 설정하고, 모니터링 데이터가 알람 조건을 충족하면 클라우드 모니터링이 즉시 알람 정보를 관련 그룹에 전송합니다. 자세한 내용은 [알람 개요](https://intl.cloud.tencent.com/document/product/248/38910) 및 [모니터링 알람 설정](https://intl.cloud.tencent.com/document/product/436/39104)을 참조하십시오.


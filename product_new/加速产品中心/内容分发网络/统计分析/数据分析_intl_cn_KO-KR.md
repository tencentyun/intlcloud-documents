액세스 로그를 통해 사용자 출처를 분석하고 데이터 분석 페이지에 유형별 그래프를 제공하여 고객이 사용자 분포 및 사용 상황을 알 수 있도록 도와줍니다.

[CDN Console](https://console.cloud.tencent.com/cdn)에 로그인한 다음 왼쪽 메뉴에서 [통계 관리]>[데이터 분석]을 클릭하여 데이터 분석 페이지로 이동합니다.

- 조회 가능한 최대 시간 구간은 31일이며 지난 데이터는 90일간 보관합니다.
- 조회 가능한 가장 빠른 지난 데이터는 본 조회일 기준 직전 3개월 이내입니다.

## 독립 IP 액세스 수
독립 IP 액세스 수는 특정 시간 주기에 따라 로그에 대한 액세스 소스 클라이언트 IP의 중복을 제거한 뒤 계산합니다.
- 시간 구간이 1일 이상일 때 5분 시간 데이터 분할 정도에서 중복 IP 수를 제거한 곡선을 제공합니다.
- 도메인 상황은 24시간 기준으로 중복을 제거하고 DAU를 계산하며, 다수 도메인/항목/계정 상황은 도메인당 DAU 기준으로 5분 시간 데이터 분할 정도를 누적합니다.

## 사용자 액세스 구역 분포
소스 클라이언트 IP를 통해 액세스한 사용자가 있는 지역을 식별하고, 지도, 목록을 표시하여 고객이 비즈니스 사용자 리전 분포 상황을 알기 쉽게 합니다.

## 사용자 통신사 분포
원본 클라이언트 IP를 통해 액세스한 사용자가 속한 통신사를 식별하고 원형 비율 그래프, 목록을 표시하여  고객이 비즈니스 사용자 통신사 분포 상황을 알기 쉽게 합니다.
![](https://main.qcloudimg.com/raw/88ab778c8ca2cbfb5f920a1684a76b9e.png)

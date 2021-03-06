## 소개

객체 스토리지 COS 콘솔은 스토리지 데이터 개요 페이지를 제공합니다. 페이지에서 버킷 수량, 객체 수량, 스토리지 용량, 요청 수 및 트래픽 등 데이터를 조회할 수 있습니다.

> !
>
> - 서브 계정으로 데이터를 조회해야 할 경우, [버킷 리스트 액세스] 권한이 있어야 합니다. 자세한 내용은 [서브 계정 버킷 리스트 액세스](https://intl.cloud.tencent.com/document/product/436/17061) 문서의 사전 설정 추가 정책 부분을 조회하십시오.
> - 이 데이터 개요는 [버킷 수량]을 제외한 실시간 데이터로, 나머지 데이터는 실시간 데이터가 아니며 약 2시간의 딜레이가 있습니다. 해당 데이터는 참고용 모니터링 데이터이며, 정확한 과금 계산은 [과금 센터](https://console.cloud.tencent.com/account)에서 조회할 수 있습니다.

## 데이터 그래프 조회

### 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 왼쪽 메뉴에서 [데이터 통계]>[기본 데이터 통계]를 클릭해 데이터 모니터링 페이지로 들어갑니다.
2. [데이터 개요] 페이지에서 다음 정보 조회가 가능합니다.
   ![](https://main.qcloudimg.com/raw/036d7c5f1e31fa9f69507733c2a4d8d9.png)
   - **버킷 수량**: 현재 생성 완료된 버킷 총 개수입니다.                                     
    - **객체 수량**: 현재 생성 완료된 모든 버킷 중 객체의 총 개수로, 각각 다른 스토리지 유형의 객체 수량 조회를 지원합니다.                      
    - **해당 월평균 스토리지 용량**: 해당 월평균 스토리지 용량의 구체적인 계산 방식은 현재 스토리지 용량/해당 월 일수입니다. 각각 표준 스토리지, 표준IA 스토리지, CAS 유형의 일 평균 스토리지 용량이 있습니다.
   - **스토리지 용량 그래프**: 표준 스토리지, 표준IA 스토리지, CAS의 스토리지 용량 조회를 선택할 수 있으며, 최근 1년의 데이터 상세 조회를 지원합니다.
   - **트래픽 그래프**: 표준 스토리지, 표준IA 스토리지의 외부 네트워크 다운스트림 트래픽, 내부 네트워크 트래픽, CDN Origin-pull 트래픽 조회를 선택할 수 있으며, 최근 1년의 데이터 상세 조회를 지원합니다.
   - **요청 수 그래프**: 표준 스토리지, 표준IA 스토리지 유형의 읽기 및 쓰기 요청 조회를 선택할 수 있으며, 최근 1년의 데이터 상세 조회를 지원합니다. 
   - **사용자 유효 요청 비율 그래프**: 표준 스토리지의 사용자 유효 읽기 및 쓰기 요청 비율 조회를 선택할 수 있으며, 최근 1년의 데이터 상세 조회를 지원합니다. 
   - **데이터 검색량 그래프**: 표준 스토리지, 표준IA 스토리지 유형의 검색량 조회를 지원합니다. 그중 CAS 유형은 고속 검색량, 일반 검색량, 일괄 검색량을 포함하며, 최근 1년의 데이터 상세 조회를 지원합니다.
   - **버킷 데이터 개요**: 버킷마다 어제와 해당 월의 버킷 핵심 데이터를 보여줍니다. 핵심 데이터 종류는 귀하가 선택한 스토리지 유형에 따라 달라지며, 표준 스토리지, 표준IA 스토리지, CAS의 용량, 저빈도 데이터 검색량, 보관 데이터 검색량, 일반/저빈도 읽기 및 쓰기 요청 수, 외부 네트워크 다운스트림 트래픽, 내부 네트워크 다운스트림 트래픽, CDN Origin-pull 트래픽을 포함합니다.
3. 도표 오른쪽의 다운로드 버튼을 통해 핵심 데이터를 일괄적으로 내보낼 수 있습니다. 

## 버킷 차원에 따른 데이터 조회

### 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인해 왼쪽 메뉴에서 [버킷 리스트]를 클릭하고 인터페이스에서 [통계 데이터]를 선택합니다.
2. 통계 데이터 인터페이스에서 스토리지 유형과 시간대에 따라 버킷 용량, 데이터 검색량, 트래픽, 요청 수 등 각 버킷의 통계 데이터를 조회할 수 있습니다.

## 개요

Cloud Object Storage(COS) 콘솔의 통계 페이지로 이동하여 버킷/객체/요청 수, 스토리지 사용량, 트래픽 및 기타 데이터를 볼 수 있습니다.

>!
> - 서브 계정으로 데이터 통계를 보려면 **버킷 리스트 액세스** 권한이 있어야 합니다. 자세한 내용은 [서브 계정으로 버킷 리스트 액세스](https://intl.cloud.tencent.com/document/product/436/17061) 문서의 사전 설정 정책 추가 부분을 참고하십시오.
> - **버킷 수**를 제외한 다른 데이터는 실시간이 아니며 약 2시간의 딜레이가 있습니다. 데이터는 모니터링 참고용으로만 사용합니다. 정확한 청구 데이터를 보려면 [과금 센터](https://console.cloud.tencent.com/account)로 이동하십시오.
> 

## 데이터 그래프 조회

### 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 왼쪽 사이드바에서 **사용 통계** > **기본 사용 통계**를 클릭하여 기본 사용 통계 페이지로 이동합니다.
2. **데이터 개요** 페이지에서 다음 정보를 조회할 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7cdb582b1cbb4859ffce7cf69d23b212.png)
    - **버킷 수**: 현재 생성된 버킷 수입니다.                                     
    - **총 객체 수**: 모든 버킷에서 생성된 객체 수입니다. 스토리지 클래스별 객체 수를 볼 수 있습니다.                      
    - **이번 달 일평균 사용량**: 스토리지 클래스(즉, STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE 및 DEEP ARCHIVE)별 일평균 사용량입니다. 일일 스토리지 사용량 = ‘5분당 사용량’ 합계 / 288(통계 포인트 수). 당월 일평균 스토리지 사용량 = 당월 일일 스토리지 사용량 합계/당월 일수.
   - **스토리지 사용량**: STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE 및 DEEP ARCHIVE에 대한 스토리지 사용량입니다. 지난 93일 동안의 데이터를 볼 수 있으며 각 쿼리의 시간 범위는 31일을 초과할 수 없습니다.
   - **트래픽**: STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING 및 MAZ_INTELLIGENT TIERING에 대한 공중망/사설망 다운스트림 트래픽 및 CDN Origin-pull 트래픽. 지난 93일 동안의 데이터를 볼 수 있으며 각 쿼리의 시간 범위는 31일을 초과할 수 없습니다.
   - **요청 수**: STANDARD, MAZ_STANDARD, STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING 및 MAZ_INTELLIGENT TIERING에 대한 읽기/쓰기 요청 수입니다. 지난 93일 동안의 데이터를 볼 수 있으며 각 쿼리의 시간 범위는 31일을 초과할 수 없습니다.
   - **요청 성공률**: STANDARD 및 MAZ_STANDARD에 대한 요청 성공률입니다. 지난 93일 동안의 데이터를 볼 수 있으며 각 쿼리의 시간 범위는 31일을 초과할 수 없습니다.
   - **데이터 검색**: STANDARD_IA, MAZ_STANDARD_IA, INTELLIGENT TIERING, MAZ_INTELLIGENT TIERING, ARCHIVE 및 DEEP ARCHIVE에 대해 검색된 데이터의 양입니다. ARCHIVE의 경우 금액은 긴급 검색, 일반 검색, 일괄 검색으로 구분됩니다. 지난 93일 동안의 데이터를 볼 수 있으며 각 쿼리의 시간 범위는 31일을 초과할 수 없습니다.
3. 각 차트의 오른쪽 상단 모서리에 있는 다운로드 버튼을 클릭하여 데이터를 다운로드할 수 있습니다. 

## 버킷 레벨 데이터 보기

### 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5) 로그인 후 왼쪽 사이드바에서 **버킷 리스트**를 클릭한 다음 **통계 데이터**를 선택합니다.
2. 통계 데이터 페이지에서 지정된 기간 동안의 스토리지 사용량, 데이터 검색, 트래픽 및 요청 수와 같은 버킷 데이터를 볼 수 있습니다.


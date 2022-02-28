본문은 콘솔에서 TDSQL for MySQL 인스턴스를 생성하는 방법을 설명합니다.

## 전제 조건
Tencent Cloud에 회원가입 및 실명 인증을 완료해야 합니다.
- Tencent Cloud 계정 생성 방법:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Tencent Cloud 계정 생성하기</a></div>
- 실명 인증 방법:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

## 작업 단계
1. [TDSQL for MySQL 구매 페이지](https://console.cloud.tencent.com/tdsqld/tdmysql-buy)에 로그인하여, 각 항목의 구성 정보를 필요에 따라 선택하고 오류가 없는지 확인한 뒤, **즉시 구매**를 클릭합니다.
 - **과금 방식**: 정액 과금제 및 종량제 과금 방식을 지원합니다.
    - 비즈니스에 안정적인 장기 수요가 있는 경우 정액 과금제를 선택하는 것이 좋습니다.
    - 서비스량이 급격히 변동하는 시나리오는 종량제 선택을 권장합니다.
 - **리전**: TDSQL for MySQL 인스턴스를 배포할 리전을 선택합니다. 연결할 CVM 인스턴스와 동일한 리전을 사용하는 것이 좋습니다. 다른 리전의 Tencent Cloud 서비스는 사설망을 통해 서로 통신할 수 없습니다. 리전은 구매 후 수정할 수 없습니다.
 - **네트워크**: TDSQL for MySQL 인스턴스가 있는 네트워크를 선택합니다. 연결할 CVM 인스턴스와 동일한 리전에서 동일한 VPC를 선택하는 것이 좋습니다. 그렇지 않으면 사설 네트워크를 통해 CVM 인스턴스와 데이터베이스에 연결할 수 없습니다.
 - **인스턴스 버전**: 자세한 내용은 [인스턴스 아키텍처](https://intl.cloud.tencent.com/document/product/1042/33319)를 참고하시고, 샤드 설정은 [샤드 설정](https://intl.cloud.tencent.com/document/product/1042/33354), 결제 세부 정보는 [과금 개요](https://intl.cloud.tencent.com/document/product/1042/35777)를 참고하십시오.
2. 결제 후 인스턴스 목록으로 돌아와 인스턴스 상태가 **초기화되지 않음**이 될 때까지 기다렸다가 인스턴스를 초기화합니다.


## 후속 작업
TDSQL for MySQL 인스턴스를 초기화해야 합니다. 자세한 내용은 [인스턴스 초기화](https://intl.cloud.tencent.com/document/product/1042/33337)를 참고하십시오.


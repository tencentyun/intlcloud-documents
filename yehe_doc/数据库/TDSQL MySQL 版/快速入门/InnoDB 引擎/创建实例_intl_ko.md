본문은 콘솔에서 TDSQL for MySQL 인스턴스를 생성하는 방법을 설명합니다.

## 전제 조건
Tencent Cloud 계정을 등록하고 본인 확인을 완료합니다.
- Tencent Cloud 계정 생성 방법:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Sign up for a Tencent Cloud account</a></div>
- 실명 인증 방법:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

## 작업 단계
1. [TDSQL for MySQL 구매 페이지](https://console.cloud.tencent.com/tdsqld/tdmysql-buy)에 로그인하여, 각 항목의 구성 정보를 필요에 따라 선택하고 오류가 없는지 확인한 뒤, **즉시 구매**를 클릭합니다.
 - **과금 방식**: 정액 과금제 및 종량제가 지원됩니다.
    - 장기 수요가 안정적인 비즈니스라면 정액 과금제를 권장합니다.
    - 비즈니스의 요청량이 순간적으로 크게 변동하는 경우 종량제를 권장합니다.
 - **리전**: TDSQL for MySQL 인스턴스를 배포할 리전을 선택합니다. 연결할 CVM 인스턴스와 동일한 리전을 사용하는 것이 좋습니다. 다른 리전의 Tencent Cloud 서비스는 사설망을 통해 서로 통신할 수 없습니다. 리전은 구매 후 수정할 수 없습니다.
 - **네트워크 유형**: TDSQL for MySQL 인스턴스가 있는 네트워크를 선택합니다. 연결할 CVM 인스턴스와 동일한 리전에서 동일한 VPC를 선택하는 것이 좋습니다. 그렇지 않으면 사설망을 통해 CVM 인스턴스와 데이터베이스에 연결할 수 없습니다.
 - **인스턴스 버전**: 자세한 내용은 [인스턴스 아키텍처](https://intl.cloud.tencent.com/document/product/1042/33319)를 참고하십시오.
 - **소스/복제본 AZ**: 다른 소스 및 복제본 AZ를 선택하여 장애 및 AZ 중단으로부터 데이터베이스를 보호합니다.
 - **커널 버전**: MySQL 5.6 커널은 분산 트랜잭션(XA)을 지원하지 않습니다. 이 기능이 필요한 경우 v5.7을 선택하십시오. 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product/1042/38142)를 참고하십시오.
 - **샤드 수량/사양/디스크**: 데이터 왜곡을 방지하기 위해 2개, 4개 또는 8개의 샤드를 권장합니다. 샤드 설정에 대한 자세한 내용은 [인스턴스 설정 및 샤드 설정 선택](https://intl.cloud.tencent.com/document/product/1042/33354)을 참고하십시오.
 - **프로젝트**: TencentDB 인스턴스가 속한 프로젝트를 선택합니다. 기본 프로젝트가 사용됩니다.
 - **태그**: 태그를 사용하여 리소스를 분류하고 관리합니다. 자세한 내용은 [Overview](https://intl.cloud.tencent.com/document/product/651/13334)를 참고하십시오.
 - **보안 그룹**: 보안 그룹의 생성 및 관리에 관한 내용은 [보안 그룹 설정](https://intl.cloud.tencent.com/document/product/1042/33348)을 참고하십시오.
 - **인스턴스 이름**: 지금 또는 나중에 인스턴스의 이름을 지정합니다.
 - **지원되는 문자 세트**: UTF8, LATIN1, GBK, UTF8MB4 및 GB18030이 지원됩니다.
 - **테이블 이름 대소문자 구분**: 대소문자 구분(lower_case_table_names = 0) 또는 대소문자 구분하지 않음(lower_case_table_names = 1)을 선택합니다. 초기화 매개변수이며 데이터베이스가 초기화된 후에는 수정할 수 없습니다.
 - **강제 동기화 사용**: 강제 동기화(다운그레이드 가능) 및 비동기화가 지원됩니다. 자세한 내용은 [강제 동기화](https://intl.cloud.tencent.com/document/product/1042/33318)를 참고하십시오.
 - 과금에 대한 자세한 내용은 [제품 가격](https://intl.cloud.tencent.com/document/product/1042/35777)을 참고하십시오.
2. 결제 후 인스턴스 리스트로 되돌아갑니다. 인스턴스 상태가 **실행 중**으로 변경되면, 정상적으로 사용할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4ad820a453b3b55b9b3039b4ab13655a.png)

## 후속 작업
사설망 또는 공중망 주소에서 MySQL용 TDSQL 인스턴스에 연결하는 방법에 대한 자세한 내용은 [인스턴스 연결](https://intl.cloud.tencent.com/document/product/1042/33338)을 참고하십시오.

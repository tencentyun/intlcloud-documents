
본 문서는 콘솔을 통한 MySQL 인스턴스 생성 방법에 대해 소개합니다.

## 전제 조건
Tencent Cloud에 회원가입 및 실명 인증을 완료해야 합니다.
- Tencent Cloud 계정이 없을 경우
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Tencent Cloud 계정 생성</a></div>
- 실명 인증을 완료해야 할 경우
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

## 작업 절차
1. [MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 로그인하여, 각 항목의 구성 정보를 필요에 따라 선택하고 오류가 없는지 확인한 뒤, **즉시 구매**를 클릭합니다.
 - **과금 방식**: 종량제 지원.
    - 서비스량이 급격히 변동하는 시나리오는 종량제 선택을 권장합니다.
 - **리전**: MySQL을 배포할 비즈니스의 리전을 선택합니다. 서로 다른 리전의 클라우드 서비스는 내부 네트워크도 각자 다르므로 CVM과 동일한 리전을 선택할 것을 권장하며, 구매한 후에는 변경할 수 없습니다.
  - **아키텍처**: 이중 노드, 삼중 노드 버전을 제공합니다. 각 아키텍처에 관한 소개는 [데이터베이스 아키텍처](https://intl.cloud.tencent.com/document/product/236/38328)를 참고하십시오.
 - **마스터 가용존 및 슬레이브 가용존**: 선택한 마스터/슬레이브 가용존이 서로 다를 경우(즉 [멀티 가용존 배포](https://intl.cloud.tencent.com/document/product/236/8459), 장애가 발생하거나 가용존이 중단되어도 데이터베이스를 보호할 수 있습니다.
 >?마스터/슬레이브 기기가 서로 다른 가용존에 있으면, 네트워크 동기화가 2~3ms 가량 딜레이 될 수 있습니다. 
 - **격리 정책**: 범용형, 전용형을 지원합니다. 자세한 내용은 [격리 정책](https://intl.cloud.tencent.com/document/product/236/39794)을 참고하십시오.
 - **인스턴스 사양**: 범용형과 전용형 2가지의 인스턴스 사양을 지원합니다. 
    - 범용형: 할당된 메모리와 디스크를 단독으로 사용하고, 동일 베어메탈의 기타 범용 규격 인스턴스와 CPU 리소스를 공유합니다. 
    - 전용형: 할당된 CPU, 메모리와 스토리지 리소스를 전용합니다. 
 - **디스크**: 디스크 공간은 MySQL 실행 시 필요한 파일을 저장합니다. 
 - **데이터 복사 방식**: 비동기화 복사, 반동기화 복사, 강제 동기화 복사 3가지 방식을 제공하며, 자세한 설명은 [데이터베이스 인스턴스 복사](https://intl.cloud.tencent.com/document/product/236/7913)를 참고하십시오.
 - **네트워크**: TencentDB for MySQL 소속 네트워크는 CVM과 동일 리전에 있는 동일 VPC를 선택할 것을 권장합니다. 그러지 않으면, 내부 네트워크를 통해 CVM과 데이터베이스를 연결할 수 없으며, 기본 설정은 Default-VPC(기본)이 됩니다.
 - **보안 그룹**: 보안 그룹의 생성 및 관리에 관한 내용은 [CDB 보안 그룹](https://intl.cloud.tencent.com/document/product/236/14470)을 참고하십시오.
 >?보안 그룹의 Inbound rule은 MySQL 인스턴스의 3306 포트를 개방해야 합니다. MySQL 내부 네트워크의 기본 포트는 3306이며, 사용자 정의 포트도 지원합니다. 만약 기본 포트 번호를 수정했다면, 보안 그룹에서 새로운 포트 정보를 다시 개방해야 합니다.
 - **매개변수 템플릿**: 제공된 시스템 매개변수 템플릿 외에도 사용자 정의 매개변수 템플릿을 생성할 수 있습니다. 자세한 내용은 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참고하십시오.
  - **알람 정책**: 클라우드 서비스 상태 변경 시 경고를 트리거하고 관련 메시지를 발송하는 알람을 생성합니다. 자세한 내용은 [알람 정책](https://intl.cloud.tencent.com/document/product/236/8457)을 참고하십시오.
 - **지정 항목**: 데이터베이스 인스턴스에 소속된 항목을 선택할 수 있으며, 디폴트가 기본 항목으로 설정되어 있습니다.
 - **구매 수량**: 한 사용자가 각 가용존에서 구매할 수 있는 총 종량제 인스턴스 수량은 10대입니다.
2. 결제를 완료하고 인스턴스 리스트로 돌아온 뒤 **발송 중**(약 3~5분 정도 소요될 수 있으니 기다려 주시기 바랍니다)으로 표시된 것을 확인할 수 있으며, 인스턴스 상태가 **미초기화**로 바뀌었다면 초기화 작업을 진행할 수 있습니다.

## 후속 작업
콘솔을 통해 MySQL 인스턴스를 초기화합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/3128)를 참고 바랍니다.

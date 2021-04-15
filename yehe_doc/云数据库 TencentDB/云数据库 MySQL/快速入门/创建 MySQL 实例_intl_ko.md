
본 문서는 콘솔을 통한 MySQL 인스턴스 생성 방법에 대해 소개합니다.

## 전제 조건
Tencent Cloud의 계정을 생성한 후 실명 인증을 완료합니다.
- Tencent Cloud 계정이 없는 경우:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Tencent Cloud 계정 생성하기</a></div>
- 실명 인증이 필요한 경우:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

## 작업 순서
1. [MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 로그인하여 각 항목의 설정 정보를 알맞게 선택하고 정보가 올바른지 확인한 뒤 [즉시 구매]를 클릭합니다.
 - **과금 방식**: 종량제를 지원합니다.
    - 작업량이 급격히 변동하는 시나리오의 경우 종량제를 권장합니다.
 - **리전**: 작업에 필요한 MySQL을 배포할 리전을 선택합니다. CVM과 동일한 리전을 선택하시길 권장합니다. 클라우드 서비스의 리전이 다를 경우, 내부 네트워크가 연결되지 않으므로 구매 후 변경할 수 없습니다.
  - **아키텍처**: 단일 노드, 이중 노드, 3중 노드 버전을 제공합니다. 각 아키텍처에 관한 소개는 [데이터베이스 아키텍처](https://intl.cloud.tencent.com/document/product/236/38328)를 참조하십시오.
 - **마스터 가용존 및 슬레이브 가용존**: 선택한 마스터/슬레이브 가용존이 서로 다른 경우([다중 가용존 배포](https://intl.cloud.tencent.com/document/product/236/8459)), 장애가 발생하거나 가용존이 중단되어도 데이터베이스를 보호할 수 있습니다.
 >?마스터/슬레이브 기기가 서로 다른 가용존에 있는 경우, 네트워크 동기화가 2ms~3ms 가량 더 딜레이될 수 있습니다.
 - **격리 정책**: 기본형, 범용형, 전용형을 지원합니다. 자세한 내용은 [격리 정책](https://intl.cloud.tencent.com/document/product/236/39794)을 참조하십시오.
 - **네트워크**: TencentDB for MySQL 소속 네트워크는 CVM과 같은 리전에 있는 동일한 사설 네트워크를 선택하는 것이 좋습니다. 그렇지 않으면 내부 네트워크를 통해 CVM과 데이터베이스를 연결할 수 없으며, 'Default-VPC(기본)'로 기본 설정됩니다.
 - **보안 그룹**: 보안 그룹 생성 및 관리에 관한 내용은 [CDB 보안 그룹](https://intl.cloud.tencent.com/document/product/236/14470)을 참조하십시오.
 >?보안 그룹의 Inbound rule은 MySQL 인스턴스의 3306 포트를 개방해야 합니다. MySQL 내부 네트워크의 기본 포트는 3306이지만, 사용자 정의 포트도 지원합니다. 기본 포트 번호를 수정하려면, 보안 그룹에서 MySQL의 새로운 포트 정보를 개방해야 합니다.
 - **매개변수 템플릿**: 제공된 시스템 매개변수 템플릿 외에도 사용자 정의 매개변수 템플릿을 생성할 수 있습니다. 자세한 내용은 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참조하십시오.
  - **알람 정책**: 클라우드 서비스 상태 변경 시 경고를 트리거하고 관련 메시지를 발송하는 알람을 생성합니다. 자세한 내용은 [알람 정책](https://intl.cloud.tencent.com/document/product/236/8457)을 참조하십시오.
 - **프로젝트 지정**: 데이터베이스 인스턴스에 포함할 프로젝트를 선택합니다. 기본값은 기본 프로젝트로 설정되어 있습니다.
 - **구매 수량**: 한 가용존에서 사용자가 구매할 수 있는 종량제 인스턴스의 수량은 총 10개입니다.
2. 결제 완료 후 인스턴스 리스트가 반환되면 '발주 중'(약 3~5분이 소요되니 잠시 기다려 주십시오) 표시가 뜨고, 인스턴스 상태가 '초기화되지 않음'으로 바뀌면 초기화 작업을 진행할 수 있습니다.

## 후속 작업
콘솔을 통해 MySQL 인스턴스를 초기화합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/3128)를 참조하십시오.

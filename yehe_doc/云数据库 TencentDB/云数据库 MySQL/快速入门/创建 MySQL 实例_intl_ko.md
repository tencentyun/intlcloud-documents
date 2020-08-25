
본 문서는 콘솔을 통한 MySQL 인스턴스 생성 방법에 대해 소개합니다.

## 전제 조건
Tencent Cloud에 회원가입 및 실명 인증을 완료합니다.
- Tencent Cloud 계정이 없을 경우
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Tencent Cloud 회원가입하기</a></div>
- 실명 인증을 완료해야 할 경우
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

## 작업 순서
1. [MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 로그인하여, 각 항목의 구성 정보를 필요에 따라 선택하고 착오가 없는지 확인한 뒤, [바로 구매]를 클릭합니다.
 - **과금 방식**: 종량제 지원.
    - 비즈니스 양이 급격히 변동하는 시나리오라면, 종량제를 선택하시길 권장합니다.
 - **리전**: MySQL을 배포할 비즈니스의 리전을 선택합니다. 서로 다른 리전의 클라우드 서비스는 내부 네트워크도 각자 다르므로 CVM과 동일 리전을 선택할 것을 권장하며, 구매한 후에는 변경할 수 없습니다.
 - **액티브 가용존 및 스탠바이 가용존**: 선택한 액티브 스탠바이 가용존이 서로 다를 경우(즉 [멀티 가용존 배포](https://intl.cloud.tencent.com/document/product/236/8459)), 장애가 발생하거나 가용존이 중단되어도 데이터베이스를 보호할 수 있습니다.
 >?액티브 스탠바이 기기가 서로 다른 가용존에 있으면, 네트워크 동기화 딜레이가 2~3ms가량 증가할 수 있습니다.
 - **네트워크**: TencentDB for MySQL 소속 네트워크는 CVM과 동일 리전에 있는 동일 사설 네트워크를 선택할 것을 권장합니다. 그러지 않으면, 내부 네트워크를 통해 CVM과 데이터베이스를 연결할 수 없으며, 'Default-VPC(기본)'로 기본 설정되어 있습니다.
 - **보안 그룹**: 보안 그룹의 생성 및 관리에 관한 내용은 [CDB 보안 그룹](https://intl.cloud.tencent.com/document/product/236/14470)을 참조 바랍니다.
 >?보안 그룹의 Inbound rule은 MySQL 인스턴스의 3306 포트를 개방해야 합니다. MySQL 내부 네트워크의 기본 포트는 3306이지만, 그와 동시에 사용자 정의 포트도 지원합니다. 기본 포트 번호를 수정했다면, 보안 그룹에서 새로운 포트 정보를 다시 개방해야 합니다.
 - **아키텍처**: 고가용성 버전 및 파이낸스 버전과 기본 버전을 제공하며, 각 아키텍처에 관한 소개는 [데이터베이스 아키텍처](https://intl.cloud.tencent.com/document/product/236/17136)를 참조 바랍니다.
 - **항목 지정**: 데이터베이스 인스턴스에 포함할 항목을 선택할 수 있으며, 디폴트가 기본 항목으로 설정되어 있습니다.
 - **구매 수량**: 각 가용존에서 한 사용자가 구매 가능한 종량제 인스턴스의 총 수량은 10대입니다.
2. 결제를 완료하고 인스턴스 리스트로 돌아온 뒤 "발주중"(약 5분~10분간 소요할 수 있으니 기다려 주시기 바랍니다.)으로 표시된 걸 볼 수 있고, 인스턴스 상태가 '초기화하지 않음'으로 바뀌었다면 초기화 작업을 진행할 수 있습니다.


## 후속 작업
콘솔을 통해 MySQL 인스턴스를 초기화합니다. 자세한 내용은 [MySQL 인스턴스 초기화](https://intl.cloud.tencent.com/document/product/236/3128)를 참조 바랍니다.


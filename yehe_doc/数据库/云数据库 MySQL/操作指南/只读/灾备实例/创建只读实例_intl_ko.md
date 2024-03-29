## 작업 시나리오
TencentDB for MySQL은 하나 이상의 읽기 전용 인스턴스를 생성할 수 있습니다. 이를 통해 읽기/쓰기 분리 및 단일 원본 다중 복제본 시나리오를 지원하며 데이터베이스 읽기 부하 용량을 향상시킵니다.

현재 데이터베이스 프록시가 지원되며, 읽기 전용 인스턴스를 생성한 후 데이터베이스 프록시 서비스를 구매하여 읽기/쓰기 분리 기능을 활성화할 수 있습니다. 그런 다음, 쓰기 요청을 원본 인스턴스에 자동으로 전달하고 읽기 요청을 읽기 전용 인스턴스에 전달하도록 애플리케이션에서 데이터베이스 프록시 주소를 구성할 수 있습니다.

>?
>- 읽기 전용 인스턴스 요금에 대한 내용은 [제품 가격](https://buy.intl.cloud.tencent.com/price/cdb)을 참고하십시오.
>- 읽기 전용 인스턴스는 인스턴스 세부 정보 페이지에서 고유한 내부 네트워크 주소 활성화 및 내부 IP와 포트의 사용자 정의 변경을 지원합니다.
>![](https://qcloudimg.tencent-cloud.cn/raw/667761ccccc029b2723eea47c2034186.png)

#### 기본 개념
- RO 그룹: Cloud Load Balacer(CLB) 기능이 적용된 읽기 전용 인스턴스 그룹입니다. RO 그룹에 읽기 전용 인스턴스가 여러 개 있을 경우, 사용자의 읽기 요청량을 그룹 내의 각 읽기 전용 인스턴스에 균일하게 할당할 수 있습니다. 또한, RO 그룹의 데이터베이스는 외부 IP, PORT로 액세스할 수 있습니다.
- 읽기 전용 인스턴스: 읽기 요청을 지원하는 단일 노드(복제본 미포함) 인스턴스입니다. 읽기 전용 인스턴스는 단독으로 존재할 수 없으며, 각 읽기 전용 인스턴스는 모두 특정 RO 그룹에 속합니다.

#### 기초 아키텍처
MySQL 원본-복제본 binlog 동기화 기능은 읽기 전용 인스턴스에 채택되어 원본 인스턴스(원본 데이터베이스)의 변경 사항을 모든 읽기 전용 인스턴스에 동기화할 수 있습니다. 읽기 전용 인스턴스의 단일 노드 아키텍처(복제본 없음)가 주어지면 실패한 읽기 전용 인스턴스를 복원하려는 반복적인 시도가 이루어집니다. 따라서 더 높은 가용성을 위해 읽기 전용 인스턴스 보다 RO 그룹을 선택하는 것이 좋습니다.
>!RO 그룹에 읽기 전용 인스턴스가 하나만 있는 경우 단일 장애점이 존재할 수 있으며, 이 RO 그룹은 TencentDB for MySQL 서비스의 전체 가용성 계산에 포함되지 않습니다. 단일 읽기 전용 인스턴스는 가용성 SLA 보장을 제공하지 않으므로, RO 그룹의 가용성을 보장하기 위해 RO 그룹에 최소 2개의 읽기 전용 인스턴스를 구매하는 것이 좋습니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/e8000e0fae60f2f8ff884bf47d6babb0.png)

## 기능 제한
- 클라우드 디스크 버전의 단일 노드 인스턴스에 대해서는 읽기 전용 인스턴스를 생성할 수 없습니다.
- **1GB 메모리, 50GB 디스크 및 그 이상의 사양과 더불어 MySQL 5.6 이상 버전 및 InnoDB 엔진 2노드, 3노드** 원본 인스턴스만 읽기 전용 인스턴스를 구매할 수 있습니다. 원본 인스턴스의 사양이 낮은 경우, 먼저 사양을 업그레이드하시기 바랍니다.
- 읽기 전용 인스턴스의 최저 사양은 1GB 메모리, 50GB 디스크이며, 기존에 구매한 원본 인스턴스의 스토리지 사양보다 크거나 같아야 합니다.
- 원본 인스턴스당 읽기 전용 인스턴스를 최대 5개 생성할 수 있습니다.
- 백업, 롤백을 지원하지 않습니다.
- 데이터터를 읽기 전용 인스턴스에 마이그레이션할 수 없습니다.
- 데이터베이스를 생성/삭제할 수 없으며, phpMyAdmin(PMA)을 지원하지 않습니다.
- 계정을 생성/삭제할 수 없으며, 계정에 계정 및 비밀번호 수정 권한이 없습니다.

## 주의 사항
- 읽기 전용 인스턴스는 계정과 데이터베이스를 점검하지 않고, 원본 인스턴스로부터 동기화합니다.
- MySQL 버전이 5.6이지만 GTID가 활성화되지 않은 경우 읽기 전용 인스턴스를 생성하기 전에 먼저 콘솔에서 GTID를 활성화해야 합니다.
GTID 활성화 작업은 시간이 오래 걸리며 인스턴스 연결이 몇 초 동안 끊어집니다. 사용량이 적은 시간에 작업을 진행하고 데이터베이스에 액세스하는 프로그램에 재연결 메커니즘을 추가하는 것이 좋습니다.
- 읽기 전용 인스턴스는 InnoDB 엔진만 지원합니다.
- 여러 읽기 전용 인스턴스 간의 데이터 불일치는 읽기 전용 인스턴스와 원본 인스턴스 간의 데이터 동기화 지연으로 인해 발생할 수 있습니다. 콘솔에서 지연을 확인할 수 있습니다.
- 읽기 전용 인스턴스 사양은 원본 인스턴스와 다를 수 있으며, 부하 상황에 따라 유동적으로 업그레이드할 수 있습니다. 동일한 RO 그룹 내 읽기 전용 인스턴스 사양은 서로 일치하는 것이 좋습니다.

## 작업 단계
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb/ )에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 인스턴스 상세 페이지에서 **인스턴스 아키텍처**중의 **읽기 전용 인스턴스 추가**를 클릭하거나 읽기 전용 인스턴스 페이지에서 **생성**을 클릭하여 구매 페이지로 이동합니다. 
3. 구매 페이지에서 읽기 전용 인스턴스에 상응하는 설정을 선택하고, 착오가 없는지 확인한 뒤 **즉시 구매**를 클릭합니다.
>?읽기 전용 인스턴스와 원본 인스턴스의 만료 기간을 동일하게 설정하려면 [연장 관리 콘솔](https://console.cloud.tencent.com/account/renewal)에서 만료일을 통일시킬 수 있으며, 자세한 작업 방식은 [Renewal Management](https://intl.cloud.tencent.com/document/product/555/7454)를 참고하십시오.
>
 - **RO 그룹 지정**: 시스템 자동 할당, 신규 RO 그룹 및 기존 RO 그룹을 지원합니다.
    - 자동 시스템 할당: 한번에 여러 개의 인스턴스를 구매할 경우, 각 인스턴스에 독립된 RO 그룹이 1개씩 할당됩니다. 가중치 할당 방식은 시스템 자동 할당으로 설정됩니다.
    - RO 그룹 생성: 한번에 여러 개의 인스턴스를 구매할 경우 모두 이 RO그룹에 할당됩니다. 가중치 할당 방식은 시스템 자동 할당으로 설정됩니다.
    - 기존 RO 그룹: 기존 RO 그룹을 지정하고, 한 번에 여러 인스턴스를 구매하는 경우 이 RO 그룹에 모두 할당됩니다.
    가중치 할당 방식은 RO 그룹 설정과 동일하며, 시스템에서 RO 그룹이 자동으로 할당되도록 설정하면 구매 사양에 따라 RO 그룹이 자동으로 추가되며, 사용자 지정 할당인 경우 기본 가중치는 0입니다.
		동일한 RO 그룹의 인트라넷 주소가 동일하므로 VPC 네트워크는 동일한 보안 그룹 설정을 공유합니다. RO 그룹을 지정하면 구매 시 보안 그룹을 더 이상 커스터마이징할 수 없습니다.
 - **지연된 RO 인스턴스 제거**: 이 옵션은 제거 정책 활성화 여부를 나타냅니다. 지연이 임계값을 초과할 때 읽기 전용 인스턴스가 제거되면 비활성화되고 가중치는 자동으로 0으로 설정되며 경고 알람이 전송됩니다(읽기 전용 인스턴스 제거 알람 및 수신자 구성 방법에 대한 자세한 내용은 [알람 정책](https://intl.cloud.tencent.com/document/product/236/8457) 참고). 지연이 임계값 아래로 떨어지면 인스턴스가 RO 그룹에 다시 추가됩니다. 이 옵션의 활성화 여부에 관계없이 인스턴스 장애로 인해 제거된 읽기 전용 인스턴스는 복구된 후 RO 그룹에 다시 추가됩니다.
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
4. 구매 완료 후 인스턴스 리스트로 되돌아갑니다. 인스턴스 상태가 **실행 중**으로 변경되면, 정상적으로 사용할 수 있습니다.

## FAQ
#### 읽기 전용 인스턴스 제거 규칙은 무엇입니까?
지연된 RO 인스턴스 제거가 활성화된 후 RO 그룹은 지연 임계값과 최소 RO 인스턴스 값을 기반으로 제거 규칙을 결정합니다. 읽기 전용 인스턴스의 지연이 임계값에 도달하면 제거 및 비활성화되며, 사용자에게 알람이 전송되고 가중치가 0으로 설정됩니다. 지연이 임계값 아래로 떨어지면 RO 그룹으로 반환됩니다.
- 지연 임계값: 읽기 전용 인스턴스에 대한 지연 임계값을 설정합니다. 임계값을 초과하면 인스턴스가 RO 그룹에서 제거됩니다.
- 최소 RO 인스턴스: 읽기 전용 그룹에서 유지해야 하는 최소 인스턴스 수입니다. 읽기 전용 그룹에 인스턴스가 더 적거나 같은 경우 지연 임계값을 초과하더라도 인스턴스가 제거되지 않습니다.

#### 읽기 전용 인스턴스가 폐기/반환되면 원본 인스턴스에 어떤 영향을 미치나요?
읽기 전용 인스턴스의 폐기/반환은 원본 인스턴스에 영향을 미치지 않습니다.




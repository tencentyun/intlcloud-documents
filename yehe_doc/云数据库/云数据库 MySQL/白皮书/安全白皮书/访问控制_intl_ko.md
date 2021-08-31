TencentDB for MySQL은 데이터베이스 Manage Account, CAM, Security Group 등을 통해 액세스 제어를 할 뿐 아니라 MySQL의 데이터 보안성을 보장합니다. 

### 데이터베이스 Manage Account
TencentDB for MySQL은 콘솔이나 API로 [데이터베이스 계정 생성](https://intl.cloud.tencent.com/document/product/236/31900) 뿐 아니라 데이터베이스 계정에 데이터 분할 정도에 대한 관리 권한을 부합니다. 권한 최소화의 권한 부여 원칙을 적용함으로써 데이터베이스의 데이터 보안을 보장할 것을 권장합니다.

### CAM
[CAM](https://intl.cloud.tencent.com/document/product/598/10583)은 사용자가 Tencent Cloud 계정에서 리소스 액세스 권한을 안전하게 관리하는 데 주로 사용합니다. CAM을 통하여 사용자(그룹)를 생성, 관리 및 폐기할 수 있으며, 신분 관리 및 정책 관리를 통해 지정 사용자가 사용 가능한 Tencent Cloud 리소스를 제어함으로써 권한 분리의 목적을 이룰 수 있습니다.

### 보안 그룹
[보안 그룹](https://intl.cloud.tencent.com/document/product/236/14470)은 사용자의 MySQL 네트워크 보안 액세스 제어를 실현하는 데 주로 사용됩니다. 보안 그룹은 스테이트풀의 필터 기능이 포함된 가상 방화벽의 일종으로, 단일 또는 다중 클라우드 데이터베이스의 네트워크 액세스 제어 설정에 사용되며 Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 방법입니다.

보안 그룹은 하나의 로직 그룹으로, 동일한 리전 내에서 같은 수준의 네트워크 보안 격리가 필요한 클라우드 데이터베이스 인스턴스를 동일한 보안 그룹에 추가할 수 있습니다. 보안 그룹 내에서는 규칙이 일치하므로 보안 그룹 규칙을 변경할 경우 MySQL 인스턴스를 재시작할 필요가 없으며, 보안 그룹 규칙을 수정하면 즉시 적용됩니다. 



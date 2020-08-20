### TencentDB for MySQL 인스턴스에 어떻게 연결하나요?
MySQL 인스턴스 연결 방식은 다음과 같습니다.
- **내부 네트워크 연결**: CVM을 통해 CDB의 내부 네트워크 주소에 직접 연결합니다. 이 방식은 내부 고속 네트워크를 사용하므로 네트워크 속도가 빠르고 딜레이가 낮습니다.
CVM 과 데이터베이스의 계정이 동일해야 하며, 동일한 [VPC](https://intl.cloud.tencent.com/zh/document/product/215/535) 내(동일한 리전)에 있거나 기본 네트워크가 동일해야 합니다. 
- **외부 네트워크 연결**: 내부 네트워크를 통해 연결할 수 없을 때는, 외부 네트워크 주소로 TencentDB for MySQL에 연결할 수 있으나, 외부 네트워크 주소를 수동으로 활성화해야 합니다. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 상세 페이지에서 조회할 수 있으며 불필요한 경우 비활성화할 수 있습니다.

자세한 내용은 [MySQL 인스턴스 연결](https://intl.cloud.tencent.com/zh/document/product/236/3130)을 참조 바랍니다.

### 내부/외부 네트워크 주소는 어떻게 조회하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 상세 페이지에서 조회할 수 있습니다.

### 외부 네트워크 주소는 어떻게 활성화하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 상세 페이지에서 '외부 네트워크 주소'를 활성화합니다.

### 외부 네트워크의 연결 속도가 느릴 경우 어떻게 해야 하나요?
내부 네트워크로 연결하시길 권장합니다. 내부 네트워크를 사용하면 연결 속도가 빨라지며, 딜레이가 감소합니다. 내부 네트워크 연결에 대한 자세한 내용은 [MySQL 인스턴스 연결](https://intl.cloud.tencent.com/zh/document/product/236/3130)을 참조 바랍니다.

### CVM과 TencentDB for MySQL을 직접 내부 네트워크를 사용해 연결할 수 있나요?
1. 다음의 조건을 만족해야만 내부 네트워크를 사용하여 연결할 수 있습니다.
CVM 과 데이터베이스의 계정이 동일해야 하며, 동일한 [VPC](https://intl.cloud.tencent.com/zh/document/product/215/535) 내(동일한 리전)에 있거나 기본 네트워크가 동일해야 합니다. 
2. VPC 또는 기본 네트워크가 동일한지 판단하는 방법은 다음과 같습니다.
 - CVM의 네트워크로 [콘솔](https://console.cloud.tencent.com/cvm/instance)의 인스턴스 리스트 혹은 상세 페이지를 조회할 수 있어야 합니다.
 - TencentDB for MySQL의 네트워크로 [콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 리스트 혹은 상세 페이지를 조회할 수 있어야 합니다.

### CVM과 TencentDB for MySQL을 내부 네트워크로 연결할 수 없는 경우 어떻게 해야 하나요?
우선 [원클릭 연결 진단 툴](https://intl.cloud.tencent.com/zh/document/product/236/31927)을 사용하여 문제를 진단하고, 결과 보고에 따라 [연결 불가 관련 시나리오]에서 적합한 솔루션을 찾아보시길 권장합니다.

### CVM과 TencentDB for MySQL이 서로 다른 리전(예: CVM은 광저우, MySQL은 상하이)에 있을 때 내부 네트워크로 액세스할 수 있나요?
내부 네트워크로 액세스할 수 없습니다.

### CVM과 TencentDB for MySQL이 동일한 리전에 있지만 가용존이 서로 다를 경우(예: CVM은 상하이 2존, MySQL은 상하이 1존) 내부 네트워크로 연결할 수 있나요?
CVM 과 TencentDB for MySQL가 동일한 리전에 있다고 해도, VPC가 동일한지 여부는 명확하지 않습니다.
- 가용존은 다르지만 VPC가 동일할 경우 내부 네트워크로 연결할 수 있습니다.
- VPC가 동일하지 않을 경우(예: CDB는 VPC1, 다른 CDB는 VPC2)에는 내부 네트워크로 연결할 수 없습니다.

### 서로 다른 계정에 위치한 CVM과 TencentDB for MySQL을 내부 네트워크로 액세스할 수 있나요?
액세스할 수 없습니다. CVM과 MySQL이 반드시 동일한 계정에 있어야 내부 네트워크로 액세스할 수 있습니다.

### CVM과 TencentDB for MySQL의 계정과 VPC 모두 동일하여 내부 네트워크 연결 조건(동일 계정 사용 및 동일 VPC에 속함)에 부합함에도 연결할 수 없는 경우 어떻게 해야 하나요?
다음의 두 가지 방면에서 문제를 진단 및 처리할 수 있습니다.
- 보안 그룹의 설정이 정확한지 확인합니다.
- 데이터베이스의 계정 호스트 구성이 정확한지 확인합니다.

<span id = "sytyzysjk"></span>
### telnet을 사용하여 CDB의 네트워크 포트 연결이 정상임을 인증한 후에도, CVM에서 명령 라인을 통해 CDB에 로그인할 때 오류 메시지가 출력된다면 어떻게 처리하나요?
- 'ERROR 1045(28000):Access denied for user...와 같은 안내 문구가 나타난다면, 입력한 CDB 계정이나 비밀번호가 정확한지 확인하시기 바랍니다. 비밀번호를 잊어버렸을 경우 [비밀번호 재설정](https://intl.cloud.tencent.com/zh/document/product/236/31901)을 참조 바랍니다. 정확한 정보를 입력해도 계속 오류가 발생한다면, [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 관리 페이지의 [데이터베이스 관리]>[계정 관리]에서 연결 IP에 제한이 있는지 조회하시기 바랍니다.

- 'ERROR 1040(00000):Too many connections'와 같은 안내 문구가 나타난다면, CDB의 인스턴스가 현재 최대 연결 수 제한을 초과했음을 의미합니다. 원인과 솔루션은 다음과 같습니다.
i. sleep 스레드 수가 너무 많을 경우에는 콘솔에서 wait_timeout 및 interactive_timeout 매개변수 값을 낮춰야 합니다.
ii. 슬로우 쿼리가 많이 쌓여 있을 경우에는 10s로 기본 설정되어 있는 long_query_time의 매개변수 값을 1s - 2s로 설정한 뒤 슬로우 쿼리 로그를 모니터링 합니다.
iii. sleep 스레드 수도 적고 쌓인 슬로우 쿼리도 없다면 콘솔에서 max_connections의 매개변수 값을 높입니다.
- 'ERROR 2003 (HY000): Can't connect to MySQL server...'와 같은 안내 문구가 나타난다면, 입력한 CDB의 IP나 포트 정보가 정확한지 확인하시기 바랍니다. 정확한 정보를 입력해도 오류가 발생할 경우엔 해당 인스턴스 콘솔의 보안 그룹 정책에서 CVM의 데이터베이스 연결 권한 유무를 확인 바랍니다.
- 데이터 마이그레이션에서 연결성 테스트 미통과 시, 마이그레이션 프록시 IP가 보안 정책을 활성화했는지 여부를 조회하시기 바랍니다.
- 사용자가 init_connect 매개변수를 다음 예시와 같이 설정했을 경우: mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';
이렇게 하면 super 권한이 없는 모든 사용자의 연결이 트리거되고, 데이터베이스에 연결할 때마다 db_monitor.accesslog 테이블에 기록이 삽입됩니다. db_monitor.accesslog 테이블에 제출되지 않은 트랜잭션 또는 관련 잠금이 대기하고 있다면, insert into db_monitor.accesslog 테이블의 모든 작업이 멈추고, super 권한이 없는 사용자는 연결이 끊겨 CDB의 정상적인 사용이 불가능해지므로, init_connect 매개변수는 신중히 설정하시기 바랍니다.





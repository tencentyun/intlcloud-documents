### TencentDB for MySQL 인스턴스를 생성하는 데 얼마나 걸립니까?
일반적으로 TencentDB 인스턴스를 생성하는 데 10분 미만이 걸립니다. 읽기 전용 인스턴스를 생성하는 데 걸리는 시간은 원본 인스턴스의 데이터 볼륨에 따라 다릅니다. 데이터 볼륨이 클수록 시간이 길어집니다.
인스턴스를 생성하는 데 시간이 오래 걸린다면 문제가 있는 것일 수 있습니다. 도움이 필요한 경우 [문의하기](https://intl.cloud.tencent.com/document/product/236/32996)로 문의하십시오.

### 데이터베이스를 반환하려면 어떻게 해야 하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후 인스턴스 리스트의 **작업** 열에서 **더보기** > **폐기/반품** 또는 **폐기/반품 및 환불**을 선택하여 인스턴스를 반환할 수 있습니다. 자세한 내용은 [인스턴스 폐기](https://intl.cloud.tencent.com/document/product/236/31895)를 참고하십시오.

[](id:shilixiaohui)
### TencentDB for MySQL 인스턴스가 폐기되면 어떻게 됩니까?
반환된 인스턴스는 7일(정액 과금제 인스턴스) 또는 1일(종량제 인스턴스) 동안 휴지통에 보관됩니다. 보관 기간 동안 휴지통에서 복원할 수 있습니다.

[](id:zhanghaomima)
### 실수로 계정을 삭제하거나 비밀번호를 잊어버린 경우 어떻게 해야 하나요?
- 실수로 계정을 삭제한 경우 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동한 후 **데이터베이스 관리** > **계정 관리** > **계정 생성**을 클릭하거나 sql 명령을 사용하여 계정을 생성할 수 있습니다. 자세한 내용은 [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)을 참고하십시오.
- root 비밀번호를 잊은 경우 **데이터베이스 관리** > **계정 관리** 페이지에서 해당 계정을 찾은 후 작업 열에서 자세히 > **비밀번호 재설정**을 클릭하십시오. 자세한 내용은 [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)을 참고하십시오.
상기 작업은 [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) API를 통해서도 수행할 수 있습니다.

### TencentDB for MySQL에 대한 최대 연결 수는 몇 개입니까? 어떻게 수정합니까?
TencentDB for MySQL의 최대 연결 수는 콘솔에서 확인할 수 있습니다. 연결 수가 너무 많으면 최대값을 직접 늘리기보다 먼저 원인을 찾아 문제를 해결하는 것이 좋습니다.
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다. **데이터베이스 관리** > **매개변수 설정** 페이지를 선택하고 `max_connections` 매개변수를 수정합니다.

### MySQL 인스턴스 모니터링에서 max_connections 값이 실제 현재 최대 연결 수가 아닌 항상 1000으로 표시되는 이유는 무엇입니까?
max_connections는 인스턴스 모니터링에서 허용되는 최대 연결 수(1 - 100000)를 나타냅니다. **열린 연결 수**는 현재 사용 가능한 연결 수를 의미하며 실시간으로 변경되는 값입니다.

### 디스크 용량이 부족하다는 것을 어떻게 알 수 있습니까?
모니터링 센터는 TencentDB 인스턴스의 디스크 용량을 모니터링합니다. 디스크 사용률이 90% 이상이면 SMS 및 이메일 알람이 트리거됩니다. 이러한 알람을 수신하도록 Cloud Monitor에서 알람 수신자를 설정할 수 있습니다. (설정 방법에 대한 자세한 내용은 [알람 정책(Cloud Monitoring)](https://intl.cloud.tencent.com/document/product/236/8457)을 참고하십시오.)

### TencentDB for MySQL 인스턴스가 초기화된 후 테이블 이름의 대소문자 구분을 어떻게 수정합니까?
데이터베이스의 `lower_case_table_names` 매개변수를 조정해야 합니다.
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 ID 를 클릭하여 인스턴스 관리 페이지로 이동합니다. **데이터베이스 관리** > **매개변수 설정**을 선택한 다음 `lower_case_table_names` 매개변수를 수정합니다. 유효한 값은 0(대소문자 구분) 및 1(대소문자 구분 안 함)입니다.

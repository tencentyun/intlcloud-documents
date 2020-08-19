### TencentDB for MySQL을 생성하기까지 시간이 얼마나 소요되나요?
일반적으로 CDB를 생성하기까지 약 10분가량 소요됩니다. 읽기 전용 인스턴스의 생성 시간은 마스터 인스턴스의 데이터양과 관련되어 있으며, 데이터가 클수록 생성 시간도 길어집니다.
이보다 더 많은 시간이 소요된다면 생성 과정에서 문제가 발생한 것일 수 있으니 [영업 상담](https://intl.cloud.tencent.com/zh/document/product/236/32996)으로 신속히 문의 바랍니다.

### 데이터베이스를 잘못 구매했을 때는 어떻게 반품하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 Instance List의 '작업' 열에서 [더 보기]>[폐기/반품] 혹은 [폐기/반품 & 환불]을 선택하여 반품할 수 있습니다. 자세한 내용은 [인스턴스 폐기](https://intl.cloud.tencent.com/zh/document/product/236/32996)를 참조 바랍니다.

<span id = "shilixiaohui"></span>
### TencentDB for MySQL의 인스턴스를 폐기했을 경우, 어떻게 해야 하나요?
인스턴스를 반환한 후에는 일정 시간 휴지통에 보관됩니다. 정액 과금제 인스턴스는 7일, 종량제 인스턴스는 1일 동안 보관되며, 해당 시간 이내에 휴지통에서 반환한 인스턴스를 되찾아 작업을 복구할 수 있습니다.

<span id = "zhanghaomima"></span>
### 계정을 잘못 삭제했거나 비밀번호를 잊어버렸을 경우, 어떻게 해야 하나요?
- 계정을 잘못 삭제했다면 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다. [데이터베이스 관리]>[계정 관리]>[계정 생성]을 클릭하거나 sql 명령을 사용하여 생성할 수 있으며, 자세한 내용은 [계정 생성](https://intl.cloud.tencent.com/zh/document/product/236/32996)을 참조 바랍니다.
- root 비밀번호를 잃어버렸다면 [데이터베이스 관리]>[계정 관리] 페이지에서 해당하는 계정을 찾아 [비밀번호 재설정]할 수 있습니다. 자세한 내용은 [비밀번호 재설정](https://intl.cloud.tencent.com/zh/document/product/236/31901)을 참조 바랍니다.
위와 같은 작업은 [클라우드 API](https://intl.cloud.tencent.com/zh/document/product/236/31901)로도 실현할 수 있습니다.

### TencentDB for MySQL의 최대 연결 수는 얼마이고, 또 어떻게 수정하나요?
TencentDB for MySQL의 최대 연결 수는 콘솔에서 확인할 수 있습니다. 현재 연결 수가 너무 많다면 바로 최대 연결 수를 변경하지 말고, 먼저 문제를 진단한 후에 해결하시기 바랍니다.
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다. [데이터베이스 관리]>[매개변수 설정] 페이지를 선택하고 `max_connections` 매개변수를 찾아 수정합니다.


### MySQL 인스턴스 모니터링에서 max_connections의 값이 당시의 실제 최대 연결 수가 아닌 항상 1000으로 표시되는 이유는 무엇인가요?
인스턴스 모니터링에서 max_connections는 허용된 최대 연결 개수를 의미하며, 사용자 정의로 최대 15240까지 설정할 수 있습니다. [현재 열린 연결 수]는 당시의 실제 연결 수를 의미하는 것으로, 그 값이 실시간으로 변경됩니다.


### 디스크 공간이 부족한지 어떻게 확인하나요?
모니터링 센터에서 CDB의 디스크 공간에 대해 모니터링한 결과, CDB의 사용 공간이 90% 이상이라면 SMS, 이메일 형식으로 알람을 보냅니다. 따라서 Cloud Monitoring에서 상응하는 알람 수신자를 설정(설정에 관한 내용은 [알림 기능](https://intl.cloud.tencent.com/zh/document/product/236/8457)을 참조)하기만 하면 공간이 부족할 때 알림을 받을 수 있습니다.


### MySQL을 초기화한 후에 테이블의 민감도는 어떻게 수정하나요?
민감도를 수정하려면 데이터베이스의 `lower_case_table_names` 매개변수를 변경해야 합니다.
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다. [데이터베이스 관리]>[매개변수 설정] 페이지를 선택하고 `lower_case_table_names` 매개변수를 찾아 수정합니다. 0은 민감을 의미하고 1은 민감하지 않음을 의미합니다.

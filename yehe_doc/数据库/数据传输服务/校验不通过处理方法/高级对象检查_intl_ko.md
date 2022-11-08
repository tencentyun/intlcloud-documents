
## MySQL/MariaDB/Percona 확인 세부 정보
마이그레이션/고급 객체 동기화를 선택하면 DTS가 다음 내용을 확인합니다. 작업을 계속하려면 오류를 수정해야 합니다. 경고의 경우 비즈니스 위험 평가에 따라 무시하고 작업을 계속할 수 있습니다.

- 오류: 대상 인스턴스 매개변수 log_bin_trust_function_creators는 ON이어야 합니다.

- 경고:
   - 고급 객체 마이그레이션/동기화 기능이 데이터베이스/테이블 이름 변경 기능과 충돌합니다. 고급 객체를 선택한 후 데이터베이스/테이블 이름 변경을 취소해야 합니다.
   - 고급 객체로 함수 또는 저장 프로시저를 선택하면 DTS는 원본 데이터베이스의 `DEFINER`( [DEFINER = user1])에 해당하는 user1이 작업 실행 계정 user2와 동일한지 확인합니다.
     - 동일한 경우 마이그레이션/동기화 후 설정을 수정하지 마십시오.
     - 서로 다른 경우 ‘DEFINER’에서 ‘INVOKER’로 마이그레이션/동기화([INVOKER = user1])한 후 대상 데이터베이스에서 user1의 ‘SQL SECURITY’ 속성을 변경하고, 대상 데이터베이스에서 ‘DEFINER’를 작업 실행 계정 user2([DEFINER = 작업 실행 계정 user2])로 설정합니다.
     
   - 고급 객체의 마이그레이션/동기화 시간:  
     - 저장 절차 및 함수: ‘원본 데이터베이스 내보내기’ 중에 마이그레이션/동기화됩니다. 
     - 트리거 및 이벤트: 마이그레이션/동기화 작업이 없는 경우 작업이 중지되면 마이그레이션/동기화가 진행됩니다. 그렇지 않으면 **완료**를 클릭한 후 마이그레이션/동기화가 시작되며, 이 경우 전환 시간이 더 오래 걸립니다.

## 수정 방법

log_bin_trust_function_creators 매개 변수를 수정하십시오.

log_bin_trust_function_creators는 사용자가 저장된 함수를 binlog에 쓸 수 있도록 허용 여부를 제어합니다. OFF로 설정하면 SUPER 권한이 있는 사용자만 저장된 함수 생성 작업을 binlog에 쓸 수 있습니다. ON으로 설정하면 SUPER 권한이 없는 사용자도 이 작업을 수행할 수 있습니다.

오류가 발생하면 다음과 같이 문제를 해결하십시오.

1. 원본 데이터베이스에 로그인합니다.
2. 다음 명령을 실행하여 log_bin_trust_function_creators 매개변수를 수정합니다.
```
set global log_bin_trust_function_creators = ON;
```
3. 다음 명령을 실행하여 매개변수 수정이 적용되었는지 확인합니다.
```
show variables like '%log_bin_trust_function_creators%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql>  show variables like '%log_bin_trust_function_creators%';
+---------------------------------+-------+
| Variable_name                   | Value |
+---------------------------------+-------+
| log_bin_trust_function_creators | ON    |
```
4. 확인 작업을 다시 실행합니다.



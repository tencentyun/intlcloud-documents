TDSQL for MySQL에서 트랜잭션은 일반적으로 여러 물리적 노드의 데이터를 포함합니다. 이러한 트랜잭션을 분산 트랜잭션이라고 합니다.
TDSQL for MySQL은 XA 및 비XA 분산 트랜잭션 프로토콜을 지원합니다. 기본적으로 TDSQL for MySQL(커널 버전 5.7 이상)은 클라이언트가 감지할 수 없고 비분산 트랜잭션만큼 사용하기 쉬운 분산 트랜잭션을 지원합니다.
TDSQL for MySQL 분산 트랜잭션은 2단계 커밋 프로토콜(2PC)을 채택하여 트랜잭션의 원자성(Atomicity)과 일관성(Consistency)을 보장하고 Read committed, Repeatable read 및 Serializable와 같은 격리 수준을 지원합니다.

## 비 XA 분산 트랜잭션
```
begin; # 트랜잭션 시작
...    # 교차 set INSERT, DELETE, UPDATE, SELECT 및 기타 DDL이 아닌 작업
commit;    # 트랜잭션 커밋
```

## XA 분산 트랜잭션
XA 분산 트랜잭션은 인스턴스 간 트랜잭션을 나타냅니다.
```
xa begin ''; # XA 트랜잭션을 시작합니다. 트랜잭션 식별자는 시스템에서 생성하므로 빈 문자열을 전달할 수 있습니다.
...      # 교차 set INSERT, DELETE, UPDATE, SELECT 및 기타 DDL이 아닌 작업
select gtid();   # 다음 명령문에서 'xid'로 가정되는 XA 트랜잭션 식별자를 가져옵니다.
xa prepare 'xid';# 트랜잭션 준비
xa commit/rollback 'xid'; # 트랜잭션 커밋 또는 롤백
```

## 신규 트랜잭션 API
- `select gtid()` : 이 API는 분산 트랜잭션의 전역 고유 식별자를 가져오는 데 사용됩니다. 값이 반환되지 않으면 트랜잭션은 분산 트랜잭션이 아닙니다.
 - 비 XA 분산 트랜잭션 식별자의 형식: '게이트웨이id' - 'proxy 임의 값' - '일련 번호' - '타임스탬프' - '파티션 번호'(예시: c46535fe-b6-dd-595db6b8-25).
 - XA 분산 트랜잭션 식별자의 형식: 'ex' - '게이트웨이 id' - 'proxy 임의 값' - '일련 번호' - '타임스탬프' - '파티션 번호'(예시: ex-c46535fe-b6-dd-595db6b8-25).

- `select gtid_state(‘분산 트랜잭션의 전역 고유 식별자’)`: 이 API는 트랜잭션 커밋에서 예외가 발생한 후 트랜잭션 상태(기본 3초 이내)를 가져오는 데 사용됩니다. 다음 상태가 반환될 수 있습니다.
 - COMMIT: 트랜잭션이 커밋되었거나 커밋될 예정임을 나타냅니다.
 - ABORT: 트랜잭션이 롤백될 것임을 나타냅니다.
 - 빈 값: 트랜잭션 상태는 1시간 후에 지워지므로 두 가지 가능성이 있습니다.
    - 한 시간 후 쿼리의 경우 트랜잭션 상태가 지워졌음을 나타냅니다.
    - 1시간 이내 쿼리의 경우 트랜잭션이 롤백될 것임을 나타냅니다.

- `xa boost ‘분산 트랜잭션의 전역 고유 식별자’ `: 비 XA 트랜잭션 commit에서 예외가 발생한 후 트랜잭션은 특정 기간(기본적으로 30초) 동안 백엔드 구성 요소에 의해 자동으로 커밋되거나 롤백됩니다. 그렇게 오래 기다리지 않으려면 이 API를 반복적으로 호출하여 시스템이 적시에 트랜잭션을 커밋하거나 롤백하도록 할 수 있습니다. 이 API는 트랜잭션 상태(즉, 커밋 또는 롤백)를 반환합니다.

- `xa lockwait`: 이 API는 분산 트랜잭션 간의 대기 관계를 표시하는 데 사용됩니다. dot 툴을 사용하여 그래프로 변환할 수 있습니다. 

- `xa show`: 이 API는 proxy에서 활성 상태인 트랜잭션을 표시하는 데 사용됩니다.

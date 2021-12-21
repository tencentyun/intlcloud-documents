## 기능 소개
SQL 최적화는 데이터베이스 성능 최적화의 매우 중요한 부분입니다. 옵티마이저가 적절한 실행 플랜을 선택하지 못해 가져오는 영향을 피하기 위해, TXSQL은 사용자가 실행 플랜을 바인딩할 수 있는 OUTLINE 기능을 제공합니다. MySQL 데이터베이스에는 HINT를 통해 실행 플랜을 수동으로 바인딩하는 기능이 있으며, HINT 정보에는 SQL이 사용하는 최적화 규칙, 알고리즘 종류 및 데이터 스캔에 사용되는 인덱스가 종류가 포함됩니다. OUTLINE은 주로 HINT에 의존하여 쿼리 플랜을 지정합니다. 사용자가 플랜 바인딩 규칙을 추가할 수 있도록 시스템 테이블 mysql.outline을 제공하고, 스위치(cdb_opt_outline_enabled)를 사용하여 이 기능의 활성화 여부를 제어할 수 있도록 합니다.

## 지원 버전
커널 버전 MySQL 8.0 20201230 이상

## 적용 시나리오
온라인 실행 플랜에 잘못된 인덱스 선택 등 온라인 실행 플랜이 잘못되었지만, SQL 수정 및 새 버전 배포 없이 해결하고 싶은 경우.

## 성능 영향
- cdb_opt_outline_enabled가 활성화된 경우, outline에 히트되지 않은 SQL의 실행 효율은 영향을 받지 않습니다.
- outline에 히트된 SQL의 실행 효율은 일반 실행만큼 높지 않지만, 일반 outline 바인딩은 기존 플랜보다 성능이 몇 배는 더 향상됩니다.
- 스위치 사용 시 성능 저하를 유발할 수 있는 바인딩 오류를 방지하기 위해 유지보수 또는 커널 담당자와 상의해야 합니다.

## 사용 설명
OUTLINE 구문 설정은 다음과 같은 새로운 구문 형식을 채택합니다.
- OUTLINE 정보 설정: `outline "sql" set outline_info "outline";`
- OUTLINE 정보 리셋: `outline reset ""; outline reset all;`
- OUTLINE 정보 플러시: `outline flush;`

다음 schema를 예시로 OUTLINE의 주요 사용법을 설명합니다.
```
create table t1(a int, b int, c int, primary key(a));
create table t2(a int, b int, c int, unique key idx2(a));
create table t3(a int, b int, c int, unique key idx3(a));
```

| 매개변수 이름                  | 동적 | 유형 | 기본값  | 매개변수 값 범위 | 설명                |
| ----------------------- | ---- | ---- | ----- | ---------- | ------------------- |
| cdb_opt_outline_enabled | yes  | bool | fasle | true/false | outline 기능 활성화 여부 |

### OUTLINE 바인딩
OUTLINE을 직접 바인딩하는 방법은 하나의 SQL을 다른 SQL로 교체하는 것이나, SQL의 의미는 바뀌지 않았으며, 옵티마이저에게 실행 방법을 알려주기 위해 일부 HINT 정보만 추가되었습니다.
구문 형식: `outline "sql" set outline_info "outline";`이며, outline_info 뒤의 문자열은 "OUTLINE:"으로 시작해야 하고, "OUTLINE:" 뒤의 문자열은 HINT를 추가한 후의 SQL입니다. 예를 들어 SQL `select *from t1, t2 where t1.a = t2.a`의 t2 테이블에 a 열의 인덱스를 추가합니다.
```
outline "select* from t1, t2 where t1.a = t2.a" set outline_info "OUTLINE:select * from t1, t2 use index(idx2) where t1.a = t2.a";
```

### optimizer hint 바인딩
기능을 보다 유연하게 하기 위해 TXSQL은 SQL에 optimizer hint를 점진적으로 추가할 수 있으며, outline을 직접 바인딩하여 동일한 기능을 구현할 수 있습니다.
구문 형식은 `outline "sql" set outline_info "outline";`이며, outline_info 뒤의 문자열은 "OPT:"로 시작해야 하고 "OPT:" 뒤에는 optimizer hint 정보를 추가합니다. 예를 들어, s`elect *from t1 where t1.a in (select b from t2)`의 SQL에 대해 MATERIALIZATION/DUPSWEEDOUT의 SEMIJOIN을 지정합니다.
```
outline "select* from t1 where t1.a in (select b from t2)" set outline_info "OPT:2#qb_name(qb2)";
outline "select * from t1 where t1.a in (select b from t2)" set outline_info "OPT:1#SEMIJOIN(@qb2 MATERIALIZATION, DUPSWEEDOUT)";
```

기존 SQL 명령에 OPTIMIZER HINT를 추가하면 한 번에 하나의 HINT만 추가할 수 있습니다. 구문의 세 가지 사항에 유의해야 합니다.
- OPT 키워드는 " 바로 뒤에 와야 합니다.
- 바인딩할 새로운 명령은 ':'가 앞에 와야 합니다.
- 두 개의 필드(query block 번호 #optimizer hint 문자열)를 추가해야 하며 둘 사이는 #으로 구분해야 합니다(`ie. "OPT:1#max_execution_time(1000)"`).

### index hint 바인딩
기능을 보다 유연하게 하기 위해 TXSQL은 SQL에 index hint를 점진적으로 추가할 수 있으며, outline을 직접 바인딩하여 동일한 기능을 구현할 수 있습니다.
구문 형식은 `outline "sql" set outline_info "outline";`이며, outline_info 뒤의 문자열은 "INDEX:"로 시작해야 하고 "INDEX:" 뒤에는 index hint 정보를 추가합니다.
예시는 다음과 같습니다. SQL `select *from t1 where t1.a in (select t1.a from t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))`의 query block 3 데이터베이스 test 아래에 있는 t1 테이블에 USE INDEX의 인덱스 idx1을 추가합니다. 유형은 FOR JOIN입니다.
```
outline "select* from t1 where t1.a in (select t1.a from t1 where t1.b in (select t1.a from t1 left join t2 on t1.a = t2.a))" set outline_info " INDEX:3#test#t1#idx1#1#0";
```

INDEX의 HINT를 기존 SQL 명령에 추가합니다. 한 번에 하나의 HINT만 추가할 수 있습니다. 구문의 네 가지 사항에 유의해야 합니다.
- INDEX 키워드는 " 바로 뒤에 와야 합니다.
- 바인딩할 새로운 명령은 ':'가 앞에 와야 합니다.
- 5개의 필드(query block 번호 #db_name#table_name#index_name#index_type#clause)를 추가해야 합니다.
- Index_type에 3개의 값(0은 INDEX_HINT_IGNORE, 1은 INDEX_HINT_USE, 2는 INDEX_HINT_FORCE)이, clause에 3개의 값(1은 FOR JOIN, 2는 FOR ORDER BY, 3은 FOR GROUP BY)이 있어야 합니다. 둘 사이는 #으로 나눕니다(`ie. "INDEX:2#test#t2#idx2#1#0"`은 두 번째 query block의 test.t2 테이블에서 USE INDEX FOR JOIN 유형의 idx1 인덱스를 바인딩하는 것을 의미합니다).

### 특정 SQL에 해당하는 OUTLINE 정보 삭제
TXSQL은 사용자가 특정 SQL 명령의 OUTLINE 바인딩 정보를 삭제할 수 있도록 허용합니다.
구문: `outline reset "sql";`. `select *from t1, t2 where t1.a = t2.a` 의 outline 정보 삭제 예시: `outline reset "select* from t1, t2 where t1.a = t2.a";`.

### 모든 OUTLINE 정보 지우기
TXSQL은 사용자가 커널에서 모든 OUTLINE 바인딩 정보를 삭제할 수 있도록 허용합니다. 구문은 `outline reset all`이고 실행 명령은 `outline reset all;`입니다.

때때로 온라인 비즈니스에서 인덱스에 바인딩해야 하는 매우 구체적인 문제가 있습니다. 여기에서 OUTLINE을 바인딩하도록 직접 설정할 수 있습니다.
OUTLINE 설정 후 발생할 수 있는 성능 롤백을 분석하고, 허용 가능한 성능 롤백 범위 내에서 바인딩합니다. 필요에 따라 커널 담당자와 논의해야 합니다.

## 관련 매개변수 상태 설명
TXSQL은 다양한 방식으로 사용자의 SQL을 볼 수 있는 OUTLINE 바인딩을 제공하며, 우선 mysql.outline 테이블을 통해 사용자 OUTLINE 설정을 확인할 수 있습니다. 그런 다음 show cdb_outline_info와 select * from information_schema.cdb_outline_info 두 인터페이스를 통해 메모리에 있는 OUTLINE 정보를 볼 수 있습니다. SQL 변경 여부는 메모리 안에 OUTLINE 정보 존재 여부에 달려 있기 때문에 사용자는 상기 두 인터페이스로 디버깅할 수 있습니다.

mysql.outline 시스템 테이블이 새로 추가되었으며 사용자가 설정한 OUTLINE 정보 레코드가 이 테이블에 저장됩니다. 테이블 필드는 다음과 같습니다.

| 필드 이름       | 설명                                   |
| ------------ | -------------------------------------- |
| Id                | OUTLINE 정보 설정 번호                     |
| Digest         | 원본 SQL 명령 해시 값                    |
| Digest_text  | 원본 SQL 명령의 지문 정보 텍스트              |
| Outline_text | OUTLINE이 바인딩된 SQL 명령의 지문 정보 텍스트 |

show cdb_outline_info 또는 select * from information_schema.cdb_outline_info를 통해 메모리에 있는 레코드를 볼 수 있으며, SQL이 OUTLINE 레코드 바인딩 플랜을 실행합니다. 매개변수는 다음과 같습니다.

| 필드 이름  | 설명                         |
| ------- | ---------------------------- |
| origin  | 원본 SQL 명령 지문              |
| outline | OUTLINE이 바인딩된 SQL 명령 지문 |


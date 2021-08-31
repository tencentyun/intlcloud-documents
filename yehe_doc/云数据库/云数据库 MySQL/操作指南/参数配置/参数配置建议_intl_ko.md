TencentDB for MySQL은 공식 설정 기본값을 바탕으로 최적화가 진행되었으나, 인스턴스를 구매한 후 고객의 다양한 시나리오에 맞게 아래의 매개변수를 적절히 설정하시길 권장합니다.

### character_set_server
- 기본값: UTF8
- 재시작 필요 여부: 필요
- 용도: MySQL 서버의 기본 문자 세트 설정에 사용됩니다. TencentDB for MySQL에서는 LATIN1, UTF8, GBK, UTF8MB4 등의 문자 세트 4종을 제공하며, 이 중 LATIN1은 영어 문자를 지원하며 한 문자당 1바이트를 차지합니다. UTF8은 전 세계 모든 국가의 필수 문자를 포함하는 국제 인코딩으로서, 범용으로 사용할 수 있으며 한 문자당 3바이트를 차지합니다. GBK의 문자 인코딩은 2바이트로 표시되므로 영어, 중국어에 관계없이 모두 2바이트를 차지합니다. UTF8MB4는 UTF8의 상위 집합으로, 하위 집합과 완전하게 호환됩니다. 한 문자당 4바이트를 차지하며 이모티콘(emoji) 사용을 지원합니다.
- 제안: 인스턴스를 구매한 후 비즈니스에서 지원하는 데이터 형식에 맞게 적절한 문자 세트를 선택합니다. 클라이언트와 서버 간의 문자 세트 설정이 일치하지 않아 나타난 글자 깨짐 현상과 불필요한 재시작 작업을 방지하기 위해 동일한 문자 세트를 설정하시기 바랍니다.

### lower_case_table_names
- 기본값: 0
- 재시작 필요 여부: 필요
- 용도: 데이터베이스 및 테이블을 생성할 때, 스토리지 및 쿼리 시 대소문자에 민감한지 여부입니다. 해당 매개변수의 설정 값은 0, 1이며 기본값은 0입니다. 0은 데이터베이스 및 테이블 생성 시 스토리지 및 쿼리 모두 대소문자를 구분함을 의미하며, 1은 그 반대를 의미합니다.
- 제안: MySQL 데이터베이스는 대소문자에 민감하도록 기본 설정되어 있습니다. 비즈니스 수요 및 스타일에 맞게 적절히 설정하시길 권장합니다.

### sql_mode
- 기본값:
```
NO_ENGINE_SUBSTITUTION(5.6버전), ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION(5.7버전)
```
- 재시작 필요 여부: 불필요
- 용도: MySQL은 다양한 sql 모드에서 실행할 수 있으며, sql 모드에 mysql이 지원해야 하는 sql 구문, 데이터 검증 등이 정의되어 있습니다.
해당 매개변수 5.6버전의 기본 매개변수 값은 `NO_ENGINE_SUBSTITUTION`으로, 사용하는 스토리지 엔진이 비활성화되었거나 Uncompiled되어 오류가 발생함을 의미합니다. 또한 5.7버전의 기본 매개변수 값은 `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`입니다.
그중에서,
 - `ONLY_FULL_GROUP_BY`는 GROUP BY 작업 시 SELECT 칼럼, HAVING 혹은 ORDER BY 칼럼이 있다면 반드시 GROUP BY에 나타나야 하거나 GROUP BY의 함수 칼럼에 종속되어야 함을 의미합니다.
 - `STRICT_TRANS_TABLES`가 포함되어 있으면 Strict mode가 활성화되며, NO_ZERO_IN_DATE는 날짜의 월, 일에 0을 포함하도록 허용하는지, Strict mode에 영향을 받는지 여부를 결정합니다.
 - `NO_ZERO_DATE`를 포함하면 데이터베이스에서 날짜에 0을 삽입할 수 없으며, Strict mode에 영향을 받는지 여부를 결정합니다.
 - `ERROR_FOR_DIVISION_BY_ZERO`는 Strict mode에서 INSERT 혹은 UPDATE 할 때 0으로 나뉘면 오류가 발생하지만 이를 알리지 않으며, Strict mode가 아닐 때 0으로 나뉘면 MySQL이 NULL을 반환합니다.
 - `NO_AUTO_CREATE_USER`는 GRANT로 생성하여 비밀번호가 없는 사용자를 차단합니다.
 - `NO_ENGINE_SUBSTITUTION`은 사용하는 스토리지 엔진이 비활성화되었거나 Uncompiled 되어 오류가 발생함을 의미합니다.
- 제안: 각 SQL 모드에 따라 지원되는 SQL 구문이 다르므로, 비즈니스 시나리오에 및 개발 스타일에 맞게 적절히 설정하시길 권장합니다.

### long_query_time
- 기본값: 10
- 재시작 필요 여부: 불필요
- 용도: 슬로우 쿼리의 임계 시간을 정할 때 사용되며, 기본값은 10s입니다. 어느 한 쿼리의 실행 시간이 10s 및 그 이상이라면, 해당 쿼리의 실행 현황이 슬로우 로그에 기록되어 이후에 슬로우 쿼리를 분석할 때 용이합니다.
- 제안: 비즈니스 시나리오 및 성능상의 민감도가 서로 다르므로, 향후 성능 분석을 위해 각 비즈니스 시나리오에 맞게 적절한 값을 설정하시길 권장합니다.



TencentDB for MySQL은 MySQL의 공식 기본값을 기반으로 최적화되었습니다. 비즈니스 시나리오에 따라 구매 후 TencentDB for MySQL 인스턴스에 대해 다음 매개변수를 구성하는 것이 좋습니다.

### character_set_server
- 기본값: UTF8
- 재시작 필요 여부: 필요
- 설명: MySQL 서버의 기본 문자 세트를 구성합니다. TencentDB for MySQL은 LATIN1, UTF8, GBK, UTF8MB4의 네 가지 문자 세트를 제공합니다. 그 중 LATIN1은 영어 문자를 지원하며 하나의 문자는 1바이트입니다. UTF8은 일반적으로 모든 국가에서 사용되는 모든 문자를 포함하는 국제 인코딩에 사용되며 하나의 문자는 3바이트입니다. GBK에서 모든 문자는 2바이트입니다. UTF8MB4(UTF8의 상위 집합)는 이전 버전과 완벽하게 호환되며 한 문자가 4바이트인 이모티콘(emoji)을 지원합니다.
- 권장 사항: 인스턴스를 구매한 후 비즈니스에 필요한 데이터 형식을 기반으로 적절한 문자 세트를 선택하여, 클라이언트와 서버가 동일한 문자 세트를 사용하도록 하여, 텍스트 왜곡 및 불필요한 재시작을 방지합니다.

### lower_case_table_names
- 기본값: 0
- 재시작 필요 여부: 필요
- 설명: 데이터베이스 또는 테이블을 생성할 때 저장 및 쿼리 작업의 대소문자 구분 여부를 설정할 수 있습니다. 이 매개변수는 0(대소문자 구분) 또는 1(대소문자 구분 안 함)로 설정할 수 있습니다. 기본값은 0입니다.
- 권장 사항: TencentDB for MySQL은 기본적으로 대소문자를 구분합니다. 비즈니스 요구 사항 및 사용 습관에 따라 이 매개변수를 구성하는 것이 좋습니다.

### sql_mode
- 기본값:
```
NO_ENGINE_SUBSTITUTION(5.6버전), ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION(5.7버전)
```
- 재시작 필요 여부: 불필요
- 설명: TencentDB for MySQL은 지원해야 하는 sql 구문 및 데이터 검사를 정의하는 여러 SQL 모드에서 작동할 수 있습니다.
 - v5.6에서 이 매개변수의 기본값은 `NO_ENGINE_SUBSTITUTION`입니다. 즉, 사용된 스토리지 엔진이 비활성화되거나 컴파일되지 않으면 오류가 발생합니다.
 - v5.7, 8.0에서 기본값은 `ONLY_FULL_GROUP_BY, STRICT_TRANS_TABLES, NO_ZERO_IN_DATE, NO_ZERO_DATE, ERROR_FOR_DIVISION_BY_ZERO, NO_AUTO_CREATE_USER, NO_ENGINE_SUBSTITUTION`입니다.
이 중,
   - 'ONLY_FULL_GROUP_BY'는 GROUP BY 집계 작업에서 SELECT, HAVING 또는 ORDER BY 절의 열이 GROUP BY에 나타나거나 GROUP BY 열에 종속되는 함수 열이어야 함을 나타냅니다.
   - `STRICT_TRANS_TABLES`는 SQL Strict mode를 활성화합니다. NO_ZERO_IN_DATE는 날짜의 월 또는 일 부분에 0 포함 허용 여부를 제어합니다. NO_ZERO_IN_DATE의 효과는 SQL Strict mode의 활성화 여부에 따라 다릅니다.
   - `NO_ZERO_DATE`는 날짜에 0 삽입 허용 여부를 제어합니다. 그 효과는 SQL Strict mode가 활성화 여부에 따라 다릅니다.
   - `ERROR_FOR_DIVISION_BY_ZERO`는 SQL Strict mode에서 INSERT 또는 UPDATE 프로세스 중에 데이터를 0으로 나누면 경고가 아닌 오류가 발생하고, SQL Strict mode가 아닌 경우 NULL이 반환됨을 의미합니다.
   - `NO_AUTO_CREATE_USER`는 GRANT 문이 비밀번호가 비어 있는 사용자를 생성하는 것을 금지합니다.
   - `NO_ENGINE_SUBSTITUTION`은 스토리지 엔진이 비활성화되거나 컴파일되지 않으면 오류가 발생함을 의미합니다.
- 권장 사항: 각각의 SQL 모드는 서로 다른 SQL 구문을 지원하므로 비즈니스 요구 사항과 개발 습관에 따라 구성하는 것이 좋습니다.

### long_query_time
- 기본값: 10
- 재시작 필요 여부: 불필요
- 설명: 슬로우 쿼리에 대한 시간 임계값을 정의하는 데 사용되며 기본값은 10s입니다. 쿼리 실행에 10s 이상이 소요되면 향후 분석을 위해 실행 세부 정보가 슬로우 로그에 기록됩니다.
- 권장 사항: 비즈니스 시나리오 및 성능 민감도가 다를 수 있으므로 향후 성능 분석을 고려하여 값을 설정하는 것이 좋습니다.


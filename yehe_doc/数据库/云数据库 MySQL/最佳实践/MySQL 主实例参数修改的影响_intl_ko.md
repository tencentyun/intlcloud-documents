TencentDB for MySQL 인스턴스에 대해 사용자는 [콘솔](https://console.cloud.tencent.com/cdb)에서 마스터 인스턴스의 매개변수를 수정할 수 있습니다. 이 중 일부 중요 매개변수는 부적절한 수정 방식을 사용할 경우 재해 복구 비정상 또는 데이터 불일치를 초래할 수 있습니다. 본 문서에서는 아래와 같이 매개변수 수정 후의 영향을 소개합니다.


### lower_case_table_names
**기본값**: 0
**용도: **데이터베이스 및 테이블을 생성할 때, 스토리지 및 쿼리 시 대소문자에 민감한지 여부. 해당 매개변수의 설정 값은 0, 1이며 기본값은 0입니다. 0은 데이터베이스 및 테이블 생성 시 스토리지 및 쿼리 모두 대소문자를 구분함을 의미하며, 1은 그 반대를 의미합니다.
**영향: **마스터 인스턴스 수정 후, 재해 복구의 매개변수를 동기화 수정할 수 없습니다. 마스터 인스턴스 대소문자에는 민감하고, 재해 복구 대소문자에는 민감하지 않을 경우(예: 마스터 인스턴스에서 테이블을 2개 생성하고, 테이블 이름이 각각 Test, TEst), 재해 복구가 애플리케이션 대응 로그에 있으면 데이터 동기화 상태 오류가 발생할 수 있습니다. 오류의 원인은 TEst 테이블 이름이 이미 존재하기 때문입니다.


### auto_increment_increment
**기본값: **1
**용도: **자동 증가 AUTO_INCREMENT의 증가량 값에 사용. 해당 매개변수의 설정 가능 범위는 1~65535이며, 기본값은 1입니다.
**영향: **마스터 인스턴스에서 매개변수를 수정하면 재해 복구 인스턴스의 매개변수를 동기화 수정할 수 없습니다. binlog_format을 statement로 설정 시, 실행 명령어만 기록됩니다. 이때 마스터 인스턴스에서 자동 증가된 증가량 값은 수정하나, 재해 복구 인스턴스는 동기화 변경하지 않아 마스터/슬레이브의 데이터 불일치가 발생할 수 있습니다.

### auto_increment_offset
**기본값: **1
**용도: **자동 증가 AUTO_INCREMENT의 시작값(오프셋)에 사용. 해당 매개변수의 설정 가능 범위는 1~65535이며, 기본값은 1입니다.
**영향: **마스터 인스턴스에서 매개변수를 수정하면 재해 복구 인스턴스의 매개변수를 동기화 수정할 수 없습니다. 마스터/슬레이브에서 Auto Increment의 시작값은 수정하나, 재해 복구 인스턴스는 동기화 변경하지 않아 마스터/슬레이브의 데이터 불일치가 발생할 수 있습니다.


### sql_mode
**기본값: **NO_ENGINE_SUBSTITUTION
**용도: **MySQL은 다양한 sql mode 방식으로 실행할 수 있으며, sql 모드에 mysql이 지원해야 하는 sql 구문, 데이터 인증 등이 정의되어 있습니다. 해당 매개변수 5.6 버전의 기본 매개변수값은 NO_ENGINE_SUBSTITUTION으로, 사용하는 스토리지 엔진이 비활성화되었거나 Uncompiled되어 오류가 발생함을 의미합니다. 5.7 버전의 기본 매개변수값은 `ONLY_FULL_GROUP_BY`,`STRICT_TRANS_TABLES`,`NO_ZERO_IN_DATE`,`NO_ZERO_DATE`,
`ERROR_FOR_DIVISION_BY_ZERO`,`NO_AUTO_CREATE_USER`,`NO_ENGINE_SUBSTITUTION`입니다.
그중에서,
- `ONLY_FULL_GROUP_BY`는 GROUP BY 작업 시 SELECT 칼럼, HAVING 혹은 ORDER BY 칼럼이 있다면, 반드시 GROUP BY에 나타나야 하거나 GROUP BY의 함수 칼럼에 종속되어야 함을 의미합니다.
- `STRICT_TRANS_TABLES`가 포함되어 있으면 Strict mode가 활성화됩니다.
- `NO_ZERO_IN_DATE`가 날짜의 월, 일에 0을 포함하도록 허용하는지, Strict mode에 영향을 받는지 결정합니다.
- `NO_ZERO_DATE`를 포함하면 데이터베이스에서 날짜에 0을 삽입할 수 없으며, Strict mode에 영향을 받는지 결정합니다.
- `ERROR_FOR_DIVISION_BY_ZERO`는 Strict mode에서 INSERT 혹은 UPDATE 할 때 0으로 나뉘면 오류가 발생하지만 이를 알리지 않으며, Strict mode가 아닐 때 0으로 나뉘면 MySQL이 NULL을 출력합니다.
- `NO_AUTO_CREATE_USER`은 GRANT로 생성하여 비밀번호가 없는 사용자를 차단합니다.
- `NO_ENGINE_SUBSTITUTION`은 사용하는 스토리지 엔진이 비활성화되었거나 Uncompiled 되어 오류가 발생함을 의미합니다.

**영향: **마스터 인스턴스에서 매개변수를 수정하면 재해 복구 인스턴스의 매개변수를 동기화 수정할 수 없습니다. 마스터 인스턴스에서 sql mode 방식은 수정하나, 재해 복구 인스턴스는 동기화 변경하지 않습니다. 예를 들어 마스터 인스턴스 sql mode 방식 제한이 재해 복구 sql mode 방식 제한보다 작을 경우, 마스터 인스턴스에서 실행 성공한 SQL을 재해 복구에 동기화할 때 오류가 발생하여 마스터/슬레이브 데이터 불일치가 발생할 수 있습니다.  














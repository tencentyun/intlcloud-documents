### TencentDB for MySQL의 구성 매개변수는 어떻게 수정합니까?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하여 관리 페이지로 이동한 다음, **데이터베이스 관리** > **매개변수 설정**을 클릭합니다. 그 중 일반적인 var\_name에는 다음과 같은 변수가 포함되어 있습니다.
<table>
<tbody><tr>
<th>변수</th><th>설명</th></tr>
<tr>
<td>character_set_server</td><td>서버 기본 문자 세트</td></tr>
<tr>
<td>connect_timeout</td><td>연결 타임아웃</td></tr>
<tr>
<td>long_query_time</td><td>해당 시간을 초과한 쿼리는 슬로우 쿼리입니다.</td></tr>
<tr>
<td>max_allowed_packet</td><td>패킷 최대 길이</td></tr>
<tr>
<td>max_connections</td><td>최대 연결 수</td></tr>
<tr>
<td>sql_mode</td><td>현재 서버의 SQL 모드</td></tr>
<tr>
<td>table_open_cache</td><td>전체 스레드에서 테이블을 연 개수. 해당 값을 높이면 mysqld의 열린 파일 설명 부호 개수가 늘어납니다.</td></tr>
<tr>
<td>wait_timeout</td><td>Non-interactive 연결 타임아웃 시간</td></tr>
</tbody></table>

더 많은 구성 매개변수를 더 보려면 콘솔의 **데이터베이스 관리** > **매개변수 설정**으로 이동하십시오.

### TencentDB for MySQL에서 중국어 쿼리를 설정하는 방법은 무엇인가요?
TencentDB for MySQL은 현재 중국어를 지원하지 않습니다.

### TencentDB for MySQL의 타이머 기능을 활성화하려면 어떻게 해야 하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하여 관리 페이지로 이동한 다음, **데이터베이스 관리** > **매개변수 설정** 탭에서 event_scheduler 매개변수를 ON으로 설정합니다.

### TencentDB for MySQL 연결 타임아웃을 너무 짧게 설정했습니다. 어떻게 늘릴 수 있나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하여 관리 페이지로 이동한 다음, **데이터베이스 관리** > **매개변수 설정** 탭에서 wait_timeout 매개변수를 수정합니다.

### TencentDB for MySQL에서 group_concat_max_len 매개변수를 수정하려면 어떻게 해야 하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하여 관리 페이지로 이동한 다음, **데이터베이스 관리** > **매개변수 설정** 탭에서 group_concat_max_len 매개변수를 수정합니다.

### TencentDB for MySQL 전체 테이블 스캔(Full table scan)의 SQL 명령을 찾는 방법은 무엇인가요?
전체 테이블 스캔의 명령은 기록하지 않음으로 기본 설정되어 있습니다. TencentDB for MySQL 콘솔 **매개변수 설정**에서 log_queries_not_using_indexes 매개변수를 ON으로 설정할 수 있습니다. 단, 너무 장시간 ON으로 두지 않도록 합니다.

### CDB의 기본 문자 세트 인코딩은 어떻게 수정하나요?
TencentDB for MySQL의 기본 문자 세트 인코딩 포맷은 UTF8이며 현재 LATIN1, GBK, UTF8, UTF8MB4 네 종류의 문자 세트 설정을 지원합니다.

TencentDB는 기본 문자 세트 변경을 지원하지만, 더 나은 애플리케이션 이식성을 위해, 테이블 생성 시 테이블 인코딩을 명시적으로 지정하고, 연결 설정 시 연결 인코딩을 지정하는 것이 좋습니다. MySQL 기본 문자 세트 및 수정 방법에 대한 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">사용 제한</a>을 참고하십시오. [콘솔](https://console.cloud.tencent.com/cdb)에서도 문자 세트를 수정할 수 있습니다.

### TencentDB에서 문자 세트 데이터 정렬을 보려면 어떻게 해야 하나요?
TencentDB for MySQL에서는 인스턴스를 생성할 때 문자 세트 조합을 설정할 수 있습니다. 데이터에 대한 대소문자 구분, 악센트 구분 또는 이진 데이터 정렬을 제공하기 위해 문자 세트를 선택할 수 있지만 그렇게 하면 관련 데이터베이스 작업의 결과에 영향을 미칩니다.
show collation 명령을 실행하여 데이터 정렬을 볼 수 있습니다.
**예시**:
```
show collation where charset ='utf8mb4';
```
**정렬 규칙 설명**

| 정렬 옵션 | 설명 | 
|---------|---------|
| _CS | 대소문자를 구분합니다. | 
| _CI | 대소문자를 구분하지 않습니다. | 
| _AS | 악센트를 구분합니다. 예를 들어 ‘a’와 ‘ấ’는 다른 문자입니다. | 
| _AI | 악센트를 구분하지 않습니다. | 
| _BIN | 바이너리. | 

**문자 세트 접미사 설명**

| 인스턴스 문자 세트 접미사 | 설명 | 
|---------|---------|
|_CI_AI|대소문자 및 악센트를 구분하지 않습니다. |
|_CI_AS|대소문자를 구분하지 않으며 악센트는 구분합니다. |
|_CS_AI|대소문자를 구분하며 악센트는 구분하지 않습니다. |
|_CS_AS|대소문자 및 악센트를 구분합니다. |

### lower_case_table_names 매개변수 수정에 실패했습니다. 어떻게 처리해야 하나요?
콘솔을 통해 매개변수 lower_case_table_names를 1로 설정하면 대소문자를 구분하지 않습니다. 다음 두 가지 사항에 주의하십시오.
- 해당 매개변수를 수정하면 데이터베이스가 재시작됩니다.
- 인스턴스에 있는 라이브러리를 확인하고 테이블이 모두 소문자로 되어 있는지 확인합니다. DB 테이블 이름에 대문자가 있는 경우 모두 소문자로 변경한 후에 매개변수를 수정해야 합니다. 그렇지 않을 경우 오류를 보고합니다.
- 8.0 버전은 해당 매개변수를 수정할 수 없으며, 8.0 버전은 기본적으로 대소문자를 구분합니다.

대문자 테이블 존재 여부 확인:
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
대문자 데이터베이스 존재 여부 확인:
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```

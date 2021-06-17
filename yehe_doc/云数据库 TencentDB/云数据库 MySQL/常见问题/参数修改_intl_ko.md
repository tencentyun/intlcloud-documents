### TencentDB for MySQL의 설정 매개변수는 어떻게 수정하나요?
- **TencentDB for MySQL 콘솔에서 수정**
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 이름을 클릭하여 관리 페이지로 이동한 다음, [데이터베이스 관리]>[매개변수 설정]을 클릭합니다. var\_name에는 아래의 변수가 포함되어 있습니다.
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

- **phpMyAdmin 콘솔 방식**
phpMyAdmin을 통해 TencentDB for MySQL에 로그인한 후 상단 메뉴의 [변수]를 클릭하고 하단의 변수 리스트에서 수정할 변수에 해당하는 위치의 [편집]을 클릭하여 수정한 다음 [저장]을 클릭합니다.
![](https://main.qcloudimg.com/raw/214fec618ff4e166c6e4d747be3fea0b.png)

더 많은 매개변수 설정은 콘솔의 [데이터베이스 관리]>[매개변수 설정] 페이지에서 확인할 수 있습니다.

### TencentDB for MySQL에서 중국어 쿼리를 설정하는 방법은 무엇인가요?
TencentDB for MySQL은 현재 중국어를 지원하지 않습니다.

### TencentDB for MySQL의 타이머 기능은 어떻게 설정하나요?
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 이름을 클릭하여 관리 페이지로 이동한 다음, [데이터베이스 관리]>[매개변수 설정] 페이지를 열고 매개변수 설정에서 event_scheduler 매개변수를 ON으로 설정합니다.

### TencentDB for MySQL 연결 타임아웃 설정이 너무 짧습니다. 시간은 어떻게 늘리나요?
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 이름을 클릭하여 관리 페이지로 이동한 다음, [데이터베이스 관리]>[매개변수 설정] 페이지를 열고 매개변수 설정에서 wait_timeout 매개변수를 수정합니다.

### TencentDB for MySQL에서 group_concat_max_len 매개변수는 어떻게 조정하나요?
[TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 이름을 클릭하여 관리 페이지로 이동한 다음, [데이터베이스 관리]>[매개변수 설정] 페이지를 열고 매개변수 설정에서 group_concat_max_len 매개변수를 수정합니다.

### TencentDB for MySQL 전체 테이블 스캔(Full table scan)의 SQL 명령어는 어떻게 찾나요?
전체 테이블 스캔의 명령어는 기록하지 않도록 기본 설정되어 있습니다. TencentDB for MySQL 콘솔의 [매개변수 설정]에서 log_queries_not_using_indexes 매개변수를 ON으로 설정할 수 있습니다. 단, 너무 장시간 ON으로 두지 않도록 합니다.

### CDB의 기본 문자 세트 인코딩은 어떻게 수정하나요?
TencentDB for MySQL의 기본 문자 세트 인코딩 포맷은 UTF8이며 현재 LATIN1, GBK, UTF8, UTF8MB4 네 종류의 문자 세트 설정을 지원합니다.

CDB는 기본적으로 문자 세트 인코딩 설정을 지원하지만, 테이블을 생성할 때 지정 테이블의 인코딩을 명시하고, 연결 생성 시에 연결된 인코딩을 지정하시길 권장합니다. 이는 애플리케이션을 더욱 원활하게 이식하도록 도와줍니다. MySQL 기본 문자 세트 설명 및 수정 방법에 대한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">사용 제한</a>을 참조하십시오. [콘솔](https://console.cloud.tencent.com/cdb)에서도 문자 세트를 수정할 수 있습니다.

### lower_case_table_names 매개변수 수정에 실패했습니다. 어떻게 처리해야 하나요?
콘솔을 통해 매개변수 lower_case_table_names를 1로 설정하면 대소문자를 구분하지 않습니다. 다음 두 가지 사항에 주의하십시오.
- 해당 매개변수를 수정하면 데이터베이스가 재시작됩니다.
- 인스턴스에 있는 라이브러리를 확인하고 테이블이 모두 소문자로 되어 있는지 확인합니다. DB 테이블 이름에 대문자가 있는 경우 모두 소문자로 변경한 후에 매개변수를 수정해야 합니다. 그렇지 않을 경우 오류를 보고합니다.
- 8.0 버전은 해당 매개변수를 수정할 수 없으며, 8.0 버전은 기본적으로 대소문자를 구분합니다.


본문은 지원되는 명령 시나리오와 병렬 쿼리의 제한된 시나리오를 설명합니다.

[](id:JRYJCJ1)
## 지원되는 명령 시나리오
TencentDB for MySQL은 다음과 같은 특성을 가진 SQL 명령에 대한 병렬 쿼리 기능을 구현했으며 앞으로 더 추가될 예정입니다.
- 단일 테이블 스캔: 오름차순 또는 내림차순의 전체 테이블 스캔, 인덱스 스캔, 인덱스 범위 스캔 및 인덱스 REF 쿼리를 지원합니다.
- 다중 테이블 연결: NLJ(Nested Loop Join) 알고리즘과 Semi Join, Anti Join, Outer Join을 지원합니다.
- 서브 쿼리: derived table에 대해 병렬 쿼리가 지원됩니다.
- 데이터 유형: 정수, 문자열, 부동 소수점, 시간 및 오버플로(런타임 크기 제한 포함)와 같은 다양한 데이터 유형을 쿼리할 수 있습니다.
- 공통 오퍼레이터 및 함수에 대한 제한이 없습니다.
- COUNT/SUM/AVG/MIN/MAX 집계 함수를 지원합니다.
- UNION/UNION ALL 쿼리가 지원됩니다.
- traditional(기본값), json 및 tree EXPLAIN 형식이 지원됩니다.

## 제한된 시나리오
TencentDB for MySQL의 병렬 쿼리 기능은 다음 시나리오에서 지원되지 않습니다.

<table>
<thead><tr><th>제한</th><th>설명</th></tr></thead>
<tbody>
<tr>
<td rowspan="6">명령 호환성 제한</td>
<td>INSERT ... SELECT 및 REPLACE ... SELECT를 포함하여 쿼리가 아닌 명령에 대해서는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>stored program의 명령에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>prepared statement에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>직렬 격리 레벨 트랜잭션의 명령에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>select for update/share lock과 같은 잠금 읽기에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>CTE에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr>
<td rowspan="5">테이블/인덱스 호환성 제한</td>
<td>시스템, 임시 및 비 Innodb 테이블에 대해서는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>스페이스 인덱스에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>전체 텍스트 인덱스에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>분할된 테이블에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>index_merge 스캔 모드에서는 테이블에 대해 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr>
<td rowspan="13">표현식/ Field 호환성 제한</td>
<td>Generated Column 또는 BLOB, TEXT, JSON, BIT 및 GEOMETRY 필드를 포함하는 테이블에 대해서는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>BIT_AND, BIT_OR 또는 BIT_XOR 유형의 집계 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>aggregation(distinct)에는 SUM(DISTINCT) 및 COUNT(DISTINCT)와 같은 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>SP_WITHIN_FUNC 및 ST_DISTANCE와 같은 GIS 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>사용자 지정 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>json_length, json_type, JSON_ARRAYAGG와 같은 json 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>xml_str과 같은 XML 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>is_free_lock, is_used_lock, release_lock, release_all_locks 및 get_lock과 같은 사용자 잠금 기능에 대해서는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>sleep, random, GROUP_CONCAT, set_user_var, 및 weight_string 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>STD/STDDEV/STDDEV_POP, VARIANCE/VAR_POP/VAR_SAMP와 같은 특정 통계 함수에 대해서는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>서브 쿼리에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>윈도우 함수에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
<tr><td>rollup에는 병렬 쿼리가 지원되지 않습니다.</td></tr>
</tbody></table>	

[지원되는 명령 시나리오](#JRYJCJ1) 예시 외에도 병렬 쿼리 실행 계획 및 스레드 작업 상태를 확인하여 명령을 병렬로 쿼리할 수 있는지 확인할 수 있습니다. 자세한 내용은 [병렬 쿼리 조회](https://www.tencentcloud.com/document/product/236/53411)를 참고하십시오.


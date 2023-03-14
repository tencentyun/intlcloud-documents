TencentDB for MySQL을 사용하면 매개변수를 조정하여 병렬 쿼리 기능을 활성화 또는 비활성화할 수 있습니다. 구체적으로 콘솔의 HINT 문을 통해 모든 SQL 문에 대한 기능을 활성화 또는 비활성화하거나, 실행 조건을 설정하거나, 특정 SQL 문의 실행 모드를 지정할 수 있습니다.
>?hint 문은 SQL 문 실행 여부를 지정하고 SQL 문에 session 매개변수를 적용할 수 있습니다. 또한 지정된 병렬 테이블 쿼리도 지원합니다.
>

## hint 문 사용법

| 기능 | 명령 라인 | 설명 |
|---------|---------|---------|
| 병렬 쿼리 활성화 | `SELECT /*+PARALLEL(x)*/ ... FROM ...;` | x는 0보다 커야 하는 SQL 문의 병렬 처리를 나타냅니다. |
| 병렬 쿼리 비활성화 | `SELECT /*+PARALLEL(x)*/ ... FROM ...;` | x가 0으로 설정되면 병렬 쿼리를 비활성화함을 나타냅니다. |
| 병렬 테이블 지정 | 다음 방법 중 하나로 병렬 쿼리 실행 계획에 포함하거나 제외할 테이블을 지정할 수 있습니다. <li>PARALLEL을 통해 계획에 포함될 테이블을 지정합니다. <br>`SELECT /*+PARALLEL(t)*/ ... FROM ...;`<li>NO_PARALLEL을 통해 계획에서 제외할 테이블을 지정합니다. <br>`SELECT /*+NO_PARALLEL(t)*/ ... FROM ...;`</li> | t는 테이블 이름입니다. |
| 병렬 테이블과 병렬 처리를 모두 지정 | `SELECT /*+PARALLEL(t x)*/ * ... FROM ...;` | x는 0보다 커야 하는 SQL 문의 병렬 처리를 나타냅니다. t는 테이블 이름입니다. |
| 지정된 SQL 문에 대해서만 적용되는 hint 문을 통해 session 매개변수 설정 | `SELECT /*+SET_VAR(var=n)*/ * ... FROM ...;` | var는 session 범위의 병렬 쿼리 매개변수입니다.|

## hint 문 사용 사례
**사용 사례1:**
`select /*+PARALLEL()*/ * FROM t1, t2;`
병렬 쿼리에 대한 병렬 처리 수준을 txsql_parallel_degree(기본값) 값으로 설정합니다. 문이 병렬 쿼리 실행 조건을 충족하지 않으면 직렬 쿼리가 사용됩니다.

**사용 사례2:**
`select /*+PARALLEL(4)*/ * FROM t1, t2;`
기본값과 상관없이 명령문의 병렬 처리 수준을 4로 설정합니다. 즉, txsql_parallel_degree = 4입니다. 문이 병렬 쿼리 실행 조건을 충족하지 않으면 직렬 쿼리가 사용됩니다.

**사용 사례3:**
`select /*+PARALLEL（t1）*/ * FROM t1，t2；`
병렬 쿼리에 t1 테이블을 포함하고 기본 병렬 처리를 사용합니다. t1이 txsql_parallel_table_record_threshold 값보다 작으면 직렬 쿼리가 사용됩니다.

**사용 사례4:**
`select /*+PARALLEL（t1 8）*/ * FROM t1，t2；`
병렬 쿼리에 t1 테이블을 포함하고 병렬 처리 수준을 8로 설정합니다. t1이 txsql_parallel_table_record_threshold 값보다 작으면 직렬 쿼리가 사용됩니다.

**사용 사례5:**
`select /*+NO_PARALLEL（t1）*/ * FROM t1，t2；`
병렬 쿼리에서 t1 테이블을 제외합니다. t1이 txsql_parallel_table_record_threshold 값보다 크면 직렬 쿼리가 사용됩니다.

**사용 사례6:**
`select /*+SET_VAR(txsql_parallel_degree=8)*/ * FROM t1，t2；`
기본값과 상관없이 문의 병렬 처리 수준을 8로 설정합니다. 즉, txsql_parallel_degree = 8입니다.

**사용 사례7:**
`select /*+SET_VAR(txsql_parallel_cost_threshold=1000)*/ * FROM t1，t2`
명령문에 대해 txsql_parallel_cost_threshold=1000을 설정합니다. 실행 페널티가 1000보다 크면 병렬 쿼리를 사용할 수 있습니다.

**사용 사례8:**
`select /*+SET_VAR(txsql_optimizer_context_max_mem_size=500000)*/ * FROM t1，t2`
명령문에 대해 txsql_optimizer_context_max_mem_size=500000을 설정합니다. 이는 병렬 쿼리 계획 환경에서 적용할 수 있는 최대 메모리 크기를 500000으로 조정하는 것을 의미합니다.

## 관련 문서
- [병렬 쿼리 활성화/비활성화](https://www.tencentcloud.com/document/product/236/52512)
- [병렬 쿼리 보기](https://www.tencentcloud.com/document/product/236/53411)


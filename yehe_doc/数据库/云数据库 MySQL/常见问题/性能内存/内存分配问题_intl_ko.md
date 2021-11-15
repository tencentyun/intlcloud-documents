TencentDB for MySQL 메모리는 성능에 영향을 미치는 주요 매개변수로, 주로 SQL의 요청 오류 및 데이터베이스 최적화 작업 대기 시 사용률이 증가합니다. 심한 경우 OOM으로 인한 인스턴스의 HA 변환이 발생해 비즈니스 안정성과 가용성이 떨어질 수 있습니다.

MySQL 메모리는 global 레벨의 공유 메모리와 session 레벨의 전용 메모리로 구분합니다. 공유 메모리는 인스턴스 생성과 동시에 할당되는 메모리 용량으로, 모든 액세스에 공유됩니다. 전용 메모리는 MySQL 서버 연결 시 할당되는 개별 캐시입니다. 일부 특수 SQL 또는 필드는 단일 스레드가 다수의 캐시를 할당해 OOM 오류가 발생할 수 있으며, 이는 연결한 전용 메모리가 원인입니다. 각 구성 부분에 대한 자세한 내용은 다음과 같습니다.

## 공유 메모리
다음 명령어를 실행하면 예시와 같은 공유 메모리 할당 내용을 확인할 수 있습니다.
```
show variables where variable_name in ('innodb_buffer_pool_size','innodb_log_buffer_size','innodb_additional_mem_pool_size','key_buffer_size','query_cache_size');
```
	
>?5.7버전은 innodb_additional_mem_pool_size를 지원하지 않습니다.

다음 매개변수는 1000MB 메모리 인스턴스의 공유 메모리에 할당된 내용을 조회한 결과입니다(이하 인스턴스 구성 테스트).
	1.  +---------------------------------+-----------+
	2.  | Variable_name                   | Value     |
	3.  +---------------------------------+-----------+
	4.  | innodb_additional_mem_pool_size | 8388608   |
	5.  | innodb_buffer_pool_size         | 524288000 |
	6.  | innodb_log_buffer_size          | 67108864  |
	7.  | key_buffer_size                 | 16777216  |
	9.  | query_cache_size                | 0         |
	10. +---------------------------------+-----------+
	11. 5 rows in set (0.01 sec)

**매개변수 설명:**
- **innodb_buffer_pool_size**
 해당 캐시는 Innodb 엔진에서 가장 중요한 캐시 영역으로, 메모리로 물리적 데이터 파일을 보충하는 주요 수단입니다. TencentDB for MySQL은 인스턴스 사양의 50 ~ 80%를 해당 용량(위 도표 1000MB * 0.5 = 500MB)으로 설정합니다. 해당 캐시는 데이터 페이지, 인덱스 페이지, undo 페이지, insert buffer, 자기 적응 해시 인덱스, lock 정보 및 데이터 사전 등 정보를 담고 있습니다. SQL에서 읽기와 쓰기 작업이 일어나면 물리적 데이터 파일이 아닌 buffer_pool에서 작업이 발생한 뒤 checkpoint와 같은 메커니즘을 거쳐 데이터 파일을 write back합니다. 해당 캐시 공간은 데이터베이스의 성능 향상, SQL 실행 속도 향상의 장점이 있는 반면, 장애 복구가 더딜 수 있습니다.

- **innodb_log_buffer_size**
 해당 영역은 주로 redo log 정보를 저장하며, TencentDB for MySQL은 64MB의 용량이 설정되어 있습니다. InnoDB는 redo log를 이 영역에 입력한 뒤, 일정한 빈도수에 따라 새로 고침하여 로그 파일을 새로 생성합니다. 통상 해당 영역 캐시는 빠른 주기로 redo log가 새로 고침(Master Thread가 매초마다, 트랜잭션 제출 시마다, 해당 공간이 1/2 미만일 때 새로 고침)되기 때문에 큰 용량이 요구되지 않습니다.

- **innodb_additional_mem_pool_size**
 해당 영역은 주로 InnoDB 내부의 일부 데이터 구조를 저장하며, TencentDB for MySQL은 8MB로 일괄 설정되어 있습니다. 통상 buffer_pool에서 메모리 신청 시 해당 객체 구조 정보를 저장할 수 있는 별도 메모리를 신청해야 합니다. 해당 영역의 용량은 테이블 개수와 관련이 있어 테이블 개수가 많을수록 용량도 늘어납니다.

- **key_buffer_size**
 해당 영역은 MyISAM 테이블의 주요 캐시 영역으로, 모든 인스턴스는 16M로 설정되며, MyISAM 테이블 키를 저장합니다. MyISAM 테이블은 InnoDB 테이블과 달리 인덱스 캐시가 key_buffer에 저장되며, 데이터 캐시는 운영 체제의 메모리에 저장됩니다. TencentDB for MySQL은 MyISAM 엔진을 채택하고 있어 해당 영역을 위한 공간을 할애해야 합니다.

- **query_cache_size**
 해당 영역은 조회 결과를 캐시 형태로 저장하며, SQL의 리졸브 및 실행을 위한 비용을 줄일 수 있습니다. TencentDB for MySQL은 해당 영역의 캐시 저장을 비활성화하고 있습니다. 주로 읽기가 많고, 쓰기가 적은 응용 시나리오에 적합하며, SQL 명령에 의한 hash 값에 따라 캐시 형태로 저장되기 때문에 테이블 데이터가 변동 하면 즉시 무효화됩니다.

## 전용 메모리
다음 명령어를 실행하면 예시와 같은 session 전용 메모리 할당 내용을 확인할 수 있습니다.
```
show variables where variable_name in ('read_buffer_size','read_rnd_buffer_size','sort_buffer_size','join_buffer_size','binlog_cache_size','tmp_table_size');
```

조회 결과는 다음과 같습니다(이하 인스턴스 구성 테스트).
		1.  +----------------------+-----------+
		2.  | Variable_name        | Value     |
		3. +----------------------+-----------+
		4.  | binlog_cache_size    | 32768     |
		5.  | join_buffer_size     | 262144    |
		6.  | read_buffer_size     | 262144    |
		7.  | read_rnd_buffer_size | 524288    |
		8.  | sort_buffer_size     | 524288    |
		9.  | tmp_table_size       | 209715200 |
		10.  +----------------------+-----------+
		11.  6 rows in set (0.00 sec)

**매개변수 설명:**

- **read_buffer_size**
	순차 스캐닝(progressive scanning)에 의한 캐시 메모리를 각각 저장합니다. thread가 데이터를 순차적으로 스캔하는 경우 buffer 공간을 우선 스캔하기 때문에 물리적 읽기를 줄일 수 있습니다.

- **read_rnd_buffer_size**
	랜덤 스캐닝(Random Scanning)에 의한 캐시 메모리를 각각 저장합니다. thread가 데이터를 랜덤으로 스캔하는 경우 buffer 공간을 우선 스캔하기 때문에 물리적 읽기를 줄일 수 있습니다.
	
- **sort_buffer_size**
	order by 및 group by의 SQL 실행 시 정렬된 중간 결과를 저장하기 위한 sort_buffer를 할당합니다. 정렬 시, 스토리지가 sort_buffer_size를 초과하는 경우, 작업 완료를 위해 디스크에 임시 테이블이 생성됩니다.

- **join_buffer_size**
	MySQL은 nest loop의 join 알고리즘만 지원하며, 선행 테이블의 행을 추출하여 후행 테이블을 읽으면서 조인하는 로직을 사용하고 있습니다. 이때 후행 테이블을 join_buffer에 삽입하기 때문에 동시 접속 보호 메커니즘이 있는 buffer_pool에 액세스하지 않아도 됩니다.

- **binlog_cache_size**
	해당 영역은 해당 thread의 binlog 로그를 캐시 형태로 저장합니다. 개별 트랜잭션은 commit되기 전 관련 로그를 binlog_cache에 우선 저장합니다. 트랜잭션이 commit되면 디스크에 binlog 파일이 생성되어 장기 보존됩니다.

- **tmp_table_size**
	앞선 session 레벨의 buffer와 달리 해당 매개변수는 콘솔에서 수정할 수 있습니다. 사용자 메모리의 임시 테이블 용량을 가리키며, 해당 thread로 생성된 임시 테이블의 용량이 설정 값을 초과한 경우, 임시 테이블이 디스크 내의 MyISAM 임시 테이블로 전환됩니다.

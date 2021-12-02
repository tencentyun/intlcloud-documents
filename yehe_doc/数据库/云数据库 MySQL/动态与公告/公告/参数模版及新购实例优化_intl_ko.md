
클라우드 데이터베이스 MySQL은 2021년 12월 7일부터 매개변수 관련 기능 및 전달 프로세스의 최적화를 진행합니다. 이 최적화에는 매개변수 템플릿 생성, 매개변수 비교, 매개변수 템플릿 적용, 매개변수 수정 및 기타 기능, 수정 가능한 매개변수, 신규 구입 인스턴스 최적화 업데이트가 포함됩니다.

>?이 매개변수의 관련 기능 최적화 및 전달 프로세스의 최적화를 미리 체험하시려면 2021년 9월 27일 이후 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 베타 테스트를 신청할 수 있습니다.
매개변수 관련 기능은 2노드 및 3노드 MySQL 5.6, MySQL 5.7 및 MySQL 8.0 버전에만 적용됩니다.

## 신규 구매 인스턴스 최적화
기존 신규 구매 인스턴스 프로세스 대비, 초기화 프로세스가 취소되었으며, 신규 구매 페이지에 문자 세트 선택, 테이블명 대소문자 구분, 데이터베이스 액세스 포트 입력, root 비밀번호 등 지원이 추가되었습니다.

자세한 내용은 [MySQL 인스턴스 생성](https://intl.cloud.tencent.com/document/product/236/43472)을 참고하십시오.

## 매개변수 관련 최적화
### 매개변수 활용
일부 매개변수는 공식 정의를 지원합니다. 이러한 유형의 매개변수는 사양 변경에 따라 변경될 수 있으므로 데이터베이스가 항상 최상의 구성으로 실행됩니다.
표현식 구문 관련 내용은 다음 표를 참고하십시오.

| 지원 카테고리 | 설명 | 예시 |
| ------ | ------------------------------------------------------------ | --------------------- |
| 변수   | <li>DBinitMemory: 정수인 인스턴스 유형의 메모리 크기입니다. 예를 들어 인스턴스 사양의 메모리 크기가 4000MB인 경우 DBinitMemory의 값은 4000입니다. <li>DBInitCpu: 인스턴스 사양의 CPU 코어 수, 정수 유형. TencentDB for MySQL의 innodb_buffer_pool_size 매개변수 설정은 메모리 크기의 50% - 90% 사이를 유지해야 하며, 설정 값이 90%보다 크면 90%로, 설정 값이 50%보다 작으면 50%로 자동 설정됩니다. | {DBinitMemory*786432} |
| 오퍼레이터 | 공식 구문: {} 패키지를 사용합니다. <li>나눗셈 오퍼레이터(/): 피제수를 제수로 나누고 정수 몫을 반환합니다. 계산 결과가 10진수이면 정수 부분만 취하며, 소수점은 지원되지 않습니다. 예를 들어 시스템은 {MIN(DBInitMemory/4+500,1000000)}을 지원하지만 {MIN(DBInitMemory\*0.25+500,1000000)}은 지원하지 않습니다. <li> 곱셈 연산자(*): 두 개의 승수를 곱하여 정수 값을 반환합니다. 계산 결과가 10진수이면 정수 부분만 취합니다. 소수 연산을 지원하지 않습니다. |  -                     |
| 함수   | <li>MAX() 함수는 정수 유형 또는 매개변수 공식 목록에서 가장 큰 값을 반환합니다. <li>MIN() 함수는 정수 유형 또는 매개변수 공식 목록에서 가장 작은 값을 반환합니다.</li> | {MAX(DBInitCpu/2,4)} |

자세한 설정은 [인스턴스 매개변수 설정](https://intl.cloud.tencent.com/document/product/236/35793)을 참고하십시오.

### 매개변수 템플릿 생성
매개변수 템플릿 생성 시 기존 1개의 템플릿이 2개의 템플릿(고성능 매개변수 템플릿/고안정성 매개변수 템플릿)으로 변경되며, 기존 템플릿 유형 옵션이 추가됩니다.
<img src="https://main.qcloudimg.com/raw/a93abb9d05b05c0018c46d5efa027221.png"  style="zoom:90%;">

템플릿별 매개변수 비교:

|   차이 매개변수 이름           | 기본 템플릿                  | 고성능 매개변수 템플릿       | 고안정성 템플릿              |
| -------------------- | ------------------------- | ------------------------ | -------------------------- |
| innodb_read_io_threads          | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}             |
| innodb_write_io_threads         | 12            | {MAX(DBInitCpu/2,4)}              | {MAX(DBInitCpu/2,4)}                |
| max_connections       | 800    | {MIN(DBInitMemory/4+500,100000)} | {MIN(DBInitMemory/4+500,100000)} |
| table_definition_cache                 | 768                       | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache                       | 2000                      | {MAX(DBInitMemory*512/1000,2048)} | {MAX(DBInitMemory*512/1000,2048)} |
| table_open_cache_instances             | 16                        | {MIN(DBInitMemory/1000,16)}       | {MIN(DBInitMemory/1000,16)}       |
| innodb_disable_sort_file_cache         | OFF                       | OFF                               | ON                    |
| innodb_log_compressed_pages            | ON                        | OFF                               | ON                   |
| innodb_print_all_deadlocks             | OFF                       | OFF                               | ON                    |
| sync_binlog                            | 0                         | 1000                              | 1                                 |
| thread_handling                        | one-thread-per-connection | pool-of-threads                   | one-thread-per-connection         |
| innodb_flush_redo_using_fdatasync      | FALSE                     | TRUE                   | FALSE                 |
| innodb_fast_ahi_cleanup_for_drop_table | FALSE                     | TRUE        | FALSE                             |
| innodb_adaptive_hash_index             | FALSE                     | TRUE                   | FALSE                      |
| innodb_table_drop_mode                 | SYNC_DROP                 | ASYNC_DROP             | SYNC_DROP         |
| innodb_flush_log_at_trx_commit         | 2                         | 2                                 | 1                                 |

매개변수 템플릿에 대한 자세한 소개는 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참고하십시오.

### 설정 가능한 매개변수 추가

| 매개변수 이름                                               |  MySQL 5.6  | MySQL 5.7  | MySQL 8.0  |
| ------------------------------------------------ | -------- | ---- | ---- |
| character_set_client                           |     -            |  &#10003;    |  -    |
| default_password_lifetime                   |      -          |  &#10003;    |  &#10003;    |
| innodb_alter_table_default_algorithm   |      -          |  &#10003;    |   -   |
| innodb_async_truncate_size                |      -          |  &#10003;    |  &#10003;    |
| innodb_async_truncate_work_enabled  |     -          | &#10003;     |    -  |
| innodb_buffer_pool_instances              |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_buffer_pool_size                      |  &#10003; |  &#10003;   |  &#10003;   |
| innodb_default_row_format                  |       -         | &#10003;     | &#10003;    |
| innodb_fast_ahi_cleanup_for_drop_table |     -        |      -             | &#10003;     |
| innodb_flush_redo_using_fdatasync     |       -         | &#10003;     | &#10003;    |
| innodb_page_cleaners                         |       -        | &#10003;     | &#10003;     |
| innodb_table_drop_mode                     |      -         |      -             | &#10003;     |
| innodb_temp_tablespace_fast_cleanup |       -        |       -            | &#10003;     |
| internal_tmp_mem_storage_engine       |       -        |      -            | &#10003;    |
| slave_net_timeout                               |  &#10003; | &#10003;     |   -   |
| slave_parallel_type                             |  &#10003; |          -        |  -    |
| slave_parallel_workers                        |  &#10003; | &#10003;   |&#10003;    |
| sort_buffer_size                                  |  &#10003; |    -              |  -    |
| temptable_use_mmap                          |           -      |      -            | &#10003;    |
| thread_handling                                  |   &#10003; | &#10003;   |&#10003;   |
| thread_handling_switch_mode             |        -          |         -          | &#10003;   |
| thread_pool_oversubscribe                  |   &#10003; | &#10003;    |&#10003;    |
| thread_pool_size                                |        -          | &#10003;    | &#10003;   |
| tx_isolation                                        |          -        | &#10003;    | &#10003;    |

### 템플릿별 성능 테스트
테스트 결과는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0f1aadfa080a43281fd98bea342812e6.png)
![](https://qcloudimg.tencent-cloud.cn/raw/29c6c04452626abe48e32c8370fe3aef.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3ed85cff088505c9f6979c42d5aadf20.png)
。

### 기본 매개변수 템플릿을 유지하는 방법
새 매개변수 시스템 런칭 후 기본 매개변수 템플릿은 고성능 매개변수 템플릿 및 고안정성 템플릿으로 대체됩니다. 새 매개변수 시스템 런칭 전에 매개변수 템플릿 생성을 통해 기본 템플릿 설정을 유지할 수 있습니다. [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참고하십시오.

### 매개변수 비교
각 템플릿 간의 매개변수를 비교하고 다른 템플릿 간의 매개변수 차이점을 볼 수 있는 기능을 제공합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8529618ea8427864dea55f10b675ecb4.png)
매개변수 템플릿 페이지에서 **비교**를 클릭하고 팝업창에서 비교하고자 하는 템플릿을 선택하여 비교할 수 있습니다. 동일한 버전의 데이터베이스 템플릿 비교만 지원됩니다. 참고용 결과는 다음과 같습니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/aad046642c7bec92ccacfda616887781.png"  style="zoom:80%;">

## 문의하기
기타 문의사항은 언제든지 [고객센터](https://console.cloud.tencent.com/workorder/category)를 통해 문의 바랍니다. Tencent Cloud에 대한 지속적인 지원에 감사드립니다. 앞으로도 가성비 높은 제품을 제공하도록 하겠습니다.


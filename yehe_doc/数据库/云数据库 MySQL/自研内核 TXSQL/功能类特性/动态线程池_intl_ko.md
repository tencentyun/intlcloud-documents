## 기능 소개
스레드 풀(Thread_pool)은 특정 수의 작업자 스레드를 사용하여 연결 요청을 처리하며, 이는 일반적으로 OLTP 워크로드 시나리오에 더 적합합니다. 그러나 스레드 풀의 단점은 요청이 슬로우 쿼리로 편향되면 작업자 스레드가 딜레이 시간이 긴 작업에서 차단되어 새 요청에 신속하게 응답하기 어려워 결과적으로 시스템 처리량은 one-thread-per-connection(Per_thread) 모드보다 낮습니다.

Per_thread 모드와 Thread_pool 모드는 각각의 장단점이 있으며, 시스템은 비즈니스 유형에 따라 유연하게 전환되어야 합니다. 안타깝게도 현재 두 모드 간의 전환은 서버를 재시작해야만 완료할 수 있습니다. 일반적으로 업무량이 많은 피크 시간대에 두 모드를 전환해야 하는 상황이 발생하는데 이때 강제로 서버를 재시작하면 업무에 심각한 영향을 미치게 됩니다.

TencentDB for MySQL은 Per_thread 모드와 Thread_pool 모드 간의 전환 유연성을 향상시키기 위해 데이터베이스 서비스를 다시 시작하지 않고 스레드 풀을 동적으로 활성화/비활성화하는 동적 스레드 풀 전환의 최적화를 제안합니다.

## 지원 버전
- 커널 버전 MySQL 8.0 20201230 이상
- 커널 버전 MySQL 5.7 20201230 이상

## 적용 시나리오
성능에 민감하고 비즈니스 유형에 따라 데이터베이스 작업 모드를 유연하게 조정해야 하는 비즈니스.

## 성능 영향
- pool-of-threads를 one-thread-per-connection으로 전환하는 프로세스는 query 누적 및 성능 영향을 초래하지 않습니다.
- one-thread-per-connection에서 pool-of-threads로 전환하는 프로세스 이전에 스레드 풀이 휴면 상태였기 때문에 QPS가 매우 높고 지속적으로 높은 압력이 있을 때 특정 요청이 누적될 수 있습니다. 솔루션은 다음과 같습니다.
  - 옵션1: thread_pool_oversubscribe를 적절하게 늘리고, thread_pool_stall_limit를 적절하게 조정하여 스레드 풀을 빠르게 활성화합니다. 누적된 힙 SQL을 요약한 후 위의 수정 사항을 적절하게 복원합니다.
  - 옵션2: SQL 누적이 발생하면 몇 초 동안 비즈니스 트래픽을 일시적으로 중단하거나 줄이고 pool-of-threads가 활성화를 완료할 때까지 기다렸다가 계속해서 높은 압력을 가하는 비즈니스 트래픽을 복구합니다.

## 사용 설명
새로 추가된 thread_handling_switch_mode는 스레드 풀의 동적 전환 기능을 제어하는 ​​데 사용되며, 옵션값과 그 의미는 다음과 같습니다.

| 옵션값   | 의미                                               |
| -------- | -------------------------------------------------- |
| disabled | 금지 모드 동적 마이그레이션                                   |
| stable    | 새 연결만 마이그레이션                                     |
| fast       | 새 연결 + 새 요청이 마이그레이션됨, 기본 모드                      |
| sharp    | 현재 활성 연결을 kill하여, 빠른 전환 효과를 얻기 위해 사용자가 다시 연결하도록 합니다. |

`show threadpool status` 에 다음 상태를 추가합니다.
- connections_moved_from_per_thread는 Per_thread에서 Thread_pool로 마이그레이션된 connections 수를 나타냅니다.
- connections_moved_to_per_thread는 Thread_pool에서 Per_thread로 마이그레이션된 connections 수를 나타냅니다.
- events_consumed는 각 스레드 풀 작업자 스레드 그룹이 소비하는 총 events 수를 나타내며 Thread_pool이 Per_thread로 마이그레이션되면 더 이상 총 events 수가 증가하지 않습니다.
- average_wait_usecs_in_queue는 queue에 있는 각 event의 평균 대기 시간을 나타냅니다.

'show full processlist'에 다음 상태를 추가합니다.
- Moved_to_per_thread는 연결이 Per_thread로 마이그레이션된 횟수를 나타냅니다.
- Moved_to_thread_pool은 연결이 Thread_pool로 마이그레이션된 횟수를 나타냅니다.

## 관련 매개변수 상태 설명
스레드 풀 관련 매개변수 소개:

| 매개변수 이름                          | 동적         | 유형 | 기본            | 매개변수 값 범위                  | 설명                             |
| ------------------------------- | ------------ | ---- | --------------- | --------------------------- | ------------------------------- |
| thread_pool_idle_timeout        | Yes          | uint | 60              | [1, UINT_MAX]               | 처리해야 하는 네트워크 이벤트가 없을 때 worker 스레드는 최대 이 시간(단위 초)을 기다렸다가 폐기됩니다. |
| thread_pool_oversubscribe       | Yes          | uint | 3               | [1,1000]                    | 작업 그룹에 허용되는 worker 수                          |
| thread_pool_size                | Yes          | uint | 현재 기기 CPU 번호 | [1,1000]                    | 스레드 그룹 수                  |
| thread_pool_stall_limit         | Yes          | uint | 500             | [10, UINT_MAX]              | 이 시간의 모든 간격(단위 밀리초)에서 timer 스레드는 모든 스레드 그룹을 한 번 순회하고 검사합니다.<br>스레드 그룹에 listener가 없고 우선 순위가 높은 큐와 낮은 큐가 비어 있지 않고 새로운 IO 네트워크 이벤트가 없는 경우 스레드 그룹은 stall 상태로 간주되며 timer 스레드는 스레드 그룹에 대한 압력을 완화하기 위해 새 worker 스레드를 깨우거나 생성하는 역할을 합니다. |
| thread_pool_max_threads         | Yes          | uint | 100000          | [1,100000]                  | 스레드 풀에 있는 모든 worker 스레드의 총 수                               |
| thread_pool_high_prio_mode      | Yes, session | enum | transactions    | transactions\statement\none | 세 가지를 포함한 높은 우선 순위 큐 작업 모드:<li>transactions: 트랜잭션을 활성화하고 thread_pool_high_prio_tickets가 0이 아닌 하나의 SQL만 높은 우선 순위 큐에 들어갑니다. 각 연결이 thread_pool_high_prio_tickets의 우선 큐에 배치된 후 일반 큐로 이동됩니다.<li>statement: 모든 연결은 우선 순위가 높은 큐에 넣습니다.<li>none: statement과 달리 모든 연결은 우선 순위가 낮은 큐에 넣습니다.</li> |
| thread_pool_high_prio_tickets   | Yes, session | uint | UINT_MAX        | [0, UINT_MAX]               | transactions 작업 모드에서 각 연결에 부여된 tickets 크기        |
| threadpool_workaround_epoll_bug | Yes          | bool | false           | true/false                  | linux2.x에서 epoll bug를 우회할지 여부, bug는 linux3에서 수정됩니다.          |

`show threadpool status` 명령으로 표시되는 관련 상태 소개:

| 상태 이름                            | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| groupid                               | 스레드 그룹 ID                                                     |
| connection_count                | 스레드 그룹 사용자 연결                                             |
| thread_count                      | 스레드 그룹의 작업자 스레드 수                                           |
| havelistener                       | 스레드 그룹에 현재 listener 존재 여부                                   |
| active_thread_count               | 스레드 그룹의 활성 worker 수                                       |
| waiting_thread_count              | 스레드 그룹에서 대기 중인 worker 수(wait_begin을 호출하는 worker)         |
| waiting_threads_size              | 스레드 그룹에 처리해야 하는 네트워크 이벤트가 없고 휴면 기간에 진입하여 깨어나기를 기다리는 worker 수(thread_pool_idle_timeout 초 대기 후 자동 폐기됨) |
| queue_size                             | 스레드 그룹 일반 우선 순위 큐 길이                                     |
| high_prio_queue_size              | 스레드 그룹 높은 우선 순위 큐 길이                                       |
| get_high_prio_queue_num           | 스레드 그룹의 이벤트가 높은 우선 순위 큐에서 가져온 총 횟수                     |
| get_normal_queue_num              | 스레드 그룹의 이벤트가 일반 우선 순위 큐에서 제거된 총 횟수                   |
| create_thread_num                  | 스레드 그룹에서 생성된 총 worker 스레드 수                                 |
| wake_thread_num                    | 스레드 그룹의 waiting_threads 큐에서 깨어난 총 작업자 수              |
| oversubscribed_num                | 스레드 그룹의 worker가 현재 스레드 그룹이 oversubscribed 상태에 있고 절전 모드로 전환할 준비가 되었음을 발견한 횟수 |
| mysql_cond_timedwait_num     | 스레드 그룹의 worker가 waiting_threads 큐에 들어간 총 횟수                |
| check_stall_nolistener             | 스레드 그룹이 timer 스레드 check_stall에 의해 검사되고 listener가 없음을 발견한 총 횟수   |
| check_stall_stall                     | timer 스레드 check_stall 검사에서 스레드 그룹이 stall 상태로 판단된 총 횟수  |
| max_req_latency_us                | 스레드 그룹의 사용자 연결이 큐에서 대기하는 가장 긴 시간(단위 밀리초)             |
| conns_timeout_killed               | 새로운 메시지가 없는 클라이언트 시간이 임계값(net_wait_timeout)을 초과하여 스레드 그룹의 사용자 연결이 killed된 총 횟수 |
| connections_moved_in               | 다른 스레드 그룹에서 이 스레드 그룹으로 마이그레이션된 총 연결 수                         |
| connections_moved_out             | 이 스레드 그룹에서 다른 스레드 그룹으로 마이그레이션된 총 연결 수                         |
| connections_moved_from_per_thread | one-thread-per-connection 모드에서 스레드 그룹으로 마이그레이션된 총 연결 수      |
| connections_moved_to_per_thread     | 이 스레드 그룹에서 one-thread-per-connection 모드로 마이그레이션된 총 연결 수    |
| events_consumed                          | 스레드 그룹에서 처리한 총 events 수                                     |
| average_wait_usecs_in_queue       | 큐의 스레드 그룹에 있는 모든 events의 평균 대기 시간                     |




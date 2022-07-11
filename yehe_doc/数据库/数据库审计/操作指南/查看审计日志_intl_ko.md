
## 로그 조회
1.[MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql), [TDSQL-C MySQL 콘솔](https://console.cloud.tencent.com/dls/cynosdb/instance) 또는 [MongoDB 콘솔](https://console.cloud.tencent.com/dls/mongodb)에 로그인하고 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고 상단에서 리전을 선택한 후 **감사 로그** 탭을 클릭합니다.
2. **감사 로그** 탭의 감사 인스턴스 섹션에서 감사가 활성화된 데이터베이스 인스턴스를 선택하여 SQL 감사 로그를 봅니다. 또는 **감사 인스턴스** 탭에서 인스턴스 ID를 클릭하여 **감사 로그** 탭으로 이동하여 감사 로그를 봅니다.
>?감사 로그 표시 시간이 밀리초로 줄어들어 SQL 명령의 보다 정확한 정렬 및 문제 분석이 용이합니다.

### 툴 리스트
![](https://qcloudimg.tencent-cloud.cn/raw/a285a1b3e7e1dba10b34127448f9c0f3.png)
 - **시간창**에서 기간을 선택하면 선택한 기간의 감사 결과를 볼 수 있습니다.
>?검색할 데이터가 있는 기간을 선택할 수 있습니다. 처음 60000개의 적합한 레코드를 표시할 수 있습니다.
 - **검색창**에서 키 태그로 검색하여 관련 감사 결과를 볼 수 있습니다. 공통 키 태그에는 SQL 명령, 클라이언트 IP, 데이터베이스 이름, 데이터베이스 계정, SQL 유형, 정책 이름, 실행 시간, 영향을 받는 행 수 및 반환 행 수가 포함됩니다.
  - 검색을 위해 여러 키 태그를 입력할 때 엔터 키를 눌러 분리할 수 있습니다.
  - 와일드카드 ‘*’를 사용하여 IP 주소를 필터링할 수 있습니다. 예를 들어 ‘클라이언트 IP: 9.223.23.2*’를 입력하면 9.223.23.2로 시작하는 IP 주소가 검색됩니다.
  - 키 태그 ‘SQL 명령’ 선택: 콤보 검색이 지원됩니다. 쉼표 또는 공백을 사용하여 필터를 구분할 수 있으며, 이 때 이들 사이의 로직 관계는 AND입니다. 수직 막대 | 를 사용하여 필터를 구분할 수 있으며, 이 때 이들 사이의 로직 관계는 OR입니다.
>?SQL 명령으로 필터링할 때 * 기호는 퍼지 일치를 나타내지 않습니다. 모든 SQL 명령 검색은 퍼지 검색입니다.
>

### 로그 리스트
- **SQL 유형** 드롭다운 목록에서 필터링할 여러 SQL 유형을 선택할 수 있습니다.
- **반환된 행** 필드는 주로 SELECT 명령의 영향을 결정하는 데 사용되는 SQL 명령을 실행하여 반환된 특정 행 수를 나타냅니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/8a035147191070ae4789aec12e67faf1.png)

## SQL 감사 필드
### TencentDB for MySQL/TDSQL-C for MySQL 감사 필드
다음 필드는 TencentDB for MySQL 및 TDSQL-C for MySQL 감사 로그에서 지원됩니다. [TencentDB for MySQL](https://console.cloud.tencent.com/dls/mysql) 또는 [TDSQL-C for MySQL](https://console.cloud.tencent.com/dls/cynosdb/instance) 콘솔에서 전체 SQL **감사 로그**를 가져오고 볼 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/40f34d23921fb707599548204d0dda6a.png)

| 시리얼 넘버 | 필드 이름 | 필드 의미                                                         | 비고                                         |
| ---- | ------------- | ------------------------------------------------------------ | -------------------------------------- |
| 1            | host     |클라이언트 IP                                           |   -                                           |
| 2            |dbname   | 데이터베이스 이름                                                 |  -                                            |
| 3            |user       | 사용자 이름                                                    |      -                                        |
| 4            | sql        | SQL 명령                                             |    -                                          |
| 5            | sqlType    | SQL 명령 유형                                          |   -                                           |
| 6    | errCode       | 에러 코드                                                | 0은 성공을 의미함                           |
| 7    | affectRows    | 영향받는 행의 수                                                     |     -                                         |
| 8    | checkRows     | 스캔된 행의 수                                                     |     -                                         |
| 9    | sentRows      | 반환된 행의 수                                                     |    -                                          |
| 10   | threadId      | 스레드 ID                                                       |       -                                       |
| 11   | ruleNum       | 감사 규칙 번호                                                 |     -                                         |
| 12   | policyName    | 감사 정책 이름                                                   |    -                                          |
| 13   | instanceName  | 인스턴스 이름                                                       |    -                                          |
| 14   | timestamp     | 시작 시간 (초)                                               |   -                                           |
| 15   | nsTime        | 시작 시간 (나노 초). timestamp와 조합하여 시작 시간을 나노 초 단위까지 표기 가능 | 예시 timestamp.nsTime 1577953020.887984015 |
| 16   | execTime      | 실행 시간 (밀리 초)                                             |    -                                          |
| 17   | cpuTime       | CPU 시간 (마이크로 초)                                              |     -                                         |
| 18   | lockWaitTime  | 잠금 대기 시간（마이크로 초）                                           |    -                                          |
| 19   | ioWaitTime    | IO 대기 시간（마이크로 초）                                           |     -                                         |
| 20   | trxLivingTime | 트랜잭션 실행 시간 (마이크로 초）                                   |      -                                        |



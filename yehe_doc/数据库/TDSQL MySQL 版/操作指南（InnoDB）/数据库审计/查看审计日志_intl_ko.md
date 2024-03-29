
## 로그 조회
1. [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/tdsqld/instance-tdmysql) 로그인 후, 왼쪽 사이드바에서 **데이터베이스 감사**를 선택하고, 상단의 리전 선택 후, **감사 로그** 탭을 클릭합니다.
2. **감사 로그** 탭의 감사 인스턴스 섹션에서 감사가 활성화된 데이터베이스 인스턴스를 선택하여 SQL 감사 로그를 봅니다. 또는 **감사 인스턴스** 탭에서 인스턴스 ID를 클릭하여 **감사 로그** 탭으로 이동하여 감사 로그를 봅니다.

### 툴 리스트
![](https://qcloudimg.tencent-cloud.cn/raw/55ece67783162a16cdfeb5e857ad0d5f.png)
 - **시간 창**에서 기간을 선택하면 선택한 기간의 감사 결과를 볼 수 있습니다.
>?검색할 데이터가 있는 기간을 선택할 수 있습니다. 처음 60000개의 적합한 레코드를 표시할 수 있습니다.
 - **검색 창**에서 키 태그로 검색하여 관련 감사 결과를 볼 수 있습니다. 공통 키 태그에는 SQL 명령, 클라이언트 IP, 데이터베이스 이름, 데이터베이스 계정, 실행 시간, 영향을 받는 행 수 및 반환 행 수가 포함됩니다.
  - 검색을 위해 여러 키 태그를 입력할 때 엔터 키를 눌러 분리할 수 있습니다.
  - 와일드카드 ‘*’를 사용하여 IP 주소를 필터링할 수 있습니다. 예를 들어 ‘클라이언트 IP: 10.0.0.0*’를 입력하면 10.0.0.0로 시작하는 IP 주소가 검색됩니다.

### 로그 리스트
**반환된 행 수** 필드는 주로 SELECT 명령의 영향을 판단하는 데 사용되는 SQL 명령을 실행하여 반환된 행 수를 나타냅니다.

## SQL 감사 필드
TDSQL for MySQL 콘솔의 **감사 로그** 탭에서 다음 아이콘을 클릭하여 전체 SQL 감사 로그를 가져와 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3a6059efd97654507d310a6e7583b947.png)






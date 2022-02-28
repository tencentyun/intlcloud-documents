## 배경
TDSQL for MySQL은 2021년 04월 01일에 레거시 알람 정책 유형을 교체하고 수백 개의 모니터링 및 알람 메트릭을 수정하여 서버 및 설정 요소 서비스에 대한 모니터링 항목을 업그레이드했습니다. Cloud Monitor 콘솔에서 [TDSQL for MySQL](https://intl.cloud.tencent.com/document/product/248/40012) 유형의 알람 정책을 설정할 수 있습니다.

레거시 TDSQL(old) 정책 유형은 2021년 07월 29일에 비활성화되었습니다. 이 유형에서는 더 이상 새 알람 정책을 설정할 수 없으며 이전에 설정된 TDSQL 알람 정책은 새 정책 유형으로 점진적으로 이전됩니다.

**기존 알람 정책 유형과 신규 알람 정책 유형 비교:**

| 정책 유형      | 측정 범위                                       | 지원 및 유지 관리                              |
| ------------- | ------------------------------------- | ----------------------- |
| TDSQL(old)           | 8개 메트릭   | 이 정책 유형은 2021년 07월 29일에 비활성화되었으며 이후에 설정할 수 없습니다. 모든 기존 알람 정책은 새 정책 유형으로 이전됩니다. |
| 클라우드 데이터베이스 - TDSQL MySQL - 인스턴스    |37개 메트릭           | 이 정책 유형은 2021년 04월 01일에 런칭되었으며 지속적으로 유지 관리됩니다.         |

>!
>- 신규 MySQL for TDSQL 정책 유형은 레거시 TDSQL(old) 정책 유형의 모든 메트릭을 커버합니다. 자세한 내용은 [신규 및 기존 메트릭 비교표](#jump)를 참고하십시오.
> - 신규 알람 정책은 [신규 메트릭 설명](#jump2)을 참고하십시오.

## 알람 정책 마이그레이션
레거시 TDSQL(old) 정책 유형이 비활성화되면 시스템은 이전에 설정된 TDSQL(old) 알람 정책을 백엔드의 새로운 MySQL for TDSQL 정책 유형으로 자동 이전합니다.
>?일부 인스턴스 또는 사용자에 대해 시스템에서 알람을 신규 알람 정책 유형으로 자동 이전하지 않을 수 있습니다. 이 경우 메시지 센터, 이메일 또는 SMS를 통해 알려드립니다. 아래의 수동 전송 단계에 따라 알람을 수동으로 전송하십시오.

#### 수동 이전 단계
1. 기존 알람 메트릭 및 정책을 분류합니다.
  1. [클라우드 모니터링 콘솔](https://console.cloud.tencent.com/monitor/alarm2/policy)에 로그인하고 왼쪽 사이드바에서 [알람 설정] > [알람 정책]을 선택하고 [고급 필터]를 클릭합니다.
  2. 팝업 페이지의 ‘정책 유형’에서 ‘TDSQL(old)’에 해당하는 알람 정책 유형을 선택하고 이 범주의 알람 정책을 쿼리하고 원래 TDSQL(old) 정책 유형의 이전에 설정된 알람 정책을 다운로드합니다.
![](https://main.qcloudimg.com/raw/9ed66978c7d097f2465573b497f8f686.png)
2. 신규 알람 정책을 설정합니다.
  1. [알람 정책](https://console.cloud.tencent.com/monitor/alarm2/policy) 페이지에서 [생성]을 클릭합니다.
  2. 알람 정책 생성 페이지에서 ‘정책 유형’으로 [MySQL for TDSQL]을 선택하고 1단계에서 다운로드한 정책에 따라 알람을 설정합니다. 알람 설정 방법은 [알람 설정](https://intl.cloud.tencent.com/document/product/248/38916)을 참고하십시오.
3. MySQL for TDSQL 알람 정책이 활성화되어 있고 알람을 성공적으로 트리거할 수 있는지 확인합니다.
알람 정책 생성 페이지의 ‘메트릭 알람’에서 최소 트리거 임계값을 설정하고 [수신자 또는 수신자 그룹]을 설정하도록 선택한 다음 정책을 테스트할 알림 채널(이메일 또는 SMS)을 선택합니다. 예를 들어, 임계값이 1분의 한 통계 기간 동안 1%보다 크거나 같을 때 분당 한 번씩 알람을 트리거하는 CPU 사용률 메트릭에 대한 알람 정책을 설정할 수 있습니다.
4. 신규 정책 유형을 확인한 후 원래 TDSQL(old) 정책 유형에서 이전에 설정한 알람 정책을 삭제합니다.
[알람 정책](https://console.cloud.tencent.com/monitor/alarm2/policy) 페이지에서 TDSQL(old) ‘정책 유형’별로 알람 정책을 필터링하고 1단계에서 다운로드한 정책 목록에 따라 필터링된 정책을 삭제합니다. 
마이그레이션 중 문제가 발생하면 곧바로 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.

## [신규 및 기존 메트릭 비교표](id:jump)
<table>
<thead><tr><th><strong>기존 정책 유형</strong></th><th><strong>메트릭/이벤트 알람</strong></th><th><strong>레거시 메트릭/이벤트 알람 이름</strong></th><th><strong>새 정책 유형</strong></th><th><strong>신규 메트릭/이벤트 알람 이름</strong></th></tr></thead>
<tbody><tr>
<td rowspan="14">CDB - TDSQL(old)</td>
<td>메트릭 알람</td><td>CPU 사용률</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>원본 노드의 최대 CPU 사용률</td></tr>
<tr>
<td>메트릭 알람</td><td>저장 공간 활용</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>원본 노드의 최대 데이터 디스크 활용도</td></tr>
<tr>
<td>메트릭 알람</td><td>느린 쿼리</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>원본 노드의 총 느린 쿼리</td></tr>
<tr>
<td>메트릭 알람</td><td>활성 연결</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>총 활성 스레드</td></tr>
<tr>
<td>메트릭 알람</td><td>캐시 적중률</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>원본 노드의 최소 캐시 적중률</td></tr>
<tr>
<td>메트릭 알람</td><td>데이터베이스 연결</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>총 클라이언트 연결</td></tr>
<tr>
<td>메트릭 알람</td><td>프라이머리/세컨더리 지연</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>보조 노드 지연</td></tr>
<tr>
<td>메트릭 알람</td><td>프라이머리/세컨더리 전환</td>
<td>클라우드 데이터베이스 - TDSQL MySQL - 인스턴스</td><td>프라이머리/세컨더리 전환 수</td></tr>
</tbody></table>

## [신규 메트릭 설명](id:jump2)
<table>
<thead><tr><th><strong>정책 유형</strong></th><th><strong>메트릭/이벤트 알람</strong></th><th><strong>메트릭/이벤트 알람 이름</strong></th></tr></thead>
<tbody><tr>
<td rowspan="30">클라우드 데이터베이스 - TDSQL for MySQL</td>
<td>메트릭 알람</td><td>CPU 사용률</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 UPDATE 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>총 열린 연결</td></tr>
<tr>
<td>메트릭 알람</td><td>총 최대 연결 수</td></tr>
<tr>
<td>메트릭 알람</td><td>SQL 처리량</td></tr>
<tr>
<td>메트릭 알람</td><td>SQL 오류 처리량</td></tr>
<tr>
<td>메트릭 알람</td><td>SQL 성공 처리량</td></tr>
<tr>
<td>메트릭 알람</td><td>5ms 미만이 소요되는 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>5–20ms가 소요되는 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>20–30ms가 소요되는 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>30ms 이상 소요되는 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>모든 샤드의 최소 남은 Binlog 디스크 공간</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 Binlog 디스크 공간</td></tr>
<tr>
<td>메트릭 알람</td><td>최대 데이터베이스(DB) 연결 활용도</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 사용 가능한 데이터 디스크 공간</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 DELETE 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 최대 IO 활용도</td></tr>
<tr>
<td>메트릭 알람</td><td>innodb 디스크에서 총 논리적 읽기</td></tr>
<tr>
<td>메트릭 알람</td><td>미리 읽기 스레드가 innodb 버퍼 풀로 읽은 총 페이지 수</td></tr>
<tr>
<td>메트릭 알람</td><td>innodb 버퍼 풀의 총 논리적 읽기</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 innodb 테이블에서 DELETE된 총 행</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 innodb 테이블에 INSERT된 총 행</td></tr>
<tr>
<td>메트릭 알람</td><td>nnodb 테이블에서 READ된 총 행</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 innodb 테이블에서 UPDATE된 총 행</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 INSERT 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 사용 가능한 캐시</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 REPLACE_SELECT 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 노드의 총 REPLACE 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>원본 및 복제본 노드의 총 요청</td></tr>
<tr>
<td>메트릭 알람</td><td>총 SELECT 요청</td></tr>
</tbody></table>


## 2021년 09월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>Percona/MariaDB/MySQL 간의 이종 마이그레이션 지원</td>
<td>Percona/MariaDB/MySQL 간의 이종 마이그레이션을 지원합니다.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42644" target="_blank">MariaDB 또는 Percona에서 MySQL 로 마이그레이션</a></td></tr><tr>
<tr>
<td>데이터 구독의 TDSQL for MySQL 지원</td>
<td>DTS는 TDSQL for MySQL 구독을 지원합니다.</td>
<td>2021-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42663" target="_blank">데이터 구독이 지원하는 데이터베이스</a></td></tr>
</tbody></table>


## 2021년 08월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>사용자 정의 라우팅 정책 지원</td>
<td>MySQL 구독은 Kafka 파티션으로 라우팅하기 위한 사용자 정의 데이터 필드를 지원합니다.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42664" target="_blank">데이터 구독 작업 생성</a></td></tr><tr>
<td>TDSQL-C 데이터 동기화 지원</td>
<td>DTS는 TDSQL-C 인스턴스 간 데이터 동기화를 지원합니다.</td>
<td>2021-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42621" target="_blank">TDSQL-C에 대한 TDSQL-C 데이터 동기화</a></td></tr>
</tbody></table>


## 2021년 07월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<td>기본 알람 정책 지원</td>
<td>데이터 마이그레이션, 데이터 동기화 및 데이터 구독의 주요 이벤트 모니터링에 대한 기본 설정을 지원하여, 트리거된 이벤트를 즉시 알립니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42611" target="_blank">지원되는 이벤트 및 메트릭</a></td></tr>
<tr>
<td>데이터 마이그레이션 재시도 지원</td>
<td>데이터 마이그레이션 작업이 예외로 인해 중단된 경우 예외 수정 후 재시작 가능합니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42634" target="_blank">작업 재시도</a></td></tr>
<tr>
<td>TDSQL for PostgreSQL에 MySQL 데이터 동기화 지원</td>
<td>DTS는 MySQL에서 TDSQL for PostgreSQL로의 데이터 동기화를 지원합니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42622" target="_blank">TDSQL for PostgreSQL 및 TDSQL-A for PostgreSQL로 MySQL 데이터 동기화 지원</a></td></tr>
<tr>
<td>테이블 매핑 지원</td>
<td>대상 데이터베이스로 마이그레이션된 테이블의 이름을 변경할 수 있습니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42629" target="_blank">테이블 매핑</a></td></tr>
<tr>
<td>마이그레이션 진행률 세부 정보 조회 지원</td>
<td>마이그레이션 진행률 탭에서 원본 테이블, 대상 테이블, 예상 행 수, 완료된 행 수, 마이그레이션 상태 등 마이그레이션 진행률 세부 정보를 볼 수 있습니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42637" target="_blank">작업 조회</a></td></tr>
<tr>
<td>뷰 내보내기 기능 수정</td>
<td><li>수정 전: 뷰를 내보낼 때 대상 user@host와 동일한 definer만 마이그레이션할 수 있습니다.<li>수정 후: 뷰를 내보낼 때 DTS는 원본 데이터베이스의 `DEFINER`([DEFINER = user1])에 해당하는 user1이 마이그레이션 대상의 user2와 동일한지 확인합니다. 그렇지 않은 경우 DTS는 대상 데이터베이스의 user1의 `SQL SECURITY` 속성을 `DEFINER`에서 `INVOKER`([INVOKER = user1])로 변경하고 대상 데이터베이스의 `DEFINER`를 마이그레이션 대상의 user2([DEFINER = 마이그레이션 대상 user2])로 설정합니다.</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42561" target="_blank">뷰 확인</a></td></tr>
</tbody></table>


## 2021년 05월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>데이터 동기화 메트릭 모니터링 지원</td>
<td>데이터 동기화 작업의 메트릭을 모니터링할 수 있습니다.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42579" target="_blank">지원되는 이벤트 및 메트릭</a></td></tr>
<tr>
<td>MySQL 데이터 동기화 지원</td>
<td>DTS는 MySQL 데이터베이스 간의 실시간 데이터 동기화를 지원합니다. 클라우드-로컬 활성-활성, 다중 사이트 활성-활성, 다중 사이트 활성-활성 및 국경 간 데이터 동기화는 물론 실시간 데이터 웨어하우징을 통해 안전하고 확장 가능하며 가용성이 높은 데이터 아키텍처를 구축할 수 있습니다.</td>
<td>2021-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42624" target="_blank">MySQL 데이터베이스 간의 데이터 동기화</a></td></tr>
</tbody></table>



## 2021년 04월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>교차 계정 마이그레이션 지원</td>
<td>NewDTS는 계정 간 인스턴스 마이그레이션을 지원합니다.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/42646" target="_blank">교차 계정 인스턴스용 ApsaraDB 간 마이그레이션</a></td></tr>
<tr>
<td>데이터 마이그레이션 MySQL 8.0 지원</td>
<td>NewDTS는 MySQL 8.0 및 낮은 MySQL 버전에서 8.0으로의 데이터 마이그레이션을 지원합니다.</td>
<td>2021-04</td><td>-</td></tr>
</tbody></table>


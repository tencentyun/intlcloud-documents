TencentDB for MySQL은 단일 노드(클라우드 디스크 버전), 2노드(이전 고가용성 버전), 3노드(이전 파이낸스 버전)의 세 가지 유형의 아키텍처를 지원합니다.
>?클라우드 디스크 버전의 단일 노드 아키텍처는 현재 상하이, 청두, 광저우, 베이징, 중국홍콩 리전에서 지원되며 향후 더 많은 리전에서 사용할 수 있습니다.
>
## 인스턴스 아키텍처 보기
- 구매할 인스턴스는 [TencentDB for MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 들어가 **아키텍처** 섹션에서 아키텍처를 선택합니다.
- 인스턴스 구매 후 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 목록에서 대상 인스턴스를 찾은 다음 **구성** 열에서 아키텍처를 확인합니다.

## 각 아키텍처 비교
<table>
<thead>
<tr><th>아키텍처</th><th >2노드</th><th>3노드</th><th colspan=2>단일 노드</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">격리 정책</a></td>
<td>일반형</td><td>일반형</td><td>일반형(읽기 전용 인스턴스)</td><td>기본형</td></tr>
<tr>
<td>지원 버전</td>
<td>MySQL 5.5, 5.6, 5.7, 8.0</td><td>MySQL 5.6, 5.7, 8.0</td><td>MySQL 5.6, 5.7, 8.0</td><td>MySQL 5.7, 8.0</td></tr>
<tr>
<td>노드</td>
<td>1 원본, 1 복제본</td><td>1 원본, 2 복제본</td><td>단일 노드</td><td>단일 노드</td></tr>
<tr>
<td>원본-복제본 복제 모드</td>
<td>비동기화(기본값), 반동기화</td><td>비동기화(기본값), 강제 동기화, 반동기화</td><td>-</td><td>-</td></tr>
<tr>
<td>인스턴스 가용성</td>
<td>99.95%</td><td>99.99%</td><td>-</td><td>-</td></tr>
<tr>
<td>기본 스토리지</td>
<td>로컬 NVMe SSD</td><td>로컬 NVMe SSD</td><td>로컬 NVMe SSD</td><td>SSD 클라우드 디스크<br>인핸스드 SSD</td></tr>
<tr>
<td>성능</td>
<td>최대 240000 IOPS</td><td>최대 240000 IOPS</td><td>최대 240000 IOPS</td><td><li>SSD 클라우드 디스크 랜덤 IOPS 계산: <br>min{1800 + 30 × 용량(GB), 26000}<li>SSD 클라우드 디스크 처리량 계산(MB/s): <br>min{120 + 0.2 × 용량(GB), 260}<li>인핸스드 SSD 랜덤 IOPS 계산: <br>min{1800 + 50 × 용량(GB), 50000}<li>인핸스드 SSD 처리량 계산(MB/s): <br>min{120 + 0.5 × 용량(GB), 350}</td></tr>
<tr>
<td>적용 시나리오</td>
<td>게임, 인터넷, IoT, 소매, 전자 상거래, 물류, 보험, 증권 등</td>
<td>게임, 인터넷, IoT, 소매, 전자 상거래, 물류, 보험, 증권 등</td>
<td>읽기/쓰기 분리 요구 사항이 있는 애플리케이션</td>
<td>개인 학습, 소규모 웹 사이트, 비핵심 소규모 기업 시스템 및 중대형 기업 개발 및 테스트 환경</td></tr>
</tbody></table>

## 관련 문서
- TencentDB for MySQL는 MySQL 8.0, MySQL 5.7, MySQL 5.6, MySQL 5.5 버전을 지원합니다. 자세한 내용은 [데이터베이스 버전](https://intl.cloud.tencent.com/document/product/236/31896)을 참고하십시오.
- TencentDB for MySQL은 원본 인스턴스, 읽기 전용 인스턴스 및 재해 복구 인스턴스와 같은 인스턴스 유형을 지원합니다. 자세한 내용은 [데이터베이스 인스턴스 유형](https://intl.cloud.tencent.com/document/product/236/7268)을 참고하십시오.
- TencentDB for MySQL은 다양한 아키텍처별 기능을 지원합니다. 자세한 내용은 [기능 비교표](https://intl.cloud.tencent.com/document/product/236/36007)를 참고하십시오.

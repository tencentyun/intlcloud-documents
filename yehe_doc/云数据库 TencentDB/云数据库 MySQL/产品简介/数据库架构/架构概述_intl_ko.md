TencentDB for MySQL은 고가용성 버전, 파이낸스 버전, 단일 노드 고IO 버전 및 기본 버전 등 네 가지 구성이 있으며, 그중에서 단일 노드 고IO 버전은 현재 [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)에만 사용할 수 있습니다.

## 인스턴스 구성 조회
- 구매 시 [MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 로그인한 뒤, '구성'에서 해당하는 구성을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/f1417a645690900e4d82515e8e609d3b.png)
- 구매 후 [MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 뒤, 인스턴스 리스트의 '설정'에서 인스턴스 구성을 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/0f5f39c3eeb7bdbcd61d6ccf157c07b2.png)


## 아키텍처별 대조

<table>
<thead>
<tr>
<th width="15%">구성</th>
<th width="20%">고가용성 버전</th>
<th width="20%">파이낸스 버전</th>
<th width="20%">단일 노드 고IO 버전</th>
<th width="25%">기본 버전</th>
</tr>
</thead>
<tbody><tr>
<td>지원하는 버전</td>
<td>MySQL 5.5, 5.6, 5.7, 8.0</td>
<td>MySQL 5.6, 5.7, 8.0</td>
<td>MySQL 5.6, 5.7, 8.0</td>
<td>MySQL 5.7</td>
</tr>
<tr>
<td>노드</td>
<td>원 마스터 원 슬레이브</td>
<td>원 마스터 투 슬레이브</td>
<td>단일 노드</td>
<td>단일 노드</td>
</tr>
<tr>
<td>마스터/슬레이브 복제 방식</td>
<td>비동기화(기본), 반동기화</td>
<td>강제 동기화</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>인스턴스 가용성</td>
<td>99.95%</td>
<td>99.99%</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>하위 스토리지</td>
<td>로컬 NVMe SSD 디스크</td>
<td>로컬 NVMe SSD 디스크</td>
<td>로컬 NVMe SSD 디스크</td>
<td>고성능 클라우드</td>
</tr>
<tr>
<td>성능</td>
<td>최대 240000 IOPS</td>
<td>최대 240000 IOPS</td>
<td>-</td>
<td>IOPS 범위 계산 공식: <br>{min 1500 + 8 * 디스크 용량, max 4500}</td>
</tr>
<tr>
<td>적용 시나리오</td>
<td>게임, 인터넷, 사물인터넷(IoT), 소매 전자상거래, 물류, 보험, 증권 등 업종의 애플리케이션</td>
<td>게임, 인터넷, 사물인터넷(IoT), 소매 전자상거래, 물류, 보험, 증권 등 업종의 애플리케이션</td>
<td>읽기/쓰기 분리 수요가 있는 애플리케이션</td>
<td>개별 학습, 마이크로 사이트, 기업의 소규모 부가 시스템, 중견/대형 기업의 개발 및 테스트 환경</td>
</tr>
</tbody></table>

## 관련 문서
- TencentDB for MySQL에서 지원하는 버전: MySQL 8.0, MySQL 5.7, MySQL 5.6, MySQL 5.5, 자세한 내용은 [데이터베이스 버전](https://intl.cloud.tencent.com/document/product/236/31896)을 참조 바랍니다.
- TencentDB for MySQL에서 지원하는 인스턴스 유형: 마스터 인스턴스, 읽기 전용 인스턴스, 재해 복구 인스턴스, 자세한 내용은 [데이터베이스 인스턴스 유형](https://intl.cloud.tencent.com/document/product/236/7268)을 참조 바랍니다.
- TencentDB for MySQL의 각 아키텍처 유형별로 지원하는 기능이 다릅니다. 자세한 내용은 [기능 차이 리스트](https://intl.cloud.tencent.com/document/product/236/36007)를 참조 바랍니다.

TencentDB for MySQL은 고가용성 버전, 파이낸스 버전, 단일 노드 고IO 버전 및 기본 버전 등 4가지 구성이 있으며, 이 중 단일 노드 고IO 버전은 현재 [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)에만 사용됩니다.

## 인스턴스 구성 보기
- 구매 시 [MySQL 구매 페이지](https://buy.cloud.tencent.com/cdb)에 로그인한 후 “구성”에서 해당하는 구성을 선택할 수 있습니다.
![](https://main.qcloudimg.com/raw/5bbc8288b981097d8f6b36e150ddf7e2.png)
- 구매 후 [MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인한 후, 인스턴스 리스트의 “설정” 부분에서 인스턴스 구성을 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/f0618995c7b9f4821c0d4f18ce4a6f45.png)


## 각 구성 비교
<table>
<thead>
<tr><th width="15%">구성</th><th width="20%">고가용성 버전</th><th width="20%">파이낸스 버전</th><th width="20%">단일 노드 고IO 버전</th><th width="25%">기본 버전</th></tr>
</thead>
<tbody><tr>
<td>지원 버전</td>
<td>MySQL 5.5, 5.6, 5.7, 8.0</td>
<td>MySQL 5.6, 5.7, 8.0</td>
<td>MySQL 5.6, 5.7, 8.0</td>
<td>MySQL 5.7</td>
</tr>
<tr>
<td>노드</td>
<td>1 마스터 1 슬레이브</td>
<td>1 마스터 2 슬레이브</td>
<td>단일 노드</td>
<td>단일 노드</td>
</tr>
<tr>
<td>마스터/슬레이브 복제 방식</td>
<td>비동기화(기본), 반동기화</td>
<td>비동기화(기본), 강제 동기화, 반동기화</td>
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
<td>기본 스토리지</td>
<td>로컬 NVMe SSD 디스크</td>
<td>로컬 NVMe SSD 디스크</td>
<td>로컬 NVMe SSD 디스크</td>
<td>고성능 클라우드 디스크</td>
</tr>
<tr>
<td>성능</td>
<td>IOPS 최대 240000</td>
<td>IOPS 최대 240000</td>
<td>-</td>
<td>IOPS 범위 계산 공식:<br>{min 1500 + 8 * 디스크 용량，max 4500}</td>
</tr>
<tr>
<td>적용 시나리오</td>
<td>게임, 인터넷, 사물인터넷, 전자상거래 판매, 물류, 보험, 증권 분야 등의 애플리케이션</td>
<td>게임, 인터넷, 사물인터넷, 전자상거래 판매, 물류, 보험, 증권 분야 등의 애플리케이션</td>
<td>읽기/쓰기 분리가 필요한 어플리케이션</td>
<td>개별 학습, 미니 사이트, 기업의 소규모 부가 시스템, 중견/대형 기업의 개발 및 테스트 환경</td>
</tr>
</tbody></table>

## 관련 문서
- TencentDB for MySQL는 MySQL 8.0, MySQL 5.7, MySQL 5.6, MySQL 5.5 버전을 지원하며, 자세한 내용은 [데이터베이스 버전](https://intl.cloud.tencent.com/document/product/236/31896)을 참조하십시오.
- TencentDB for MySQL은 마스터 인스턴스, 읽기 전용 인스턴스, 재해 복구 인스턴스를 지원하며, 자세한 내용은 [데이터베이스 인스턴스 유형](https://intl.cloud.tencent.com/document/product/236/7268)을 참조하십시오.
- TencentDB for MySQL은 각 구성별 지원 기능이 상이합니다. 자세한 내용은 [기능 비교표](https://intl.cloud.tencent.com/document/product/236/36007)를 참조하십시오.

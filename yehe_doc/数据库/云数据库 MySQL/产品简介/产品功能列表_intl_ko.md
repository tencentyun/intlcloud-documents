## 제품 기능
본문은 다양한 유형의 TencentDB for MySQL 인스턴스에서 지원하는 현재 및 향후 기능을 비교하여 각 유형의 기능에 대해 자세히 안내하고, 최신 기능 빠르게 체험해 볼 수 있게 하여 가장 적합한 인스턴스를 구매할 수 있도록 도와줍니다.
>?
>- 표에서 ‘-’는 지원되지 않음을 의미합니다.
>- 테이블 제목을 클릭하여 기능 비교와 새로운 기능 목록을 확인할 수 있습니다.

<table >
<thead><tr><th>기능 카테고리</th><th>기능</th><th>2노드</th><th>3노드</th><th colspan = "2" >단일 노드</th></tr></thead>
<tbody>
<tr>
<td rowspan="10">라이프사이클</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794" target="_blank">격리 정책</a></td><td>일반 및 전용</td><td>일반 및 전용</td><td>일반(읽기 전용 인스턴스)</td><td>기본(클라우드 디스크 버전)</td></tr>
<tr>
<td>지원되는 버전</td><td><li>MySQL 5.5</li><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td>MySQL 5.7, 8.0</td></tr>
<tr>
<td>노드 수</td><td>2</td><td>3</td><td>1</td><td>1</td></tr>
<tr>
<td>메모리/디스크</td><td>최대 720GB/12TB</td><td>최대 720GB/12TB</td><td>최대 720GB/12TB</td><td>최대 16GB/30TB</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">인스턴스 생성</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">읽기 전용 인스턴스 생성</a></td><td>지원(MySQL 5.6, 5.7 및 8.0만 해당)</td><td>지원</td><td>지원</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7272" target="_blank">재해 복구 인스턴스 생성</a></td><td>지원 (MySQL 5.6, 5.7 및 8.0만 해당)</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31895" target="_blank">인스턴스 폐기</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/52515" target="_blank">종량제를 정액 과금제로 전환</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47702" target="_blank">자동 연장</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td rowspan="4">인스턴스 관리</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/10929" target="_blank">인스턴스 유지 관리 시간 구성</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8460" target="_blank">인스턴스 프로젝트 구성</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">구성 조정</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/44337" target="_blank">AZ 마이그레이션</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">버전 업그레이드</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8126" target="_blank">데이터베이스 엔진 버전 업그레이드</a></td><td>지원(MySQL 5.5 및 5.6만 해당)</td><td>지원</td><td>지원</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">커널 마이너 버전 업그레이드</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td>아키텍처 업그레이드</td><td><a href="https://intl.cloud.tencent.com/document/product/236/35986" target="_blank">2노드에서 3노드로 업그레이드</a></td><td>지원</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">지원되는 엔진</td>
<td>InnoDB</td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47015" target="_blank">RocksDB</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="7">백업 및 롤백</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">자동 백업</a></td><td>지원</td><td>지원</td><td>-</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">수동 백업</a></td><td>지원</td><td>지원</td><td>-</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38326" target="_blank">백업 삭제</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">인스턴스 클론</a></td><td>지원</td><td>지원</td><td>-</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7276" target="_blank">롤백</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">아카이브 백업 보관</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/51881" target="_blank">백업 암호화</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan=3>모니터링 및 알람</td>
<td>리소스 모니터링</td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td>엔진 모니터링</td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td>배포 모니터링</td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td>알람</td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td rowspan="6">계정 관리</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31900" target="_blank">계정 생성</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/49197" target="_blank">암호 복잡성 구성</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31901" target="_blank">비밀번호 재설정</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31902" target="_blank">계정 권한 수정</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31903" target="_blank">액세스 호스트 주소 수정</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31904" target="_blank">계정 삭제</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td>데이터베이스 관리</td><td><a href="https://intl.cloud.tencent.com/document/product/236/39221">DMC</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td rowspan="4">데이터 보안</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470">보안 그룹</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/43496">데이터베이스 감사</a></td><td>지원(MySQL 5.6 및 5.7만 해당)</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491">TDE 구성</a></td><td>지원(MySQL 5.7 및 8.0만 해당)</td><td>지원(MySQL 5.7 및 8.0만 해당)</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/48452">SSL 암호화 구성</a></td><td>지원(MySQL 5.6, 5.7 및 8.0만 해당)</td><td>지원(MySQL 5.6, 5.7 및 8.0만 해당)</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="3">데이터 채널</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8463">DTS로 마이그레이션</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8464">오프라인 마이그레이션</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8466">SQL 파일 가져오기</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">매개변수 관리</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/35793">인스턴스 매개변수 구성</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47701">지능형 매개변수 조정</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
<tr>
<td>네트워크</td><td><a href="https://intl.cloud.tencent.com/document/product/236/31915">네트워크 스위치</a></td><td>지원</td><td>지원</td><td>지원</td><td>지원</td></tr>
<tr>
<td rowspan="1">성능</td><td><a href="https://www.tencentcloud.com/document/product/236/42048">데이터베이스 프록시(새 버전)</a></td><td>지원</td><td>지원</td><td>-</td><td>-</td></tr>
</tbody>
</table>

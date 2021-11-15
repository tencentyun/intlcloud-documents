
## 2021년 07월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>터보 변경 지원</td>
<td>TencentDB for MySQL은 터보 변경 기능을 추가하여 로컬 잔여 리소스가 충분한 상황에서 데이터베이스 설정을 조정할 경우 터보 변경 기능을 사용할 수 있습니다. 터보 변경은 데이터 마이그레이션과 무관하게 진행되며 준비 단계의 대기 시간을 줄여 더욱 빠르게 인스턴스 사양을 변경할 수 있습니다. </td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">데이터베이스 인스턴스 사양 변경</a></td></tr>
</tbody></table>


## 2021년 04월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>데이터베이스 프록시 지원</td>
<td>데이터베이스 프록시는 CDB 서비스와 애플리케이션 서비스 사이에 위치한 네트워크 프록시 서비스입니다. 애플리케이션 서비스가 CDB에 액세스할 때 발생하는 모든 요청을 중계하는 데 사용됩니다. <br>데이터베이스 프록시 액세스 주소는 기존의 데이터베이스 액세스 주소와 별개이며, 데이터베이스 프록시 주소의 요청을 통해 프록시 클러스터 내 데이터베이스의 마스터/슬레이브 노드에 액세스하여 읽기/쓰기를 분리하고, 읽기 요청을 읽기 전용 인스턴스에 전달해 마스터 데이터베이스의 부하를 낮춥니다.</td>
<td>2021-04</td>
<td><a href="https://cloud.tencent.com/document/product/236/54652" target="_blank">데이터베이스 프록시</a></td></tr>
<tr>
<td>binlog 사용 용량이 디스크 총 사용 용량에 포함된 내용에 대한 설명</td>
<td>binlog의 입력 속도가 데이터베이스 실행 성능에 영향을 미칠 수 있습니다. TencentDB for MySQL의 성능 및 안정성 향상을 위해 TencentDB for MySQL에서 binglog 스토리지를 업그레이드합니다. 업그레이드가 완료되면 인스턴스 binlog의 스토리지 미디어가 고성능 SSD 디스크(사용자 인스턴스의 스토리지 용량)로 이동합니다.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40209" target="_blank">binlog 사용 용량이 디스크 총 사용 용량에 포함된 내용에 대한 설명</a></td></tr>
<tr>
<td>로컬 binlog 보관 주기 설정 지원</td>
<td>TencentDB for MySQL은 콘솔을 통해 로컬 binlog 보관 주기 설정을 지원합니다.</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40186" target="_blank">로컬 binlog 보관 설정</a></td></tr>
</tbody></table>

## 2021년 03월
<table>
<tr><th width=20%>업데이트 명칭</th><th width=50%>업데이트 설명</th><th width=10%>배포일</th><th width=20%>관련 문서</th></tr>
<tbody>
<tr>
<td>제품 아키텍처(명칭) 업그레이드</td>
<td>TencentDB for MySQL 제품 아키텍처는 단일 노드(구 기본 버전), 이중 노드(구 고가용성 버전) 및 3중 노드(구 파이낸스 버전)로 업그레이드할 수 있으며, 격리 정책으로 기본형, 범용형, 전용형이 추가됩니다. 각 아키텍처의 기능은 그대로 유지됩니다.</td>
<td>2021-03</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38328" target="_blank">아키텍처 개요</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39794">격리 정책</a></td></tr>
<tr>
<td>고유한 내부 네트워크 주소를 지원하는 읽기 전용 인스턴스</td>
<td>읽기 전용 인스턴스는 고유한 내부 네트워크 주소 활성화 및 내부 IP와 포트의 사용자 정의 변경을 지원합니다.</td>
<td>2021-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">읽기 전용 인스턴스 생성</a></td></tr>
</tbody></table>

## 2020년 11월
<table>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
<tbody>
<tr>
<td>인스턴스 클론 지원</td>
<td>TencentDB for MySQL은 클론을 통해 인스턴스를 로그 백업 보관 시간 내의 임의 시점으로 복구하거나, 지정된 물리 백업의 백업 세트에 복구합니다.</td>
<td>2020-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">인스턴스 클론</a></td>
</tr>
</tbody></table>

## 2020년 10월
<table>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
<tbody><tr>
<td>구매 페이지 기능 최적화</td>
<td>TencentDB for MySQL 구매 페이지는 알람 정책, 매개변수 템플릿, 프로젝트 간 보안 그룹 바인딩 지정 기능을 지원합니다.</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">MySQL 인스턴스 생성</a></td>
</tr>
<tr>
<td>8.0 버전 TDE 지원</td>
<td>TencentDB for MySQL 8.0 버전은 TDE 기능을 지원합니다.</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">TDE 활성화</a></td>
</tr>
</tbody></table>

## 2020년 08월
<table>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
<tbody><tr>
<td>MySQL 8.0 지원</td>
<td>TencentDB for MySQL 8.0 버전은 완벽한 관리 서비스와 TXSQL 커널을 결합하여 더욱 빠르고 안정적인 기업급 서비스와 다양한 분야별 시나리오를 제공함으로써 클라이언트의 사업 확장을 돕습니다.</td>
<td>2020-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">데이터베이스 버전</a></td>
</tr>
</tbody></table>

## 2020년 07월
<table>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
<tbody><tr>
<td>애플리케이션 매개변수 템플릿 및 인스턴스 지원</td>
<td>TencentDB for MySQL은 매개변수 템플릿을 지원하는 동시에 여러 인스턴스의 매개변수를 수정합니다. 또한 사용자가 정의한 시간 내에 매개변수 수정 작업을 실행하거나 취소할 수 있도록 지원합니다.</td>
<td>2020-07</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/35793" target="_blank">인스턴스 매개변수 설정</a><li><a href="https://intl.cloud.tencent.com/document/product/236/31906" target="_blank">매개변수 템플릿 사용</a></td>
</tr>
<tr>
<td>TDE 지원</td>
<td>TencentDB for MySQL은 TDE 기능을 제공합니다. TDE란 데이터의 암호화와 복호화 작업을 투명하게 진행한다는 뜻이며, 데이터 파일에 대한 실시간 I/O 암호화 및 복호화를 지원합니다. 또한 데이터를 디스크에 입력하기 전 암호화하고, 디스크에서 메모리로 읽어올 때 복호화하여 정적 데이터 암호화의 컴플라이언스 요건을 충족할 수 있습니다.</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">TDE 활성화</a></td>
</tr>
</tbody></table>

## 2020년 06월
<table>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
<tbody><tr>
<td>커널 마이너 버전 수동 업그레이드 지원</td>
<td>TencentDB for MySQL은 커널 마이너 버전 수동 업그레이드를 지원합니다. 커널 마이너 버전 업그레이드로 새 기능 사용, 성능 향상, 문제 해결 등의 기능을 사용할 수 있습니다.</td>
<td>2020-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">커널 마이너 버전 업그레이드</a></td>
</tr>
</tbody></table>

## 2020년 04월
<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>고가용성 버전(1 마스터 2 슬레이브)을 파이낸스 버전으로 변경</td>
<td>1 마스터 2 슬레이브 3중 노드 아키텍처를 사용하는 파이낸스 버전은 강제 동기화 복사 방식을 지원하며, 실시간 핫 백업을 통한 데이터의 일관성 유지로 파이낸스급 신뢰성과 고가용성을 제공합니다.</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">데이터베이스 아키텍처</a></td>
</tr>
<tr>
<td>사용자 정의 구 IP 주소 회수 시간 지원</td>
<td>네트워크 전환 시 사용자 정의 구 IP 주소의 회수 시간을 지원합니다. 범위는 0~168시간까지 설정할 수 있습니다. 구 IP 주소의 회수 시간을 0시간으로 설정하면 네트워크 전환 후 즉시 구 IP 주소가 회수됩니다.</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">네트워크 전환</a></td>
</tr>
</tbody></table>

## 2020년 01월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>DBbrain 지원</td>
<td>DBbrain은 데이터베이스를 스마트하게 진단하고 최적화하는 제품입니다. 데이터베이스에 대한 근본적 예방 차원에서 데이터베이스를 실시간으로 보호하며 장애의 원인을 효율적으로 찾아내 솔루션을 제공합니다.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36027" target="_blank">DBbrain</a></td>
</tr>
<tr>
<td>슬로우 로그 및 오류 로그의 상세 내역 지원</td>
<td>TencentDB for MySQL(기본 버전 미포함) 인스턴스는 작업 로그 관리 기능을 제공합니다. 콘솔의 작업 로그 페이지에서 인스턴스의 슬로우 로그 및 오류 로그 상세 내역과 롤백 로그를 조회할 수 있으며 슬로우 로그를 다운로드할 수 있습니다.</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/34588" target="_blank">작업 로그</a></td>
</tr>
</tbody></table>

## 2019년 12월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>MySQL 백업 상용화 요금</td>
<td>MySQL 인스턴스 백업이 제공된 용량을 초과하면 요금이 부과됩니다. 백업 상용화 후 데이터 압축, 백업의 안정성과 가용성이 크게 향상되어 백업이 더욱 안전해졌습니다. 사용자는 백업 보관 일수와 백업 빈도를 줄여 백업 비용을 절감할 수 있습니다.</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">백업 용량 요금 설명</a></td>
</tr>
</tbody></table>

## 2019년 11월
<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>이벤트 알람 지원</td>
<td>구독 메모리 OOM, 마스터/슬레이브 전환, 읽기 전용 인스턴스 삭제, 서버 장애로 인한 인스턴스 마이그레이션 등 이벤트를 통해 인스턴스 실행 상태를 신속히 확인할 수 있습니다.</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8457" target="_blank">알람 기능</a></td>
</tr>
</tbody></table>

## 2019년 09월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>데이터베이스 백업 페이지 런칭</td>
<td>TencentDB for MySQL 데이터베이스 백업 페이지가 런칭됩니다. 크게 개요와 백업 리스트로 나뉘며, 개요 페이지에서는 편리하게 백업 용량의 상세 내역과 사용 추세를 조회할 수 있고, 백업 리스트에서는 데이터 백업 리스트와 로그 백업 리스트를 명확하게 확인할 수 있습니다.</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/33131" target="_blank">백업 용량 조회</a></td>
</tr>
</tbody></table>

## 2019년 05월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>자동 백업의 백업 유형을 물리 백업으로 업그레이드</td>
<td>TencentDB for MySQL은 자동 백업 이후 물리 백업만 지원합니다. 기존 저장 콘텐츠 자동 백업이 로직 백업인 인스턴스는 순차적으로 물리 백업으로 자동 전환됩니다. 로직 백업이 필요한 경우 TencentDB for MySQL 콘솔에서 수동 백업 기능 또는 API 호출로 로직 백업을 생성할 수 있습니다.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">백업 방식</a></td>
</tr>
<tr>
<td>난징 1존 서버 오픈</td>
<td>난징 1존 서버 오픈으로 TencentDB for MySQL은 화둥 지역에서 상하이와 난징의 2개 리전을 보유하게 되었습니다.</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8458" target="_blank">리전과 가용존</a></td>
</tr>
</tbody></table>

## 2019년 03월

<div class="doc-table-wrap"><table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>VPC 간 전환 지원</td>
<td>VPC A의 VPC B 전환을 지원합니다. 단일 CDB의 VPC A를 VPC B로 전환할 수 있습니다.</td>
<td>2019-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">네트워크 전환</a></td>
</tr>
</tbody></table></div>

## 2019년 02월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>원클릭 연결 진단</td>
<td>콘솔에서는 사용자가 내부/외부 네트워크 연결 문제를 빠르게 확인하고 해결할 수 있도록 원클릭 연결 진단 툴 및 적합한 솔루션을 제공합니다.</td>
<td>2019-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">원클릭 연결 진단 툴</a></td>
</tr>
</tbody></table>

## 2018년 06월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>기본 버전 인스턴스 구매 지원</td>
<td>기본 버전은 단일 노드 배포를 사용하여 컴퓨팅과 스토리지를 분리합니다. 컴퓨팅 노드에 장애가 발생하면 노드 변환을 통해 빠르게 복구할 수 있습니다. MySQL 기본 버전의 기본 스토리지 미디어는 고성능 클라우드 디스크를 사용하여 90%의 I/O 시나리오에 적합하며, 저렴한 가격, 우수한 품질, 안정적인 성능이 특징입니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">데이터베이스 아키텍처</a></td>
</tr>
<tr>
<td>네트워크 전환 지원</td>
<td>기본 네트워크 전환은 VPC와 VPC 서브넷 간의 전환입니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">네트워크 전환</a></td>
</tr>
<tr>
<td>자체 연결 점검 지원</td>
<td>데이터베이스가 정상적으로 연결되어 있는지 점검합니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">원클릭 연결 진단 툴</a></td>
</tr>
<tr>
<td>다운그레이드 환불 지원</td>
<td>데이터베이스 설정을 낮추면 잔여 요금이 환불됩니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32345" target="_blank">인스턴스 요금 조정 설명</a></td>
</tr>
<tr>
<td>MySQL 5.7 데이터 마이그레이션 지원</td>
<td>DTS 데이터 마이그레이션은 MySQL 5.7 버전을 지원합니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">MySQL 데이터 온라인 가져오기</a></td>
</tr>
<tr>
<td>제품명 변경</td>
<td>기존의 CDB for MySQL에서 TencentDB for MySQL로 제품명을 변경하였습니다.</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236" target="_blank">TencentDB for MySQL</a></td>
</tr>
</tbody></table>

## 2017년 08월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>읽기 전용 인스턴스의 탄력적 사양 지원</td>
<td>마스터 인스턴스와 동일한 사양이 아니어도 됩니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">읽기 전용 인스턴스</a></td>
</tr>
<tr>
<td>1분 단위로 모니터링 지원</td>
<td>1분 단위로 데이터베이스를 모니터링합니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8455" target="_blank">모니터링 기능</a></td>
</tr>
<tr>
<td>물리 백업 지원</td>
<td>물리 백업 방식으로 데이터를 저장합니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">백업 방식</a></td>
</tr>
<tr>
<td>수동 백업 지원</td>
<td>백업 시간과 스토리지 시간을 사용자 정의한 경우, 백업은 최대 732일 동안 저장할 수 있습니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">백업 방식</a></td>
</tr>
<tr>
<td>보안 그룹 지원</td>
<td>보안 그룹은 필터링 기능이 포함된 스테이트풀 가상 방화벽의 일종으로, 단일 또는 다중 CDB의 네트워크 액세스 제어 설정에 사용되며 Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 방법입니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470" target="_blank">CDB 보안 그룹</a></td>
</tr>
<tr>
<td>데이터 구독 지원</td>
<td>DTS는 사용자가 CDB의 실시간 증분 업데이트 데이터를 획득하도록 돕습니다. 사용자는 비즈니스 요구사항에 따라 증분 데이터를 소비합니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/8774" target="_blank">데이터 구독</a></td>
</tr>
<tr>
<td>CDB와 CDB 간의 데이터 마이그레이션 지원</td>
<td>DTS 데이터 마이그레이션은 다양한 네트워크 환경과 호환됩니다.</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">MySQL 데이터 온라인 가져오기</a></td>
</tr>
</tbody></table>

## 2017년 06월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>MySQL 5.7 지원</td>
<td>MySQL 5.6 커널을 기반으로 MySQL 5.7(Percona 브랜치)이 추가되었습니다. MySQL 5.7 기능을 바탕으로 수평적 확장, 읽기/쓰기 분리 등 기존 기능도 유지됩니다.</td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">데이터베이스 버전</a></td>
</tr>
</tbody></table>

## 2016년 03월

<table>
<thead>
<tr>
<th width=20%>업데이트 명칭</th>
<th width=50%>업데이트 설명</th>
<th width=10%>배포일</th>
<th width=20%>관련 문서</th>
</tr>
</thead>
<tbody><tr>
<td>읽기 전용 인스턴스 런칭</td>
<td>TencentDB for MySQL은 1개 이상의 읽기 전용 인스턴스 생성을 지원합니다. 사용자의 읽기/쓰기 분리 및 1 마스터 다중 슬레이브 응용 시나리오를 지원함으로써 데이터베이스의 읽기 부하 성능이 대폭 향상될 수 있습니다.</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">읽기 전용 인스턴스</a></td>
</tr>
<tr>
<td>종량제 인스턴스 지원</td>
<td>시간 단위로 데이터베이스 서비스를 제공합니다.</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/18335" target="_blank">과금 개요</a></td>
</tr>
</tbody></table>

본문은 TencentDB for MySQL 콘솔에서 데이터베이스 프록시를 활성화하는 방법을 설명합니다.

데이터베이스 프록시는 TencentDB 서비스와 애플리케이션 서비스 간의 네트워크 프록시 서비스입니다. 애플리케이션 서비스가 데이터베이스에 액세스할 때 모든 요청을 프록시하는 데 사용됩니다. 자동 읽기/쓰기 분리, 트랜잭션 분할, 연결 풀, 연결 지속성 등의 고급 기능을 제공하며 고가용성, 고성능, Ops 지원 및 사용 편의성 등의 특징이 있습니다.

## 전제 조건
- 인스턴스가 실행 중이고 2노드 또는 3노드 아키텍처를 사용합니다.
- 인스턴스 배포 방식이 단일 가용존입니다.

## 주의 사항
- 데이터베이스 프록시는 현재 다음 리전에서 지원됩니다.
  - 베이징(1, 2, 4존 제외), 상하이(1존 제외), 광저우(1, 2존 제외), 청두, 충칭, 난징, 홍콩(1존 제외).
  - 도쿄(1존 제외), 방콕(1존 제외), 버지니아(1존 제외), 실리콘밸리(1존 제외), 뭄바이(1존 제외), 서울(1존 제외), 싱가포르(1, 2존 제외).
- 데이터베이스 프록시는 현재 다음 버전에서 지원됩니다. 2노드 및 3노드 MySQL 5.7(커널 마이너 버전 20211030 이상 포함) 및 3노드 MySQL 8.0(커널 마이너 버전 20211202 이상 포함). 원본 인스턴스의 커널 마이너 버전을 업그레이드하면 연결된 읽기 전용 및 재해 복구 인스턴스가 동시에 업그레이드됩니다. 자세한 내용은 [커널 마이너 버전 업그레이드](https://intl.cloud.tencent.com/document/product/236/36816)를 참고하십시오.

## 작업 단계
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 프록시를 활성화할 원본 인스턴스를 선택하고, 인스턴스 ID 혹은 **작업**열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 프록시** 탭을 선택하고 **지금 활성화**를 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vMSm892_10.png)
3. 팝업 창에서 다음 항목을 구성하고 **확인**을 클릭합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZUjv978_11.png)
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>네트워크</td>
<td>VPC만 될 수 있는 데이터베이스 프록시의 네트워크를 선택합니다.</td></tr>
<tr>
<td>프록시 사양</td>
<td>2코어 4000MB 메모리, 4코어 8000MB 메모리 또는 8코어 16000MB 메모리를 선택합니다.</td></tr>
<tr>
<td>AZ 및 노드 수량</td>
<td>1. 데이터베이스 프록시 AZ를 선택합니다. <strong>AZ 추가</strong>를 클릭하여 AZ를 더 추가할 수 있습니다. 선택 가능한 AZ의 수는 현재 리전에서 사용 가능한 AZ의 수에 따라 다릅니다. 최대 3개의 AZ를 선택할 수 있습니다. <br>2. 노드 수량을 선택합니다. 원본 및 읽기 전용 인스턴스에서 총 CPU 코어 수의 1/8(반올림)로 수량을 설정하는 것이 좋습니다. 예를 들어 원본 인스턴스에 4개의 CPU 코어가 있고 읽기 전용 인스턴스에 8개의 CPU 코어가 있는 경우 권장 노드 수 = (4 + 8) / 8 ≈ 2입니다. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">참고</div>        <div class="rno-document-tip-desc"><ol><li>선택한 데이터베이스 프록시가 원본 인스턴스와 동일한 AZ에 있지 않은 경우 프록시를 통해 데이터베이스에 연결할 때 쓰기 성능이 떨어질 수 있습니다. </li><li>계산된 필요한 프록시 노드 수가 구매 한도를 초과하는 경우 더 높은 프록시 사양을 선택하는 것이 좋습니다. </li></ol></div>    </div></blockquote></td></tr>
<tr>
<td>보안 그룹</td>
<td>소스 인스턴스의 보안 그룹은 기본적으로 선택됩니다. 다른 기존 보안 그룹을 선택하거나 필요에 따라 새 보안 그룹을 생성할 수도 있습니다. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">참고</div>        <div class="rno-document-tip-desc"><p>데이터베이스 프록시를 통해 접근하려면 보안 그룹 정책을 구성하고 사설 포트(3306)를 열어야 합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/236/14470">TencentDB 보안 그룹 관리</a>를 참고하십시오.</p></div>    </div></blockquote></td></tr>
<tr>
<td>비고</td>
<td>(선택 사항) 활성화할 데이터베이스 프록시 서비스의 설명을 입력합니다.</td></tr>
</tbody></table>
4. 서비스를 성공적으로 활성화한 후 프록시 노드를 관리하고 데이터베이스 프록시 페이지에서 해당 기본 정보를 볼 수 있습니다. 또한 데이터베이스 프록시의 액세스 주소, 네트워크 유형 및 비고를 수정하고, 연결 구성을 보고 조정하며, 연결 주소 섹션에서 리밸런싱을 수행할 수 있습니다.
>?
>- 프록시 노드 목록에서 **연결 수**를 확인하거나 각 프록시 노드의 성능 모니터링 데이터를 확인하여 노드의 연결 수가 불균형한지 확인할 수 있으며, 불균형한 경우 **리밸런싱**을 클릭하여 연결을 분산할 수 있습니다.
>- 리밸런싱으로 인해 프록시 노드가 다시 시작되고 다시 시작하는 동안 서비스를 일시적으로 사용할 수 없게 됩니다. 사용량이 적은 시간에 서비스를 다시 시작하는 것이 좋습니다. 귀하의 비즈니스에 재연결 메커니즘이 있는지 확인하십시오.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CH3a932_12.png)


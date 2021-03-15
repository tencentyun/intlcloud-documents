사용자가 더 빠르게 콘솔을 파악하고 사용할 수 있도록 자주 사용하는 서비스를 각 사용자의 니즈에 맞게 분류하여 정리했습니다. 현재 콘솔은 기본 서비스, 시나리오 서비스, 데이터센터, 라이브 방송 툴박스 등 4개의 모듈로 나뉘어 여러 사용 시나리오에 사용됩니다.

## 기본 서비스
기본 서비스는 주로 CSS의 액세스에 사용되며, 기본적인 CSS 서비스에 액세스하려면 기본 서비스 모듈 내에서 조작하면 됩니다.


<table>
<tr><th width="17%">기능 명칭</th>
<th>기능 설명</th>
</tr>
<tr>
<td ><a href = "https://cloud.tencent.com/document/product/267/20379">개요</a></td>
<td><ul style = "margin-bottom: 0px;"><li>과금 대역폭/트래픽 추세 등 관련 데이터와 라이브 방송의 실시간 데이터, 라이브 온라인 인원 등을 조회할 수 있습니다.</li><li>필요에 따라 과금 방식 전환 혹은 시간당 데이터 분할 정도를 수정할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20381">도메인 관리</a></td>
<td><ul style = "margin-bottom: 0px;"><li>자유 가속 도메인을 추가하고 관리할 수 있으며, 도메인에 CNAME 설정을 할 수 있습니다.</li><li>라이브 방송 도메인에 이미 생성된 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크, 콜백 기능 템플릿을 호출할 수 있습니다.</li><li>라이브 방송 도메인에 인증, HTTPS 프로토콜, 가속 지역, 원본 서버 등 정보를 설정할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20380">스트리밍 관리</a></td>
<td>라이브 방송 온라인 스트리밍 및 이전 스트리밍, 푸시 스트림 금지 관리와 라이브 방송 스트리밍을 금지하거나 푸시 스트림 복구 등 작업을 할 수 있습니다.</td>
</tr></tr>
</table>

## 시나리오 서비스
시나리오 서비스는 CSS의 부가적인 서비스를 통합한 것으로, 트랜스 코딩, 워터마크, 혼합 스트림, 화면 캡처와 음란물 감지, 이벤트 기록과 알림 서비스, 라이브 방송 SDK의 사용과 관리 등을 포함합니다. 관련 서비스를 사용하려면 모듈에서 관련 설정을 하십시오.


<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://cloud.tencent.com/document/product/267/20387">기능 설정</a></td>
<td>라이브 방송에 필요한 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등 기능의 템플릿 설정 서비스를 제공해 페이지 리디렉션의 복잡도를 감소시키기 위해 템플릿 도메인 바인딩 과정을 추가했습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20388">이벤트 센터</a></td>
<td><ul style= "margin: 0"><li>트리거된 각 사건 설정에 따라 관련 콜백 정보의 경로를 수신합니다.</li><li>라이브 방송 푸시 스트림 중단 기록과 중단 원인을 빠르게 조회할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/32405">라이브 방송 SDK</a></td>
<td><ul style= "margin: 0"><li>모바일 라이브 방송 SDK와 결합하여 정식 버전 License를 추가하고 관리할 수 있습니다.</li><li>IM 애플리케이션을 추가하고 조회해 개발 중 필요한 SDKAPPID와 SecretKey를 생성할 수 있습니다.</li><li>모바일 라이브 방송 SDK 중의 마이크 연결 기능 사용 시간과 패키지의 사용 현황을 조회할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/47152">클라우드 스튜디오</a></td>
<td>CSS 콘솔로 온라인 디렉터 기능을 실현할 수 있습니다.</td>
</tr></tr>
<tr>
<td><a href = "https://cloud.tencent.com/document/product/267/34286">LCB</a></td>
<td><ul style= "margin: 0"><li>LCB 서비스(대규모 멀티미디어 업스트림 시나리오에 적합)를 사용할 수 있습니다.</li><li>LCB에 사용할 가속 도메인을 추가하고 관리하고, 이미 설정된 콜백/녹화 템플릿을 호출할 수 있습니다.</li><li>LCB에서 생산하는 다운스트림 트래픽/대역폭 현황을 조회할 수 있습니다.</li><li>LCB 사용 중 라이브 방송 동시 녹화 채널 수를 조회할 수 있습니다.</li></ul></td>
</tr>
</table>


## 데이터센터
데이터 분석은 사용자에게 전문적인 데이터 분석 서비스를 제공해 시간 데이터 분할 정도 내의 트래픽/대역폭, 트랜스 코딩, 워터마크, 공유, 화면 캡처와 음란물 감지의 소모 현황을 조회할 수 있습니다. 그리고 로그 분석 기능을 제공해 사용자는 편하게 리소스를 모니터링하고 유용한 데이터를 파악할 수 있습니다.

<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th>
</tr><tr>
<td ><a href = "https://cloud.tencent.com/document/product/267/20390">데이터 통계</a></td>
<td><ul style = "margin-bottom: 0px;"><li>과금 항목에 트래픽/대역폭, 음란물 감지 화면 캡처, 트랜스 코딩, 녹화, 공유에서 생산되는 관련 데이터를 조회할 수 있습니다.</li><li>라이브 방송 운영 데이터를 분석하고 조회할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20391">스트리밍 데이터 조회</a></td>
<td>하나의 비디오 스트리밍의 푸시 스트림 및 재생 데이터를 조회하고 로컬로 내보낼 수 있습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20382">SDK 품질 모니터링</a></td>
<td>모바일 라이브 방송 SDK의 최근 3일 푸시 스트림 데이터 정보를 조회할 수 있습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/33996">로그 분석</a></td>
<td><ul style = "margin-bottom: 0px;"><li>라이브 방송 방문 로그를 실시간으로 수집한 후 클리닝해 분석과 검색으로 빠르게 장애 위치를 파악하고 액세스 할 수 있습니다.</li><li>전날, 최근 일주일, 최근 한달 혹은 사용자가 정의한 시간대의 로그 데이터 패키지를 다운로드 할 수 있습니다.</li></ul></td>
</tr>
</table>


## 라이브 방송 툴박스
라이브 방송 툴박스는 라이브 방송 과정의 서비스를 보장하는 부가 기능을 제공합니다.

<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th>
</tr><tr>
<td ><a href = "https://cloud.tencent.com/document/product/267/35257">주소 생성기</a></td>
<td>작성된 주소로 정보를 모아 사용자가 빠르게 푸시 스트림/재생 지도를 생성하는 것을 돕습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/43392">Web 푸시 스트림</a></td>
<td>신속하게 푸시 스트림 주소를 생성해 온라인 푸시 스트림으로 라이브 방송 기능을 테스트 할 수 있습니다.</td>
</tr><tr>
<td><a href="https://console.cloud.tencent.com/live/tools/selfcheck">자가 진단</a></td>
<td>자주 발생하는 라이브 방송 푸시 스트림/재생 문제를 진단할 수 있습니다. 현재는 베타 테스트 단계이므로, 진단 결과는 참고용으로만 사용하시기 바랍니다.</td>
</tr></tr>
</table>


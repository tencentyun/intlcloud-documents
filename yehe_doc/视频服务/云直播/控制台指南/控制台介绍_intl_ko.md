사용자가 더 빠르게 콘솔을 파악하고 사용할 수 있도록 자주 사용하는 서비스를 각 사용자의 요구사항에 맞게 분류하여 정리했습니다. 현재 콘솔은 기본 서비스, 시나리오 서비스, 데이터센터, 라이브 방송 툴박스 등 4개의 모듈로 나뉘어 여러 사용 시나리오에 사용됩니다.

## 기본 서비스
기본 서비스는 주로 CSS의 액세스에 사용되며, 기본적인 CSS 서비스에 액세스하려면 기본 서비스 모듈 내에서 조작하면 됩니다.

<table>
<tr><th width="17%">기능 명칭</th>
<th>기능 설명</th>
</tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/267/31054">개요</a></td>
<td><ul style = "margin-bottom: 0px;"><li>과금 대역폭/트래픽 추세 등 관련 데이터 및 라이브 방송 실시간 데이터, 라이브 방송 온라인 시청자 수를 확인할 수 있습니다.</li><li>필요에 따라 과금 방식 또는 시간 단위를 변경할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/35970">도메인 관리</a></td>
<td><ul style = "margin-bottom: 0px;"><li>외부 가속 도메인을 추가 및 관리할 수 있으며 도메인에 CNAME을 설정할 수 있습니다.</li><li>온라인에서 해당 라이브 방송 주소를 생성할 수 있습니다.</li><li>라이브 방송 도메인에 이미 생성한 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크, 콜백 기능 템플릿을 호출할 수 있습니다.</li><li>라이브 방송 도메인에 인증, HTTPS 프로토콜, 가속 지역, 원본 서버 등의 정보를 설정할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/31068">스트림 관리</a></td>
<td>라이브 방송의 온라인 스트림, 이전 스트림, 푸시 스트림 금지를 관리할 수 있으며 라이브 방송 스트리밍을 차단하거나 복구하는 등의 작업을 할 수 있습니다.</td>
</tr></tr>
</table>


## 시나리오 서비스
시나리오 서비스는 CSS의 부가적인 서비스를 통합한 것으로, 트랜스 코딩, 워터마크, 혼합 스트림, 화면 캡처와 음란물 감지, 이벤트 기록과 공지 서비스, 라이브 방송 SDK의 사용과 관리 등을 포함합니다. 본 모듈의 관련 설정 진행을 통해 서비스를 이용할 수 있습니다.

<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/267/31073">기능 설정</a></td>
<td>라이브 방송에 필요한 녹화, 트랜스 코딩, 음란물 감지 화면 캡처, 워터마크 등 기능의 템플릿 설정 서비스를 제공합니다. 페이지 리디렉션의 복잡도를 줄이기 위해 템플릿 도메인 바인딩 과정을 추가했습니다.</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/31074">이벤트 센터</a></td>
<td><ul style= "margin: 0"><li>트리거된 각 이벤트 설정에 따라 관련 콜백 정보의 경로를 수신합니다.</li><li>라이브 방송 푸시 스트리밍 중단 기록과 원인을 빠르게 조회할 수 있습니다.</li></ul></td>
</tr></tr>
</table>

## 데이터센터
데이터 분석은 사용자에게 전문적인 데이터 분석 서비스를 제공해 시간 데이터 분할 정도 내의 트래픽/대역폭, 트랜스 코딩, 워터마크, 공유, 화면 캡처와 음란물 감지의 소모 현황을 조회할 수 있습니다. 그리고 로그 분석 기능을 제공해 사용자는 편하게 리소스를 모니터링하고 유용한 데이터를 파악할 수 있습니다.

<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th>
</tr><tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/267/31076">데이터 통계</a></td>
<td><ul style = "margin-bottom: 0px;"><li>트래픽/대역폭, 음란물 감지 화면 캡처, 트랜스 코딩, 녹화, 푸시 시 발생하는 과금 항목 관련 데이터를 조회할 수 있습니다.</li><li>라이브 방송 운영 데이터를 분석하고 조회할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/31077">스트림 데이터 조회</a></td>
<td>단일 비디오 스트림에 대한 푸시 스트리밍 및 재생 데이터 상세 정보를 조회하고 로컬로 내보낼 수 있습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/20382">SDK 품질 모니터링</a></td>
<td>MLVB SDK의 최근 3일 푸시 스트림 데이터 정보를 조회할 수 있습니다.</td>
</tr><tr>
<td><a href = "https://cloud.tencent.com/document/product/267/33996">로그 분석</a></td>
<td><ul style = "margin-bottom: 0px;"><li>라이브 방송 방문 로그를 실시간으로 수집한 후 클리닝해 분석과 인덱스로 빠르게 장애 위치를 파악하고 액세스 할 수 있습니다.</li><li>전날, 최근 일주일, 최근 한달 혹은 사용자가 정의한 시간대의 로그 데이터 패킷을 다운로드 할 수 있습니다.</li></ul></td>
</tr>
</table>

## 라이브 방송 툴박스
라이브 방송 툴박스는 라이브 방송 과정의 서비스를 보장하는 부가 기능을 제공합니다.

<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th>
</tr><tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/267/31084">주소 생성기</a></td>
<td>작성된 주소로 정보를 스티칭하여 사용자의 빠른 푸시 스트림/재생 주소 생성을 지원합니다.</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/35968">Web 푸시</a></td>
<td>신속하게 푸시 스트림 주소를 생성해 온라인 푸시 스트림으로 라이브 방송 기능을 테스트 할 수 있습니다.</td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39467">자가 진단</a></td>
<td>자주 발생하는 라이브 방송 푸시 스트림/재생 문제를 신속하게 진단할 수 있습니다. 현재는 알파 테스트 단계이므로, 진단 결과는 참고용으로만 사용하시기 바랍니다.</td>
</tr>
<tr>
<td><a href="https://cloud.tencent.com/document/product/267/55670">풀 스트림 전송</a></td>
<td>콘텐츠 풀링 및 푸시 기능을 제공하며, 라이브 방송의 스트림을 푸시할 필요 없이 빠르게 기존의 비디오/라이브 방송을 풀링하여 타깃 주소로 푸시합니다.</td>
</tr>
</table>

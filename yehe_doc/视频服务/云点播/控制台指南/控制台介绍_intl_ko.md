사용자가 더 빠르게 콘솔을 파악하고 사용할 수 있도록 자주 사용하는 서비스를 각 사용자의 니즈에 맞게 분류하여 정리했습니다. 현재 콘솔은 기본 서비스, 시나리오 서비스, 구성 서비스 및 데이터 서비스와 같은 다양한 시나리오에 적합한 모듈로 나뉘어 있습니다.

## 기본 서비스
기본 서비스는 주로 비디오 업로드, 처리, 배포와 같은 VOD 기본 기능을 구현할 수 있는 VOD 기본 서비스에 대한 액세스를 제공합니다. 기본 VOD 서비스만 사용하려면 기본 서비스 모듈 내에서 작업하시기 바랍니다.
<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/2841">서비스 개요</a></td>
<td><ul style = "margin-bottom: 0px;"><li>현재 계정의 과금 방식과 과금 대역폭 및 기타 과금 조건을 조회할 수 있습니다.</li><li>저장 공간, 트랜스코딩 시간, 트래픽 사용량, 대역폭 사용량 및 심사 시간을 확인할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33890">비디오 관리</a></td>
<td><ul style= "margin: 0"><li>비디오, 오디오 및 이미지 업로드, 삭제, 보기, 편집 및 필터링과 같은 작업을 수행할 수 있습니다.</li><li>트랜스코딩, 워터마킹 및 비디오 심사 등 오디오 및 비디오 처리 작업을 진행할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39706">작업 관리</a></td>
<td>VOD 내 작업 진행 상황 및 세부 정보를 볼 수 있습니다.</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14059">태스크 플로우</a></td>
<td><ul style= "margin: 0"><li>오디오 및 비디오 트랜스코딩, 초고속 HD, 어댑티브 비트스트림, 워터마크, 스크린샷, 애니메이션 이미지 및 스마트 식별 등 오디오 및 비디오 처리 템플릿을 설정할 수 있습니다.</li><li>태스크 플로우 템플릿은 오디오 및 비디오를 간소화된 방식으로 처리하도록 설정할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33896#editing-basic-info">비디오 재생</a></td>
<td><ul style= "margin: 0"><li>비디오 가속 재생 링크를 가져올 수 있습니다.</li><li>동영상 링크의 인증 및 액세스 제어를 설정할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7836">플레이어 SDK</a></td>
<td><ul style= "margin: 0"><li>다양한 단말(iOS, Web, Android) 및 플레이어 버전을 지원합니다.</li><li>타사 플레이어가 클라우드 PAAS 리소스에 액세스할 수 있도록 플레이어 Adapter 버전을 제공합니다.</li><li>해상도 자동 전환, 홈 화면 인스턴트 오픈, 제스처 제어 등 다양한 기능을 제공합니다.</li><li>여러 인코딩 방식의 비디오 재생을 지원합니다.</li></ul></td>
</tr>
</table>


## 시나리오 서비스
시나리오 서비스는 미디어 자산 콜드 스토리지, 비디오 스마트 식별, 애플리케이션 관리, License 관리 등 VOD 사용 시나리오에서 파생된 업그레이드 서비스를 제공합니다. 관련 서비스를 사용하려면 이 모듈에서 작업하시기 바랍니다.
<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/42092">미디어 자산 콜드 스토리지</a></td>
<td><ul style = "margin-bottom: 0px;"><li>미디어 리소스의 스토리지 유형 변경이 가능하며, 미디어 자산 콜드 스토리지, 데이터 검색 기능을 제공하여 사용자의 스토리지 비용을 효과적으로 절감합니다.</li><li>스마트 콜드 스토리지 정책을 설정하여 지정된 미디어 리소스의 자동 콜드 스토리지를 구현할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33897">비디오 스마트 식별</a></td>
<td><ul style= "margin: 0"><li>비디오 스마트 식별 작업의 결과를 확인하여 비디오에 부적절한 콘텐츠가 있는지 확인하고 사용자가 친환경적이고 건강한 소셜 네트워크 환경을 구축하도록 지원합니다.</li><li>스마트 식별 결과를 기반으로 비디오에서 새로운 식별 작업을 시작할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/42093">애플리케이션 관리</a></td>
<td><ul style= "margin: 0"><li>서브 애플리케이션을 생성하여 리소스 격리를 구현할 수 있습니다.</li><li>서브 애플리케이션을 편집, 비활성화, 제거 및 활성화할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39429">License 관리</a></td>
<td>UGSV SDK License를 관리할 수 있습니다.</td>
</tr>
</table>


## 구성 서비스
구성 서비스는 도메인 관리, 업로드 스토리지 설정, 콜백 설정, superplayer 구성 등을 포함한 VOD 구성 서비스를 제공합니다. 필요에 따라 이 모듈에서 구성할 수 있습니다.
<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/35572">도메인 관리</a></td>
<td><ul style = "margin-bottom: 0px;"><li>사용자 정의 도메인을 추가하고 도메인에 대해 CNAME을 구성할 수 있습니다.</li><li>기존 도메인에 대한 인증서 관리, 링크 도용 방지 설정 및 해외 CDN 구성 작업을 수행할 수 있습니다.</li><li>기본 배포 도메인을 설정할 수 있습니다.</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/18874">업로드 스토리지 설정</a></td>
<td><ul style= "margin: 0"><li>업로드된 파일을 분류하여 관리할 수 있습니다.</li><li>미디어 자산의 스토리지 리전을 활성화할 수 있으며 업로드된 파일의 기본 스토리지 리전을 설정할 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14055">콜백 설정</a></td>
<td>이벤트 알림 방법, 특정 이벤트 및 알림 수신 주소를 설정할 수 있습니다.</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/38261">superplayer 설정</a></td>
<td>지정된 어댑티브 비트 스트림, 스프라이트 이미지 및 superplayer의 해상도 이름 등을 구성할 수 있습니다.</td>
</tr>
</table>


## 데이터 서비스
데이터 서비스는 사용자에게 전문적인 데이터 통계 및 데이터 분석 서비스를 제공합니다. 트래픽/대역폭, 스토리지, 트랜스코딩 및 비디오 스마트 식별과 같은 사용 통계를 시간 단위로 조회하고, VOD 파일에 대한 액세스 및 재생을 조회할 수 있습니다. 또한 사용자가 데이터 모니터링 및 리소스 관리를 수행하는 데 편리한 로그 다운로드 기능을 제공합니다.
<table>
<tr><th width="17%">기능 명칭</th><th>기능 설명</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/30421">사용량 통계</a></td>
<td>대역폭/트래픽, 스토리지 공간, 트랜스코딩 및 비디오 스마트 식별을 조회할 수 있습니다.</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/30422">데이터 분석</a></td>
<td><ul style= "margin: 0"><li>독립 IP 총 액세스 횟수, 총 요청 횟수 등 액세스 데이터를 볼 수 있습니다.</li><li>파일 재생 상태, TOP100 비디오 재생 횟수 및 기타 재생 상태 데이터를 볼 수 있습니다.</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7983">로그 다운로드</a></td>
<td>도메인 액세스에 대한 자세한 정보를 다운로드할 수 있으며, 시간 단위의 CDN 로그를 제공합니다.</td>
</tr>
</table>



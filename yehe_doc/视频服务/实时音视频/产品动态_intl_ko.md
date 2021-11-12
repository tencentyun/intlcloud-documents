## 2021년 09월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 9.2 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
	<li>음성 설정 기능이 추가되었습니다.</li>
	<li>약한 네트워크 환경에서 지터 방지 알고리즘을 최적화하여 동영상 재생이 더 원활해졌습니다.</li>
</ul><br>Windows: <ul style="margin:0">
	<li>TRTCAudioQualityMusic 고음질 시나리오에 에코 제거 기능이 추가되어 음질과 에코 제거 강도를 자동 균형 조정합니다.</li>
	<li>AGC 알고리즘을 최적화해 소리가 너무 작거나 소리가 너무 큰 문제가 발생할 확률을 낮췄습니다.</li>
</ul><br>Android&iOS:<ul style="margin:0">
	<li>Socks5 프록시를 지원합니다.</li>
	<li>합창 모드의 3A 정책이 최적되었습니다.</li>
</ul><br>Android:<ul style="margin:0">
	<li>하드 디코딩 시 발생하는 ANR 문제가 최적화되었습니다.</li>
	<li>카메라의 로컬 미리보기 각도 호환 문제가 최적화되었습니다.</li>
	<li>첫 프레임의 바로 재생 속도가 최적화되었습니다.</li>
</ul></td>
<td>2021-09-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr><tr>
<td>Version 9.1 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
	<li>C++ 인터페이스에서 오디오 프레임 콜백 형식 설정을 지원합니다.</li>
	<li>약한 네트워크 환경에서의 오디오 및 비디오 경험이 최적화되었습니다.</li>
</ul><br>Windows: <ul style="margin:0">
	<li>ac3 형식 VOD 파일 재생에 대한 지원이 추가되었습니다. </li>
	<li>카메라 정보의 지원되는 해상도 목록 가져오기가 지원됩니다. 자세한 내용은 다음을 참고하십시오. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450">ITXDeviceCollection.getDeviceProperties</a></li>
	<li>Nvidia, Intel, AMD 하드웨어 디코딩을 지원합니다.</li>
</ul><br>Mac: <ul style="margin:0">
로컬 미디어 녹화에 대한 지원이 추가되었습니다.
</ul><br>Android:<ul style="margin:0">
	<li>방 퇴장 시 오디오 상태 관리가 최적화되었습니다.</li>
	<li>오디오 캡처 실행 실패 후 복구 로직을 최적화하여 성공률을 높였습니다.</li>
	<li>특정 조건에서의 영상 화면 과다 노출 문제가 최적화되었습니다.</li>
</ul></td>
<td>2021-09-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table>


## 2021년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 9.0 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>사용자 정의 오디오 트랙의 볼륨 설정을 지원합니다. 자세한 내용은 다음을 참고하십시오. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418">setMixExternalAudioVolume</a></li>
<li>상태 콜백으로 오디오와 비디오의 패킷 손실률을 구분할 수 있습니다. 자세한 내용은 다음을 참고하십시오. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics" >TRTCRemoteStatistics</a></li>
<li>구독 프로세스를 최적화하여 수동 구독의 바로 재생 속도를 개선했습니다.</li>
<li>특정 시나리오에서의 onExitRoom 콜백 중복 문제를 수정했습니다.</li>
</ul><br>iOS:<ul style="margin:0">
시스템 수집 볼륨 설정을 지원합니다. 자세한 내용은 다음을 참고하십시오. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae">setSystemAudioLoopbackVolume</a>
</ul></td>
<td>2021-08-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 07월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.9 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>특정 시나리오에서 소리가 떨리는 문제가 최적화되었습니다.</li>
<li>회사 방화벽 내부 환경 보안 설정에 보다 친화적인 클라우드 프록시 지원이 추가되었습니다.</li>
<li>muteLocalVideo 및 muteRemoteVideoStream 인터페이스에 스트림 유형 매개변수를 추가했습니다.</li>
<li>통계 상태 콜백 onStatistics에 사용자가 WiFi 공유기의 네트워크 품질을 판단하는데 사용되는 로컬 게이트웨이 지연에 대한 통계 gatewayRtt를 새롭게 추가했습니다.</li>
<li>오디오 녹음 인터페이스 startAudioRecording은 더 많은 오디오 형식을 지원합니다.</li>
</ul><br>Android:<ul style="margin:0">
<li>화면 바로 재생 속도가 최적화되었습니다.</li>
<li>오디오 전처리 알고리즘을 업그레이드하여 통화 소리가 더 선명하게 들립니다.</li>
<li>사용자 정의 렌더링의 외부 GLContext 지정을 지원하여 OpenGL 환경을 보다 효율적으로 사용할 수 있습니다.</li>
</ul><br>Windows: <ul style="margin:0">
<li>NVIDIA 플랫폼 하드 코딩을 지원하여 스트리밍 성능을 개선하였습니다.</li>
<li>시스템 오디오 수집(startSystemAudioLoopback)을 위한 스피커 지정을 지원합니다.</li>
</ul></td>
<td>2021-07-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table>


## 2021년 06월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.8 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
mixExternalAudioFrame의 사용 편의성이 최적화되어 더 이상 호출 타이밍을 완벽하게 제어할 필요가 없습니다.
</ul><br>Android&Mac&iOS:<ul style="margin:0">
주변 장치를 통한 오디오 재생을 지원합니다. 다음 API를 참고하십시오. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803" target="_blank">enableCustomAudioRendering</a>
</ul><br>Mac: <ul style="margin:0">
화면 공유 마우스 커서 캡처 활성화 시 CPU 사용량을 줄였습니다.
</ul><br>Windows: <ul style="margin:0">
<li/>AGC 사운드 증대 효과를 최적화하여 보다 빠르고 신속하게 조정됩니다.
<li/>창 필터링 활성화 시 화면 공유의 성능 부하가 최적화되었습니다.
</ul></td>
<td>2021-06-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table>

## 2021년 05월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.7 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>외부 연결 오디오 장치에 대한 예외 점검이 추가되었습니다. onStatistics 콜백 등록 후, <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics">TRTCLocalStatistics</a> 의 audioCaptureState로 장시간 음소거, 파음, 끊김 문제를 실시간으로 점검할 수 있습니다.</li>
<li>BGM 리소스 관리가 최적화되어 메모리 점유율을 적시에 릴리스합니다.</li>
<li>푸시 스트리밍측 백그라운드 전환 후 비디오 업스트림을 일시 중지하면 재생측에서 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a">onUserVideoAvailable(false)</a> 알림을 즉시 수신할 수 있습니다.</li>
</ul><br>Mac: <ul style="margin:0">
화면 공유 시 마우스 커서 캡처의 CPU 및 메모리 점유율이 최적화되었습니다.
</ul><br>Windows: <ul style="margin:0">
사용자 정의 수집의 RGBA 포맷의 비디오 데이터 입력을 지원합니다.
</ul></td>
<td>2021-05-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr><tr>
<td>Version 8.6 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>네트워크 트래픽 제어 알고리즘 최적화로 멀티미디어 전송 품질이 더욱 향상되었습니다.</li>
<li>역할 전환으로 마이크 켜짐/꺼짐 시 원활하게 오디오가 재생되도록 최적화되었습니다.</li>
</ul><br>iOS&Mac&Windows: <ul style="margin:0">
오디오 처리 모듈 최적화로 SPEECH 모드와 DEFAULT 모드의 음성 품질이 향상되었습니다.
</ul><br>iOS&Mac: <ul style="margin:0">
높은 CPU 시나리오에서 사용자 정의 오디오 수집 맞춤성이 최적화되었습니다.
</ul><br>iOS&Android: <ul style="margin:0">
비디오 녹화 시 서브 채널을 통한 공유로 데스크톱 버전 정렬을 지원합니다.
</ul><br>Windows: <ul style="margin:0">
메모리 할당 로직 최적화로 안정성이 향상되었습니다.
</ul><br>Mac: <ul style="margin:0">
Apple M1 아키텍처에 대한 네이티브 지원이 추가되었습니다.
</ul></td>
<td>2021-05-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr></table>



## 2021년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.5 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>VOD 파일 재생 기능이 추가되었습니다. TXVODPlayer와 TRTCCloud를 바인딩하여 현재 재생 중인 VOD 콘텐츠를 TRTC 서브 채널 푸시 스트림을 통해 공유할 수 있습니다.</li>
<li>서브 채널 사용자 정의 수집이 추가되었습니다. API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6">sendCustomVideoData</a>를 참고하십시오.</li>
<li>사용자 정의 믹싱 기능이 추가되었습니다. 사용자의 오디오 트랙을 SDK의 오디오 처리 프로세스에 믹싱할 수 있으며, SDK가 먼저 두 오디오 트랙을 믹싱한 후 다시 배포합니다. 자세한 내용은 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd">mixExternalAudioFrame</a>을 참고하십시오.</li>
<li>지정 퓨어 비디오 혼합 스트림을 지원하여 더 효율적으로 혼합 스트림을 제어합니다.</li>
<li>상태 콜백에 end to end 딜레이가 추가되었습니다.</li>
</ul>
<br>Windows: <ul style="margin:0">
슬라이드 창을 선택해 화면 공유 시 방송 창을 자동으로 전환합니다.
</ul>
<br>Mac: <ul style="margin:0">
<li>화면 공유 기능 최적화로 타깃 창 공유 시 동시에 다른 창을 지정해 함께 공유할 수 있습니다. 자세한 내용은 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>를 참고하십시오.</li>
<li>startSystemAudioLoopback에서 듀얼 사운드 채널을 지원합니다.</li>
</ul>
</td>
<td>2021-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr></table>




## 2021년 02월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.4 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>로컬 멀티미디어 녹화 기능이 추가되었습니다. 호스트가 푸시 스트림 중에 로컬 오디오와 비디오를 mp4 파일로 녹음 및 녹화할 수 있습니다. 자세한 내용은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b">startLocalRecording</a>을 참고하십시오.</li>
<li><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb">Music</a> 모드에서의 오디오 품질을 최적화하여 cloubhouse와 유사한 음성 라이브 방송 시나리오에 더욱 적합합니다.</li>
<li>멀티미디어 링크의 네트워크 저항력을 최적화하여 극단적인 네트워크 검색 상황(70%)에서도 멀티미디어가 비교적 원활하게 재생됩니다.</li>
</ul>
<br>Windows: <ul style="margin:0">
<li>일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소하였습니다.</li>
<li>성능 최적화를 통해 일부 사용 시나리오에서 구버전 대비 성능이 20%- 30% 향상되었습니다.</li>
<li>프로세스 음량 조절 기능이 추가되었습니다. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1">setApplicationPlayVolume</a>을 사용해 시스템 음량 믹서의 음량 크기를 설정할 수 있습니다.</li>
</ul>
<br>Mac: <ul style="margin:0">
<li>Mac 운영 체제의 출력 음성 수집을 지원합니다. Windows와 동일한 SystemLoopback 기능이며, 이 기능을 통해 SDK에서 현재 시스템의 음성을 수집할 수 있습니다. 해당 기능을 활성화하면 호스트가 편리하게 다른 사용자에게 음악 또는 영화 파일을 라이브 방송할 수 있습니다.</li>
<li>화면 공유 시 로컬 미리보기 기능을 지원합니다. 미니 창을 통해 공유할 화면 콘텐츠를 미리 볼 수 있습니다.</li>
</ul>
</td>
<td>2021-02-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr></table>



## 2021년 01월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.3 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">비디오 데이터를 직접 수집하고 TRTC SDK 자체 오디오 모듈을 사용해야 할 경우, 오디오-비디오 동기화가 이루어지지 않는 문제가 발생할 수 있습니다. 이는 SDK 내부 타임라인의 자체 제어 로직으로 인해 발생하는 것으로, 이 문제에 대한 대응책으로 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee">generateCustomPTS</a> 인터페이스가 제공됩니다. 비디오 화면을 수집할 때 이 인터페이스를 사용해서 현재 PTS(타임스탬프)를 기록한 다음 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831">sendCustomVideoData</a>를 호출할 때 이 타임스탬프를 적용하면 오디오-비디오 동기화를 유지할 수 있습니다.</ul>
<br>iOS &amp; Android &amp; Mac: <ul style="margin:0">오디오 모듈이 최적화되었습니다. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a>를 사용해 수집한 오디오 데이터를 SDK에 전송하여 처리할 경우 SDK에서 에코 억제 및 노이즈 감소 효과가 유지됩니다.</ul>
<br>iOS &amp; Android: <ul style="margin:0">TRTC SDK를 기반으로 오디오 특수효과 및 처리 로직을 계속 추가해야 할 경우, 8.3 버전을 사용하면 더욱 간편합니다. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86">setCapturedRawAudioFrameDelegateFormat</a>과 같은 인터페이스를 통해 오디오 데이터의 콜백 포맷(오디오 샘플링 레이트, 오디오 채널 수, 샘플링 포인트 등)을 설정하여 사용자가 선호하는 음성 포맷으로 오디오 데이터를 처리할 수 있습니다.</ul>
<br>Windows: <ul style="margin:0"> 버전 SDK에 도메인 포맷에 대한 Socks5 프록시 지원이 추가되었습니다.</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr></table>


## 2020년 12월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Flutter SDK 배포</td>
<td>이 <a href="https://pub.dev/packages/tencent_trtc_cloud">Flutter SDK</a>는 Tencent Cloud TRTC iOS, Android 플랫폼의 SDK를 기반으로 캡슐화합니다.</td>
<td>2020-12-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39243">Demo(Flutter) 실행</a></td>
</tr><tr>
<td>Version 8.2 버전 배포</td>
<td>
iOS&Android: <ul style="margin:0">로컬 수집과 재생된 모든 오디오 데이터의 혼합 콜백이 추가되어 로컬 오디오 녹음이 더욱 편리해졌습니다.</ul>
<br>Android: <ul style="margin:0">
	<li/>비디오 렌더링 모듈 TXCloudVideoView에서 <code>addVideoView(new TextureView(getApplicationContext()))</code> 인터페이스를 지원하여 TextureView를 로컬 렌더링에 사용합니다.
	<li/>사용자 정의 렌더링 콜백에서 RGBA 포맷의 비디오 데이터를 지원합니다.
	</li>온라인 라이브 방송 인코딩 품질 최적화로 더욱 선명한 비디오 화면을 제공합니다.
</ul>
<br>Mac&iOS: <ul style="margin:0">사용자 정의 렌더링 모드에서도 TRTCCloud.snapshotVideo를 호출하여 비디오 스트림 이미지를 추출할 수 있습니다.</ul>
<br>Windows: <ul style="margin:0">
	<li/>로컬 카메라 수집과 원격 비디오 스트림 캡처 재생을 지원합니다. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c">ITRTCCloud.snapshotVideo</a>를 참고하십시오.
	<li/>화면 공유에서 addExcludedShareWindow와 addIncludedShareWindow 인터페이스를 통해 지정된 창 제외 또는 강제 포함 기능을 지원하여 보다 유연한 화면 공유 기능을 제공합니다.
	<li/>에코 제거 알고리즘 최적화로 에코 제거 효과가 향상되었습니다.
</ul>
</td>
<td>2020-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr><tr>
<td>Version 8.1 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
	<li/>통계 정보(onStatistics)에 원격 비디오 랙과 관련된 통계 지표가 추가되었습니다.
	<li/>음량 조절 인터페이스 setAudioPlayoutVolume(100-150)를 통해 오디오 부스터 효과를 적용할 수 있습니다.
	<li/>이어폰 착용 시 음성 처리 알고리즘 최적화로 오디오 품질이 향상되었습니다.
</ul>
<br>iOS&Android: <ul style="margin:0">setLocalVideoProcessListener 인터페이스가 추가되어 3rd party 뷰티 필터 SDK 통합 지원 기능이 향상되었습니다.
</ul>
<br>Android: <ul style="margin:0">오디오 전처리 알고리즘이 최적화되어 3A 알고리즘이 음질에 미치는 영향이 감소하였습니다.
</ul>
<br>Windows: <ul style="margin:0">
 C#이 최신 버전 API로 업데이트되었습니다.
</ul>
</td>
<td>2020-12-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table> 

## 2020년 11월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>
<td>Version 8.0 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
	<li/>C++ 통합 API가 추가되었습니다. 자세한 내용은 cpp_interface/<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html">ITRTCCloud.h</a>를 참고하십시오.
	<li/>문자열 방 번호를 지원합니다. TRTCParams.strRoomId를 참고하십시오.
	<li/>TXDeviceManager 장치 관리 클래스가 추가되었습니다.
	<li/>API TRTCCloud.switchRoom이 추가되어 수집을 중단하지 않고 직접 방을 전환할 수 있습니다.
	<li/>API TRTCCloud.startRemoteView 원격 비디오 화면 렌더링 시작 기능이 추가되었습니다.
	<li/>API TRTCCloud.stopRemoteView 원격 비디오 화면 렌더링 중지 기능이 추가되었습니다.
	<li/>API TRTCCloud.getDeviceManager 장치 관리 클래스 획득 기능이 추가되었습니다.
	<li/>API TRTCCloud.startLocalAudio 로컬 오디오 수집과 업스트림 활성화 기능이 추가되었습니다.
	<li/>API TRTCCloud.setRemoteRenderParams 원격 이미지의 렌더링 사양 설정이 추가되었습니다.
	<li/>API TRTCCloud.setLocalRenderParams 로컬 이미지의 렌더링 사양 설정이 추가되었습니다.
	<li/>수동 수신 모드에서 역할 전환 시 바로 재생 효과가 최적화되었습니다.
	<li/>오디오 수신 로직을 최적화하여 오디오 효과가 향상되었습니다.
	<li/>sendCustomCmdMsg 신뢰성이 최적화되었습니다.
</ul>
<br>Android: <ul style="margin:0">
	소프트웨어/하드웨어 디코딩 전환 로직이 최적화되었습니다.
</ul>
<br>Windows: <ul style="margin:0">
	<li/>System loopback 오디오 음질 수집 및 에코 제거 효과가 최적화되었습니다.
	<li/>오디오 디바이스 선택 로직을 최적화하여 Silent rate가 감소하였습니다.
	<li/>동시 음성 제거 효과가 최적화되었습니다.
</ul>
</td>  
<td>2020-11-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr><tr>
<td>과금 변경</td>
<td>MCU 클러스터를 사용해 클라우드 혼합 스트림 트랜스 코딩을 진행하는 서비스가 정식으로 상용화되어 요금이 부과됩니다.
</td>
<td>2020-11-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">클라우드 혼합 스트림 트랜스 코딩 과금 설명</a></td>
</tr>
</table> 

## 2020년 10월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>
<td>Version 7.9 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
	<li/>사용자 정의 암호화를 지원해 인코딩된 멀티미디어 데이터를 노출된 C 인터페이스를 통해 2차 처리할 수 있습니다.
	<li/>TRTCRemoteStatistics에 오디오 랙 정보 콜백 audioTotalBlockTime과 audioBlockRate가 추가되었습니다.
	<li/>수동 구독 모드에서 시청자와 호스트 역할 전환 시의 오디오 유연성이 최적화되었습니다.
	<li/>멀티미디어 통화에서 약한 네트워크에 대한 저항력 최적화로 네트워크 환경이 좋지 않은 상황에서의 오디오 유연성이 향상되었습니다.
</ul>
<br>Android: <ul style="margin:0">
	<li/>Android 대부분 모델의 인이어 모니터링 효과를 최적화하여 인이어 모니터링 딜레이가 적정 수준까지 감소됩니다.
	<li/>Music 모드(startLocalAudio인 경우 지정)에서의 P2P 딜레이가 최적화되었습니다.
</ul>
<br>iOS: <ul style="margin:0">
오디오 모듈의 실행 속도를 최적화하여 첫 번째 오디오 프레임을 더 빨리 수집해 전송할 수 있습니다.
</ul>
<br>Mac: <ul style="margin:0">
화면 공유에 선택 창 필터링 기능을 지원합니다. 공유하지 않는 창을 제거하여 보다 개선된 사생활 보호를 제공합니다.
</ul>
<br>Windows: <ul style="margin:0">
	<li/>화면 공유의 ‘공유 중’ 알림창 프레임 색상과 프레임 크기 설정 기능을 지원합니다.
	<li/>화면 공유 기능으로 전체 화면을 공유할 때 고성능 모드를 지원합니다.
	<li/>시스템 루프의 에코 제거 알고리즘을 최적화하여 시스템 루프백(SystemLoopback) 활성화 시 에코 제거 능력이 강화되었습니다.
	<li/>화면 공유 기능의 창 수집 차폐 방지 기능이 최적화되어 창 필터 설정 기능을 지원합니다.
</ul>
</td>
<td>2020-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table> 

## 2020년 09월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<td>Version 7.8 버전 배포</td>
<td>
Android: <ul style="margin:0">
<li>조정화면 푸시스트림을 지원합니다. 사용 방법은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d">TRTCCloud.setVideoMuteImage</a>를 참고하십시오.
<li>오디오 라우팅 정책 최적화되어 이어폰 착용 시 오디오가 이어폰에서만 재생됩니다.
<li>일부 시스템에서 저딜레이 수집 재생을 지원하여 Android 시스템의 통화 딜레이가 감소하였습니다.
<li>VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
</ul>
<br>iOS: <ul style="margin:0">
VODPlayer와 trtc 동시 사용 및 에코 제거를 지원합니다.
</ul>
<br>iOS&Mac: <ul style="margin:0">
조정화면 푸시스트림을 지원합니다. 사용 방법은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2">TRTCCloud.setVideoMuteImage</a>를 참고하십시오.
</ul>
<br>Mac: <ul style="margin:0">
<li>Mac: 시스템 음량 변화 콜백이 추가되었습니다. 자세한 내용은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338">TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged</a>를 참고하십시오.
</ul>
<br>Windows: <ul style="margin:0">
<li>스크린 간 영역을 지정하여 화면을 공유하는 기능이 추가되었습니다.
<li>창 공유에 지정 창 필터링 차단 기능을 추가하였습니다. 자세한 내용은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff">TRTCCloud.addExcludedShareWindow</a> 및 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf">TRTCCloud.removeExcludedShareWindow</a>를 참고하십시오.
<li>시스템 음량 변화 콜백이 추가되었습니다. 자세한 내용은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12">ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged</a>를 참고하십시오.
<li>가상 카메라 e2eSoft Vacm과 호환됩니다.
<li>startLocalPreview와 startCameraDeviceTest 동시 호출을 지원합니다.
<li>화면을 메인 채널로 공유하고, startLocalPreview 호출 시 로컬 미리보기를 활성화합니다.
<li> SDK 내부 재생 버퍼로 인한 오디오 딜레이가 커지는 문제가 감소하였습니다.
<li>오디오 실행 로직이 최적화되어 재생 상황에 한정해 마이크를 점유하지 않습니다.
</ul>
</td>
<td>2020-09-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
<tr></tr> 
<tr>
<td>Version 7.7 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
서브 채널(화면 공유)의 바로 재생 속도가 최적화되었습니다.
</ul>
<br>iOS: <ul style="margin:0">
내부 스레드 모델 최적화로 30개 이상의 채널에서 동시 재생하는 시나리오에서의 실행 안정성이 향상되었습니다.
</ul>
<br>iOS&Android: <ul style="margin:0">
<li>Audio 모듈 기능 최적화로 첫 번째 프리엠의 수집 딜레이가 향상되어 최신 버전에서는 첫 번째 오디오 프레임을 더 빨리 획득할 수 있습니다.
<li>VodPlayer와 TRTC를 동시에 사용할 경우의 음량 크기 및 음질이 최적화되었습니다.
<li>wav 오디오 포맷의 배경 음악과 효과음 지원 파일이 추가되었습니다.
</ul>
<br>Windows: <ul style="margin:0">
<li>일부 저가형 카메라의 CPU 사용률이 지나치게 높은 문제가 최적화되었습니다.
<li>멀티 USB 카메라와 마이크에 대한 호환성 최적화로 디바이스의 실행 성공률이 향상되었습니다.
<li>카메라와 마이크 기기 선택 정책을 최적화하여 카메라 또는 마이크 사용 중 소켓으로 인해 수집 오류가 발생하는 문제가 방지됩니다.
</ul>
</td>
<td>2020-09-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>
</table>


## 2020년 08월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>
<td>Version 7.6 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
<li>enterRoom의 프로토콜 정책 최적화로 방 입장 속도와 성공률이 향상되었습니다.
<li>다수의 오디오를 구독할 경우에 발생하는 전반적 성능 소모와 랙 문제가 최적화되었습니다.
</ul>
<br>Android: <ul style="margin:0">
<li>TRTCCloudListener에 onCapturedRawAudioFrame 콜백이 추가되었으며, 기타 몇 가지 콜백 함수 이름을 변경했습니다. 순서대로 onLocalProcessedAudioFrame, onRemoteUserAudioFrame, onMixedPlayAudioFrame로 변경되었습니다.
</ul>
<br>iOS: <ul style="margin:0">
<li>View 렌더링 영역 실시간 조정을 더 쉽게 조작할 수 있는 updateLocalView와 updateRemoteView 인터페이스가 추가되었습니다.
<li>TRTCCloudDelegate에 onCapturedRawAudioFrame 콜백이 추가되었으며, 기타 몇 가지 콜백 함수 이름을 변경했습니다. 순서대로 onLocalProcessedAudioFrame, onRemoteUserAudioFrame, onMixedPlayAudioFrame로 변경되었습니다.
</ul>
<br>Windows: <ul style="margin:0">
<li>HWND 유형의 렌더링 창을 보다 쉽게 실시간으로 조정할 수 있는 updateLocalView와 updateRemoteView 인터페이스가 추가되었습니다.
<li>현재 Windows PC가 음소거로 설정되어 있는지를 확인하는 데 사용할 수 있는 getCurrentMicDeviceMute 인터페이스가 추가되었습니다.
<li>현재 Windows PC를 음소거로 설정할 수 있는 setCurrentMicDeviceMute 인터페이스가 추가되었습니다.
</ul>
<br>Mac: <ul style="margin:0">
<li>View 렌더링 영역 실시간 조정을 더 쉽게 조작할 수 있는 updateLocalView와 updateRemoteView 인터페이스가 추가되었습니다.
<li>현재 Mac이 음소거로 설정되어 있는지 확인하는 데 사용할 수 있는 getCurrentMicDeviceMute 인터페이스가 추가되었습니다.
<li>현재 Mac을 음소거로 설정할 수 있는 setCurrentMicDeviceMute 인터페이스가 추가되었습니다.
<li>화면 공유에 지정 창의 지정한 영역 공유 기능을 지원합니다.
</ul>
</td>
<td>2020-08-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr>

</table>

## 2020년 07월

<table>
<tr><th width="20%">업데이트 명칭</th><th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th></tr>
<tr>
<td>Version 7.5 버전 배포</td>
<td>전체 플랫폼: <ul style="margin:0">
<li>더블 스택 IPV6와 IPV6 only에 대한 지원이 추가되었습니다.</li>
<li>소그룹 수업 지원에 사용되는 다수 방 입장 시 풀 스트림 기능이 추가되었습니다.</li>
<li>클라우드 MCU 혼합 스트림에 배경 이미지(모니터링이 필요하므로 이미지는 TRTC 콘솔에 먼저 업로드해야 함) 설정 기능이 추가되었습니다.</li>
<li>클라우드 MCU 혼합 스트림에 A+B=>C와 A+B=>A 모드가 추가로 지원됩니다.</li>
<li>실시간 상태 콜백 onStatistics에 재생 버퍼 시간 필드 jitterBufferDelay가 추가되었습니다.</li>
<li>클라이언트 간 마이크 연결 딜레이가 감소하였습니다. 7.5 버전 클라이언트 간 통화 및 마이크 연결 딜레이가 7.4 버전 기준 40% 감소하였습니다.</li>
<li>모바일 디바이스의 인이어 모니터링 딜레이가 감소하였으며, 인이어 모니터링에 음성 변조 및 잔향 등과 같은 음향 효과 설정이 지원됩니다.</li>
<li>클라이언트 네트워크 지터 평가 알고리즘이 최적화되어 재생 딜레이가 감소하였습니다.</li>
</ul>
<br>Android: <ul style="margin:0">
<li>Android SDK의 end-to-end 마이크 연결 통화 딜레이가 감소하였습니다.</li>
<li>인이어 모니터링 딜레이 문제가 한층 더 최적화되었습니다.</li>
<li>재생 view 동적 전환 시 블랙 스크린이 발생하는 문제가 최적화되었습니다.</li>
</ul>
<br>iOS: <ul style="margin:0">
<li>인이어 모니터링 딜레이 문제가 한층 더 최적화되었습니다.</li>
<li>마이크 실행 성공률이 최적화되었습니다.</li>
</ul>
<br>Windows: <ul style="margin:0">
<li>socks5 프록시에서 사용자 이름과 비밀번호 인증을 지원합니다.</li>
<li>세로 화면 해상도 푸시 스트림 시 일부 카메라에서 프레임 레이트가 매우 낮아지는 문제가 최적화되었습니다.</li>
</ul></td>
<td>2020-07-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr><tr>
<td>CAM 리소스 레벨의 권한 부여 지원</td>
<td>TRTC에서 CAM 리소스 레벨의 권한 부여를 지원합니다. 개발자가 필요에 따라 서브 계정에 적합한 TRTC 액세스 권한을 할당할 수 있습니다.</td>
<td>2020-07-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38319">CAM</a></td>
</tr><tr>
<td>패키지에서 잔여량 알람 설정 지원</td>
<td>콘솔에 패키지 잔여량 알람 스위치가 추가되었습니다. 활성화 시 패키지 잔여량을 알람 값까지 소모하면 SMS, 내부 메시지, 이메일을 통해 알려줍니다.</td>
<td>2020-07-20</td>
<td><a href="https://console.cloud.tencent.com/trtc/package">콘솔 패키지 관리</a></td>
</tr><tr>
<td>과금 변경</td>
<td>클라우드 녹화에 <b>녹화 시간</b>에 따른 과금이 추가되었습니다.</td>
<td>2020-07-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">클라우드 녹화 과금 설명</a></td>
</tr>
</table>

## 2020년 06월

<table>
<tr><th width="20%">업데이트 명칭</th><th width="50%">업데이트 설명</th><th width="15%">배포일</th><th width="15%">관련 문서</th></tr>
<tr>
<td>Version 7.4 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
  <li>각 플랫폼 버전의 SPEECH 음질 모드에서 음성 통화 딜레이 비율의 예상 편차가 큰 문제가 최적화되었습니다.</li>
  <li>방 입장 프로세스 정책 최적화로 전체 플랫폼의 방 입장 성공률이 향상되었습니다.</li>
  <li>인이어 모니터링에서 음량 설정을 지원합니다.</li></ul>
<br>iOS: <ul style="margin:0">
  iOS 버전에서 AirPlay 미러링(구버전은 통화 음량을 사용해 미러링 불가)을 지원합니다. 
</ul>
<br>Windows: <ul style="margin:0">
  <li>Windows 플랫폼의 반향 제거(AEC) 효과 최적화로 시스템 오디오 루프백(startSystemAudioLoopback) 활성화 후 나타나는 에코 문제를 방지합니다. </li>
  <li>Windows 플랫폼의 카메라 수집 디바이스 호환성이 향상되었습니다.</li>
  <li>Windows 플랫폼의 오디오 디바이스(마이크 및 스피커) 호환성이 향상되었습니다.</li>
</ul>
</td>
<td>2020-06-24</td>
<td>-</td>
</tr>
<tr>
<td>Version 7.3 버전 배포</td>
<td>
전체 플랫폼: <ul style="margin:0">
  <li>모든 링크에서 128의 고음질 입체 음향을 지원합니다. setAudioQuality(TRTCAudioQualityMusic) 인터페이스를 통해 설정할 수 있습니다.</li>
  <li>SPEECH 음성 모드를 지원합니다. 회의 시나리오의 음성 통화에 적합합니다. 더 강력한 노이즈 감소(ANS) 효과를 원하는 경우 setAudioQuality(TRTCAudioQualitySpeech)에서 설정할 수 있습니다.</li>
  <li>다중 배경 음악 동시 재생 기능이 지원됩니다. 메인 보컬과 코러스가 분리된 노래방 시나리오 지원에 사용됩니다. 배경 음악 순환 재생도 함께 지원됩니다.</li>
  <li>기존 인터페이스가 호환되는 상황에서 신규 음향 효과 관리 인터페이스 TXAudioEffectManager가 추가되었습니다. 해당 기능은 더욱 빠르고 다양한 음향 효과 기능을 지원합니다.</li>
  <li>비디오 인코딩 매개변수 setVideoEncoderParam에 minVideoBitrate 옵션이 추가되었습니다. 화질 요구사항이 높은 라이브 방송 클라이언트에게 추천합니다.</li>
  <li>muteLocalVideo를 호출한 후 startLocalPreview를 호출하면 ‘미리보기만 하고 푸시 스트림은 하지 않는’ 효과를 지원합니다. enterRoom 전 startLocalPreview를 호출해 해당 기능을 실행할 수 있습니다.</li>
   </ul>
<br>iOS: <ul style="margin:0"> 
     <li> iOS 시스템 레벨의 녹화 방법이 추가되어 VooV Meeting와 유사한 전체 시스템 화면 공유 효과를 구현할 수 있습니다. 또한 액세스 용이성을 최적화하여 반일 내에 해당 기능의 인터페이스에 액세스할 수 있습니다.</li>
  <li> 인이어 모니터링에서 중복 잔향 등의 음향 효과를 지원합니다.</li>
   </ul>
<br>Android&Windows: <ul style="margin:0">      
  오디오에 순간 노이즈 감소 기능이 지원됩니다. setAudioQuality(TRTCAudioQualitySpeech)를 통해 활성화할 수 있습니다. 
</ul>
<br>Android: <ul style="margin:0">      
  asset 패키지 음향 효과 파일을 지원합니다.
</ul>
<br>Windows: <ul style="margin:0">  
   음성 변조 등 음향 효과 기능이 추가되었습니다.
</ul>
</td>
<td>2020-06-01</td>
<td>-</td>
</tr></table>


## 2020년 05월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>과금 변경</td>   
         <td>음성 시간이 모든 사용자가 방 안에 머무르는 총시간으로 변경되고, 여기서 모든 사용자가 비디오 스트림을 구독할 때 머무르는 시간을 제합니다.<br>보충 설명: <ul style="margin:0;"><li>여러 채널의 오디오 스트림을 동시에 구독하는 동일한 사용자의 음성 시간은 중복되지 않습니다.</li>
<li>비디오 스트림 미구독 시 오디오 스트림 구독 여부에 상관없이 음성 시간으로 계산됩니다.</li>
     <li>비디오 시간 계산 규정은 변경되지 않습니다(모든 사용자가 구독하는 비디오 스트림의 총시간).</li>
</ul></td>   
       <td>2020-05-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">과금 개요</a></td>   
     </tr> 
</table>

## 2020년 04월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr><td>통화 품질 모니터링 관련 인터페이스 배포</td>   
    <td><ul style="margin:0;"><li>SDKAppID의 방 리스트 조회 인터페이스가 추가되었습니다. 한 번에 최대 100개의 방 정보가 반환되며, 최근 5일 이내의 데이터를 조회할 수 있습니다.</li>
     <li>사용자 리스트 및 통화 지표 조회 인터페이스가 추가되어 지정 시간 내의 사용자 리스트 및 통화 품질 데이터를 조회할 수 있습니다.</li>
     <li>이전 방 및 사용자 수 조회 인터페이스가 추가되어 지정 시간 내의 이전 방 및 사용자 수를 조회할 수 있습니다.</li>
     <li>실시간 통화 규모 조회 인터페이스가 추가되어 24시간 이내의 방 수 및 통화 인원수를 조회할 수 있습니다.</li>
     <li>실시간 품질 조회 인터페이스가 추가되어 24시간 이내의 방 입장 성공률, 첫 프레임 바로 재생률, 멀티미디어 랙 발생률 데이터를 조회할 수 있습니다.</li>
     <li>실시간 네트워크 상태 조회 인터페이스가 추가되어 업/다운스트림 패킷 손실 데이터를 포함한 24시간 이내의 네트워크 상태를 조회할 수 있습니다.</li>
</ul></td>   
    <td>2020-04-29</td>   
		<td><a href="https://intl.cloud.tencent.com/document/product/647/34260">API 개요</a></td> 
</tr><tr>
    <td>SDK Version 7.2 버전 배포</td>   
  <td><br>Android: <ul style="margin:0;">
     <li>Android에 핸드폰 녹화 기능이 추가되었습니다. 해당 기능은 핸드폰에서의 라이브 방송 녹화에 적용됩니다.</li>
     <li>통화 시나리오에서 중저가 Android 핸드폰의 성능 소모를 최적화하여 통화 품질이 향상되었습니다.</li>
  </ul><br>iOS: <ul style="margin:0;">
      <li>App 내 녹화 기능이 추가되었습니다. 해당 기능은 App에서의 라이브 방송 녹화에 적용됩니다.</li>
      <li>iOS 저가형 기기 통화 음질 최적화로 음성 효과가 향상되었습니다.</li>
  </ul><br>iOS&Android: <ul style="margin:0;">필터, 그린 스크린과 같은 시각 효과 인터페이스가 최적화되었습니다.
  </ul><br>Windows: <ul style="margin:0;">Windows의 getCurrentCameraDevice 로직을 최적화하여 카메라 미사용 시 첫 번째 디바이스를 기본 디바이스로 반환합니다.
  </ul></td>   
  <td>2020-04-16</td>   
  <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
</tr><tr>      
  <td>콘솔 사용량 통계 모듈 개편</td>   
  <td>사용량 통계 모듈을 개편하여 음성, 표준 화질, 고화질, 초고화질의 실시간 과금 시간(분)을 지원하며 데이터는 5분마다 업데이트됩니다.</td>   
  <td>2020-04-01</td>   
  <td>-</td>   
</tr> 
</table>

## 2020년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 7.1 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>혼합 스트림 사전 설정 템플릿 활용성이 최적화되었습니다.</li>
     <li>방 입장 시 자동으로 릴레이하는 문제가 수정되었습니다.</li>
     <li>혼합 스트림이 최적화되어 성공률이 향상되었습니다.</li>
</ul><br>Android: <ul style="margin:0;">
		 <li>방에 입장한 이후 AGC를 반복해서 활성/비활성화할 경우 처리한 오디오가 전부 0이 되는 문제가 수정되었습니다.</li>
     <li>C++ STL 기본 라이브러리 완전 정적 컴파일을 지원합니다.</li>
     <li>통화 음량이 기본적으로 ANS, AGC를 활성화하여 통화 모드에서의 음질이 향상되었습니다.</li>
</ul><br>iOS: <ul style="margin:0;"><li>방 입장 전 startLocalPreview한 후 방 입장 시 미리보기가 검은색으로 표시되는 문제가 수정되었습니다.</li>
     <li>iOS 13.3 시스템 일부 모델의 심각한 에코 문제가 수정되었습니다.</li>
     <li>BGM 재생에서 확장자가 수반되지 않은 오디오 파일을 지원합니다.</li>
</ul><br>Mac&Windows: <ul style="margin:0;">
     <li>화면 공유 시 메인 채널에서의 푸시 스트림을 지원합니다.</li>
</ul></td>   
       <td>2020-03-27</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>'멀티미디어 범용 패키지' 런칭</td>   
         <td>멀티미디어 범용 패키지가 런칭되었습니다. 고정 패키지와 사용자 정의 패키지가 포함되어 있으며, 동시에 음성, 표준 화질, 고화질, 초고화질의 시간이 차감됩니다. 범용 패키지 시간에서 1분당 음성 1분, 표준 화질 2분, 고화질 4분, 초고화질 15분이 차감됩니다.</td>   
       <td>2020-03-11</td>   
       <td>-</td>   
     </tr> 
</table>

## 2020년 02월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>클라우드 자동 녹화 최적화</td>   
         <td>애플리케이션 단독 설정에 따라 클라우드 자동 녹화 활성화/비활성화를 지원하며, 각 애플리케이션별로 단독 녹화 파일 포맷 및 콜백 주소를 설정할 수 있습니다.</td>   
       <td>2020-02-14</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35426">클라우드 녹화 및 재생 구현</a></td>   
     </tr> 
</table>

## 2020년 01월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 6.9 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>enterRoom 매개변수 TRTCParams에 streamId 속성이 추가되었습니다. 현재 사용자의 CDN 라이브 방송 스트림 ID 설정에 사용해 라이브 방송 CDN 바인딩이 더욱 편리해집니다.</li>
     <li>enterRoom 매개변수 TRTCParams에 cloudRecordFileName 속성이 추가되어 해당 라이브 방송 클라우드 녹화 파일명을 설정할 수 있습니다. 또한 비디오 스트림 중단에 대한 녹화 서비스의 저항력을 최적화하여 원격 녹화 파일의 완전성을 확보합니다.</li>
     <li>시나리오 TRTCAppSceneAudioCall이 추가되어 enterRoom 시 설정할 수 있습니다. 해당 시나리오에서 음성 통화와 관련된 TRTC SDK가 전반적으로 최적화되었습니다.</li>
     <li>시나리오 TRTCAppSceneVoiceChatRoom이 추가되었습니다. enterRoom 시 설정할 수 있으며, TRTC SDK를 활성화하여 음성 인터랙션 채팅방 시나리오를 최적화할 수 있습니다.</li>
     <li>비디오 화면이 1080P 고해상도 수집을 지원하여 핸드폰 라이브 방송을 PC로 시청하는 시나리오에서의 화면 해상도가 향상되었습니다.</li>
     <li>API: pauseAudioEffect, resumeAudioEffect 음향 효과가 추가되어 일시 중지/복구 제어 기능을 지원합니다.</li>
     <li>API: setBGMPlayoutVolume, setBGMPublishVolume, BGM이 추가되어 로컬 재생과 푸시 스트림 오디오 믹싱을 지원합니다.</li>
     <li>API: setRemoteSubStreamViewRotation 서브 채널 비디오 재생이 추가되어 렌더링 회전 각도 조정을 지원합니다.</li>
</ul><br>iOS&Android: <ul style="margin:0;"> API: snapshotVideo()가 추가되어 로컬 및 원격 비디오의 화면을 캡처할 수 있습니다.
</ul><br>Android: <ul style="margin:0;"><li>일종의 전역 음량 유형 모드인 setSystemVolumeType(TRTCSystemVolumeTypeVOIP)이 추가되어 통화 음량을 항상 사용합니다. 블루투스 이어폰의 자체 마이크에서 발생하는 수집 전환 문제 해결에 사용됩니다.</li>
     <li>Android 10.0 시스템에 대한 지원이 추가되었습니다.</li>
</ul><br>Windows: <ul style="margin:0;"><li>C# 버전 SDK에서 리얼 윈도우 렌더링 및 사용자 정의 렌더링을 지원합니다.</li>
     <li>C# 버전 SDK에서 로컬 오디오 녹화 정렬 기능을 지원합니다.</li>
</ul></td>   
       <td>2020-01-14</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>'통화 품질 모니터링 대시보드 v2.0' 배포</td>   
         <td><ul style="margin:0;"><li>클라이언트 SDK에서 보고 데이터를 3초 이내에 조회할 수 있습니다.</li>
     <li>데이터를 15일간 저장하여 개발자가 언제든 조회할 수 있습니다.</li>
     <li>Web 프런트 엔드에서 10초 이내에 6명의 5시간 데이터를 모두 렌더링할 수 있습니다.</li>
     <li>수신 측/발송 측의 다각적인 데이터 상세 정보 및 상세 이벤트 태그를 제공합니다.</li>
     <li>단일 페이지에 전체 링크 정보를 표시하고 데이터 동기화를 비교합니다.</li>
     <li>Tencent가 자체개발한 품질 평가 체계로 실제 응용 시나리오에 적합합니다.</li>
     <li>사용 경험에 초점을 맞춰 데이터를 쉽게 이해할 수 있고 세부적이며 활용성이 높습니다.</li>
</ul></td>   
       <td>2020-01-07</td>   
       <td>-</td>   
     </tr> 
</table>

## 2019년 12월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr>
<tr>      
<td>CAM 서비스 레벨의 권한 부여 지원</td>   
<td>TRTC에서 CAM에 액세스할 수 있으며, 서비스 레벨의 권한 부여를 지원합니다.</td>   
<td>2019-12-31</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM을 지원하는 제품</a></td> 
</tr>
<tr>      
<td>과금 변경</td>   
<td>표준 화질 SD의 최대 해상도가 640×360에서 640×480으로 상향되었습니다. 즉, 640×480 이하의 해상도는 모두 표준 화질에 따라 과금됩니다.</td>   
<td>2019-12-04</td>   
<td>-</td>   
</tr>
</table>



## 2019년 11월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>콘솔 v2.0 배포</td>   
         <td>프레임워크 재설계로 왼쪽 메뉴가 추가되어 활용성이 향상되었습니다. 기능별로 개요, 사용량 통계, 모니터링 대시보드, 개발 지원, 패키지 관리, 애플리케이션 관리 등의 모듈로 구분됩니다.</td>   
       <td>2019-11-18</td>   
       <td>-</td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.8 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>방 입장 시 수동 풀 스트림을 지정할 수 있는 기능이 추가되었습니다.</li>
     <li>onRemoteUserEnterRoom / onRemoteUserLeaveRoom 콜백이 추가되었습니다. 마이크를 켜지 않은 호스트의 방 입장/퇴장 공지를 지원합니다.</li>
     <li>pts 생성 메커니즘이 최적화되었습니다.</li>
     <li>네트워크 전환 후 자동으로 더 원활한 액세스 포인트를 선택하도록 최적화되었습니다.</li>
     <li>startRemoteView에서 사전 호출을 지원합니다.</li>
</ul><br>Android: <ul style="margin:0;">인이어 모니터링 기능이 추가되었습니다.</ul>
<br>iOS&Android: <ul style="margin:0;">
		<li>엔터프라이즈 버전에 피부 미백, 눈 미백, 치아 미백, 주름 개선, 눈밑 지방 제거 등과 같은 신규 포토샵 기능이 추가되었습니다.</li>
		<li>뷰티 필터와 포토샵 동적 효과 인터페이스가 통합된 getBeautyManager 인터페이스가 추가되었습니다.</li>
</ul>
<br>Mac: <ul style="margin:0;">Mac10.15 호환성 문제가 수정되었습니다.
</ul>
<br>Windows: <ul style="margin:0;"><li>녹화 시 차단 방지를 지원합니다.</li>
     <li>socks5 프록시를 지원합니다.</li>
     <li>Windows C#에서 특정 사용자의 렌더링 콜백 제거 후 기타 사용자도 데이터를 수신할 수 없는 문제가 수정되었습니다.</li>
     <li>Windows C# 성능이 최적화되었습니다.</li>
</ul>
</td>   
<td>2019-11-15</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
</tr> 
</table>

## 2019년 10월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
    <td>과금 변경 및 베타 패키지 한도 확대</td>   
    <td><ul style="margin:0;">
            <li>음성과 비디오를 분리하여 과금합니다. 비디오는 표준 화질 SD, 고화질 HD, 초고화질 FHD로 분류하여 과금됩니다. 정가: 음성 7위안/1,000분, 표준 화질 14위안/1,000분, 고화질 28위안/1,000분, 초고화질 105위안/1,000분</li>
           <li>고정 패키지와 사용자 정의 패키지가 포함된 새로운 음성, 표준 화질, 고화질 패키지가 동시에 런칭되었으며, 패키지 유효 기간은 모두 1년입니다.</li>
           <li>2019년 10월 11일부터 TRTC 콘솔에서 처음으로 애플리케이션을 생성하는 사용자는 기본 제공되는 베타 패키지 멀티미디어 시간이 1,000분에서 10,000분으로 늘어납니다. 유효 기간은 1년이며 순서대로 음성, 표준 화질, 고화질, 초고화질 시간이 차감됩니다.</li>
           <li>TRTC 콘솔에서 처음으로 애플리케이션을 생성한 시간이 2019년 10월 11일 이전이거나 음성과 비디오를 구분하지 않는 이전 패키지를 구매한 사용자는 지속적으로 '음성과 비디오 동일 과금' 방식이 적용됩니다. 이전 패키지(1,000분 베타 패키지, 6.6위안에 300분 체험 패키지, 5만분 입문 패키지, 25만분 표준 패키지, 100만분 엔터프라이즈 패키지, 300만분 프리미엄 패키지 포함) 사용을 완료하였거나 만료된 후 익월에 신규 패키지(음성, 표준 화질, 고화질의 고정 패키지 및 사용자 정의 패키지 포함)를 구매할 수 있으며, 신규 패키지를 구매한 후에는 '음성과 비디오 분리 과금' 방식으로 전환됩니다. 과금 방식 변경 작업은 철회가 불가능합니다.</li>
</ul></td>   
       <td>2019-10-11</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">과금 개요</a></td>   
     </tr> 
</table>

## 2019년 09월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 6.7 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>푸시 소모 시간이 최적화되었습니다.</li>
     <li>사용자가 재생 음량을 독립적으로 조절할 수 있는 기능을 지원합니다.</li>
</ul><br>Android: <ul style="margin:0;"><li>AAR 패키지에 권한 획득 설정이 추가되었습니다.</li>
     <li>Android 8.0 이상 시스템의 CPU 점유율 평가가 추가되었습니다.</li>
     </ul><br>iOS: <ul style="margin:0;">인이어 모니터링 기능이 추가되었습니다.</ul><br>
     Windows: <ul style="margin:0;"><li>음향 효과 인터페이스가 추가되었습니다.</li>
     <li>64비트 C# API 지원이 추가되었습니다.</li>
</ul><br>Mac: <ul style="margin:0;">방 입장 및 출력 프레임 속도가 최적화되었습니다.</ul></td>   
       <td>2019-09-30</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.6 버전 최적화</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>시스템 음량 유형 설정 인터페이스가 추가되었습니다.</li>
     <li>음향 효과 인터페이스가 추가되었습니다. 짧은 음향 효과 재생을 지원합니다.</li></ul><br>
     iOS: <ul style="margin:0;">iOS 13 호환을 지원합니다.</ul><br>
     Mac: <ul style="margin:0;">일부 모델에서의 잡음, 소리 변형 같은 호환성 문제가 해결되었습니다.</ul><br>
     iOS&Android: <ul style="margin:0;">사용자 정의 오디오 콜백 데이터 수정을 지원합니다.</ul><br>
     Windows&Mac: <ul style="margin:0;">AGC 지원이 추가되어 일부 모델에서의 소리가 작은 문제가 해결되었습니다.</ul></td>   
       <td>2019-09-10</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
</table>

## 2019년 08월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>콘솔에 '신규 사용자 가이드' 런칭</td>   
         <td>신규 사용자 가이드가 추가되어 4단계만으로 TRTC Demo의 빠른 실행이 가능합니다.</td>   
       <td>2019-08-16</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35083">1분 만에 Demo 실행하기</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.6 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>방 입장이 최적화되어 입장 소모 시간이 단축되고 입장 성공률이 향상되었습니다.</li>
     <li>오디오 로컬 녹화 기능이 추가되었습니다.</li>
     <li>원격 비디오 인터페이스 mute 기능을 지원합니다.</li>
     <li>첫 프레임 오디오 및 비디오 전송 콜백 인터페이스가 추가되었습니다.</li>
     <li>방 입장 에러 코드가 통합되었습니다. onEnterRoom을 통해 콜백되며, result가 0보다 작은 경우 방 입장 오류를 표시합니다.</li>
     <li>Demo 최적화 및 저딜레이 대형 방이 추가되었습니다.</li>
</ul><br>Android: <ul style="margin:0;"><li>로컬 미리보기 각도가 맞지 않는 문제가 수정되었습니다.</li>
     <li>로컬 및 원격 렌더링에서 SurfaceView 방식을 지원합니다.</li>
</ul><br>Windows: <ul style="margin:0;">에코 제거 라이브러리 업그레이드로 시스템 믹싱을 구현하여 일부 수집에 ANS 설정 시 적용되지 않고 일부 기기에서 음량이 작은 문제가 해결되었습니다.</ul>
<br>iOS&Android: <ul style="margin:0;"><li>플레이어에 음량 설정 인터페이스와 음량 크기 콜백 인터페이스가 추가되었습니다.</li>
     <li>사용자 정의 전송 비디오가 로컬 렌더링을 지원합니다.</li>
     <li>사용자 정의 수집 및 전송 비디오는 1080P를 지원합니다.</li>
</ul></td>   
       <td>2019-08-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
</table>

## 2019년 06월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
     <td>SDK Version 6.5 버전 배포</td>   
     <td>전체 플랫폼: <ul style="margin:0;">
        <li>라이브 방송 모드(TRTCAppSceneLIVE)에 ‘저딜레이 대형 방’ 기능이 추가되었습니다. 
            <ul style="margin:0;"><li>멀티미디어 최적화를 위한 UDP 프로토콜을 적용함으로써 약한 네트워크에 대한 저항 능력이 강화되었습니다.</li>
                                  <li>평균 시청 딜레이 시간이 1초로, 시청자와 호스트 간의 인터랙션 적극성이 향상되었습니다.</li>
                                  <li>- 한 방에 최대 10만 명까지 입장할 수 있습니다.</li></ul></li>
     <li>오디오 평가 알고리즘(enableAudioVolumeEvaluation)이 최적화되어 음량 평가가 더욱 빠르게 이루어집니다.</li>
     <li>딜레이와 패킷 손실률이 높은 네트워크 환경에서의 QoE 알고리즘이 최적화되어 약한 네트워크에 대한 저항성이 향상되었습니다.</li>
     <li>onStatistics 상태 콜백이 최적화되어 존재하는 스트림만 콜백합니다.</li>
     <li>영상 통화(TRTCAppSceneVideoCall) 모드에서의 QoE 알고리즘이 최적화되어 약한 네트워크 환경에서도 더욱 원활한 1v1 통화 모드가 지원됩니다.</li>
     <li>디코더 성능이 최적화되어 초저가형 Android 휴대폰에서 딜레이가 점차 증가하는 Bug를 수정했습니다.</li>
     <li>약한 네트워크 환경에서 오디오-비디오가 동기화되지 않는 Bug가 최적화되었습니다.</li>
     <li>먼저 muteLocalVideo 후 취소 시 재생 화면 복구 속도가 최적화되었습니다.</li>
     <li>라이브 방송 TXLivePlayer 재생 버퍼 로직이 최적화되어 랙 비율이 감소하였습니다.</li>
</ul><br>인터페이스 변경: <ul style="margin:0;"><li>사용자 역할: TRTCParams에 role 속성이 추가되어 방 입장 시 역할을 지정합니다(호스트, 시청자).</li>
     <li>역할 전환: switchRole, 방 안에서 호스트와 시청자 역할을 동적으로 전환하여 시청자와 호스트의 마이크를 연결합니다.</li>
     <li>콜백 추가: 역할 전환 성공 또는 실패 콜백인 onSwitchRole이 추가되었습니다.</li>
     <li>콜백 변경: onFirstVideoFrame 인터페이스에 streamType 매개변수가 추가되었으며, 비디오 스트림 유형을 명시합니다.</li>
     <li>Windows: getCurrentCameraDevice, getCurrentMicDevice, getCurrentSpeakerDevice 인터페이스 반환 유형이 ITRTCDeviceInfo *로 변경되었으며, getDeviceName 및 getDevicePID를 지원합니다.</li>
</ul></td>   
       <td>2019-06-12</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr>
   <tr>      
         <td>무료 '베타 패키지' 런칭</td>   
         <td><ul style="margin:0;"><li>2019년 6월 1일부터 TRTC 콘솔에서 처음으로 애플리케이션을 생성하는 사용자에게 멀티미디어 시간 1,000분이 포함된 베타 패키지를 제공합니다. 유효 기간은 1년입니다(처음으로 애플리케이션을 생성한 날부터 내년 당월 마지막 날까지).</li>
     <li>2019년 6월 1일부터 체험 패키지, 입문 패키지, 표준 패키지, 엔터프라이즈 패키지를 신규 구매하면 일괄적으로 1년 연장됩니다.</li>
</ul></td>   
       <td>2019-06-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
</table>

## 2019년 04월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 6.4 버전 배포</td>   
         <td>전체 플랫폼: <ul style="margin:0;"><li>약한 네트워크 환경에서의 원활성이 향상되었습니다.</li>
     <li>음량 크기 콜백 알고리즘이 최적화되어 음량 콜백 값이 더욱 합리적으로 변경되었습니다.</li>
     <li>사용자 정의 오디오, 비디오 데이터 전송 시 외부 지정 데이터 프레임 타임스탬프가 지원됩니다.</li>
     <li>혼합 스트림 setMixTranscodingConfig API의 설정 콜백 함수가 추가되었습니다.</li>
     <li>setMixTranscodingConfig 인터페이스가 강화되어 roomID 매개변수를 지원합니다. 크로스 룸 마이크 연결 혼합 스트림에 사용됩니다.</li>
     <li>setMixTranscodingConfig 인터페이스가 강화되어 pureAudio 매개변수를 지원합니다. 음성 통화 전용 시나리오에서의 음성 혼합 스트림 및 녹화에 사용됩니다.</li>
</ul><br>Android: <ul style="margin:0;"><li>엔터프라이즈 버전에 눈 확대, 얼굴 축소, V라인, 움직이는 스티커 기능이 추가되었습니다.</li>
     <li>저가형 Android 기기에서의 720p 비디오 디코딩 성능 문제가 최적화되었습니다.</li>
     <li>로컬 표시 이미지와 인코더 출력 이미지 인터페이스가 추가되었습니다.</li>
</ul><br>Windows: <ul style="margin:0;"><li>Duilib 기반 라이브러리의 다기능 버전 Demo가 추가되었습니다.</li>
     <li>카메라 설정 선택 정책이 최적화되어 디바이스 선택 시 deviceId 전송을 지원합니다.</li>
     <li>일부 Windows 버전의 뷰티 필터 및 렌더링 모듈 호환성 및 성능 문제가 최적화되었습니다.</li>
</ul><br>iOS&Mac: <ul style="margin:0;"><li>부호 중복 Bug가 수정되었습니다.</li>
     <li>iOS 저가형 기기 성능이 최적화되었습니다.</li>
     <li>iOS 엔터프라이즈 버전에 눈 확대, 얼굴 축소, V라인, 움직이는 스티커 기능이 추가되었습니다.</li>
     <li>로컬 표시 이미지와 인코더 출력 이미지 인터페이스가 추가되었습니다.</li>
     <li>sendCustomVideoData에서 NSData 데이터 포맷을 지원합니다.</li>
</ul></td>   
       <td>2019-04-25</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.3 버전 배포</td>   
         <td><ul style="margin:0;"><li>Android 플랫폼 64비트 지원이 추가되었습니다.</li>
     <li>사용자 정의 비디오 수집 인터페이스 TRTCCloud >> sendCustomVideoData가 추가되었습니다.</li>
     <li>사용자 정의 오디오 수집 인터페이스 TRTCCloud >> sendCustomAudioData가 추가되었습니다.</li>
     <li>사용자 정의 비디오 렌더링 인터페이스 TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate가 추가되었습니다.</li>
     <li>사용자 정의 오디오 데이터 콜백 인터페이스 TRTCCloud >> setAudioFrameDelegate가 추가되었습니다. 다음과 같은 기능을 지원합니다.<ul style="margin:0;">
     <li>마이크 수집 데이터 반환: TRTCAudioFrameDelegate >> onCapturedAudioFrame</li>
     <li> 각 채널 원격 사용자의 오디오 데이터 반환: TRTCAudioFram eDelegate >> onPlayAudioFrame</li>
     <li>혼합 후 스피커로 재생한 오디오 데이터 반환: TRTCAudio FrameDelegate >>onMixedPlayAudioFrame</li>
</ul></ul></td>   
       <td>2019-04-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>월별 기능 사용 요금 취소</td>   
         <td>2019년 3월부터 1500위안/월의 월별 기능 사용 요금을 부과하지 않습니다. 과금 변경은 2019년 4월 1일 발송되는 청구서부터 적용됩니다.</td>   
       <td>2019-04-01</td>   
       <td>-</td>   
     </tr> 
</table>

## 2019년 03월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 6.2 버전 배포</td>   
         <td>Windows: <ul style="margin:0;"><li>TRTCCloud 클래스가 순수 가상 인터페이스 ITRTCCloud로 변경되어 LoadLibirary를 통해 동적으로 DLL을 로딩합니다.</li>
     <li>오디오 데이터 콜백 ITRTCAudioFrameCallback이 추가되었습니다.</li>
     <li>camera 호환성 및 수집 성능이 최적화되었습니다.</li></ul><br>
     Android, iOS, Mac, Windows: <ul style="margin:0;"><li>크로스 룸 통화 기능인 connectOtherRoom이 추가되었습니다. 이미 존재하는 두 개의 TRTC 방을 서로 연결하는 기능으로, 라이브 룸 호스트 PK에 사용됩니다.</li>
     <li>sendSEIMsg() 인터페이스가 추가되었습니다. 비디오 프레임의 SEI 헤드 정보를 통한 사용자 정의 메시지 발송을 지원하며, 일반적으로 비디오 스트림에 타임스탬프 정보를 삽입하는 데 사용합니다.</li>
     <li>CPU 사용률 및 안정성이 최적화되었습니다.</li>
     <li>음성 통화 전용 시나리오(예: 마피아 게임)에서 릴레이 푸시 스트림 기능을 복구하려면 TRTCParam의 bussInfo 필드를 함께 사용해야 합니다.</li>
     <li>약한 네트워크(연결 상태가 좋지 않은 네트워크 환경)에서의 화면 해상도가 향상되었습니다.</li>
     <li>TRTCCloud의 다중 인스턴스 기능을 취소하고 생성 모드를 단일 인스턴스 모드로 변경하여 다수의 TRTCCloud 인스턴스가 서로의 네트워크 리소스를 점유하지 않고 체험 효과에 영향을 미치지 않도록 방지합니다.</li>
     <li>필터 농도 설정 인터페이스 setFilterConcentration()이 추가되었습니다.</li>
</ul></td>   
       <td>2019-03-08</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
</table>

## 2019년 01월

<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>  </tr> 
<tr>      
         <td>SDK Version 6.1 버전 배포</td>   
         <td><ul style="margin:0;"><li>Windows, Mac에서 화면 공유를 지원합니다.</li>
     <li>화면 공유 스트림 보기 기능을 지원합니다.</li>
     <li>사용자 정의 비디오 데이터 전송을 지원합니다.</li>
     <li>CDN 푸시 및 혼합 스트림 구현이 최적화되었습니다.</li>
     <li>방 입장 시 라이브 방송과 영상 통화 시나리오로 구분됩니다.</li>
     <li>안정성이 개선되고, 가끔 crash가 발생하는 문제가 해결되었습니다.</li>
     <li>iOS, Windows 메모리 점유율이 최적화되었습니다.</li>
     <li>트래픽 제어가 최적화되어 약한 네트워크 환경에서의 성능이 향상되었습니다.</li>
</ul></td>   
       <td>2019-01-31</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.0 버전 배포(TRTC SDK 첫 번째 버전)</td>   
         <td><ul style="margin:0;"><li>아키텍처가 LiteAV 커널로 업데이트되었습니다.</li>
     <li>새로운 QoS 알고리즘을 적용하여 랙 발생률이 감소하고 원활성이 향상되었습니다.</li>
     <li>새로운 Audio 모듈을 적용하여 각종 네트워크 상황에서의 오디오 품질이 대폭 최적화되었습니다.</li>
     <li>대형/소형 스트림 듀얼 채널 인코딩 기능을 지원합니다(Windows와 Mac 디바이스에서만 활성화 추천).</li>
     <li>CDN 푸시 및 혼합 스트림 기능을 지원합니다.</li>
</ul></td>   
       <td>2019-01-18</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>   
     </tr> 
</table>




## 2021년 03월
<table>
<tr><th width="20%">업데이트 명칭</th>  <th width="50%">업데이트 설명</th>  <th width="15%">배포일</th>  <th width="15%">관련 문서</th>
</tr><tr>
<td>Version 8.5 버전 배포</td>
<td>전체 플랫폼:<ul style="margin:0">
<li>VOD 재생 기능 추가. TXVODPlayer와 TRTCCloud를 바인딩한 후, TRTC 서브 채널 푸시 스트림을 통해 현재 VOD에서 재생 중인 콘텐츠를 공유할 수 있습니다.</li>
<li>서브 채널 사용자 정의 수집 추가. API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629">sendCustomVideoData</a>를 참조하십시오.</li>
<li>사용자 정의 오디오 혼합 기능 추가. 사용자의 오디오 트랙 채널을 SDK 오디오 처리 프로세스에 혼합할 수 있습니다. SDK에서 두 채널의 오디오 트랙을 혼합한 후 함께 배포합니다. 자세한 내용은 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f">mixExternalAudioFrame</a>을 참조하십시오.</li>
<li>퓨어 비디오 혼합 스트림 지정 기능 지원으로 효율적인 혼합 스트림 제어 가능</li>
<li>상태 콜백에 end to end 딜레이 추가</li>
</ul>
<br>Windows:<ul style="margin:0">
슬라이드 창 선택 후 화면 공유 시, 자동으로 슬라이드 쇼 창으로 전환
</ul>
<br>Mac:<ul style="margin:0">
<li>화면 공유 기능 최적화. 타깃 창 공유 중 다른 창을 지정하여 함께 공유할 수 있습니다. 자세한 내용은 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>를 참조하십시오.</li>
<li>startSystemAudioLoopback에서 듀얼 사운드 채널 지원</li>
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
<td>전체 플랫폼:<ul style="margin:0">
<li>로컬 멀티미디어 녹화 기능 추가. 호스트가 푸시 스트리밍 중 로컬 오디오와 비디오를 하나의 mp4 파일로 녹화할 수 있습니다. 자세한 내용은 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b">startLocalRecording</a>을 참조하십시오.</li>
<li><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb">Music</a> 모드 오디오 음량 최적화. cloubhouse와 같은 음성 라이브 방송 시나리오에 더욱 적합합니다.</li>
<li>멀티미디어 링크의 네트워크 저항력 최적화. 전체 네트워크에서 70%를 차지하는 열악한 네트워크 환경에서도 멀티미디어가 비교적 원활하게 재생됩니다.</li>
</ul>
<br>Windows:<ul style="margin:0">
<li>일부 시나리오의 라이브 방송 음질을 최적화하여 오디오 품질 저하 문제가 대폭 감소되었습니다.</li>
<li>성능 최적화로 일부 사용 시나리오에서 구버전 대비 성능이 20%~30% 향상되었습니다.</li>
<li>프로세스 음량 조정 기능 추가. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1">setApplicationPlayVolume</a>을 사용해 시스템 음량 믹서의 음량 크기를 설정할 수 있습니다.</li>
</ul>
<br>Mac:<ul style="margin:0">
<li>Mac 운영 체제의 출력 오디오 수집 지원. Windows와 동일한 SystemLoopback 기능으로, SDK에서 현재 시스템 오디오를 수집하도록 합니다. 해당 기능을 활성화하면, 호스트가 편리하게 다른 사용자에게 음악 또는 영화 파일을 라이브 방송할 수 있습니다.</li>
<li>화면 공유 시 로컬 미리보기 기능 지원. 미니 창을 통해 다른 사용자에게 공유할 화면 콘텐츠를 미리 보여줄 수 있습니다.</li>
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
<td>전체 플랫폼: <ul style="margin:0">비디오 데이터를 직접 수집하고 TRTC SDK 자체 오디오 모듈을 사용해야 할 경우, 오디오-비디오가 동기화되지 않는 문제가 발생할 수 있습니다. SDK 내부 타임라인 자체의 제어 로직으로 인한 문제이며, 이에 대한 대응책으로 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee">generateCustomPTS</a> 인터페이스가 제공됩니다. 비디오 화면을 수집할 때 이 인터페이스를 호출하여 현재 PTS(타임스탬프)를 기록한 다음 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831">sendCustomVideoData</a> 호출 시 이 타임스탬프를 적용하면 오디오-비디오 동기화를 유지할 수 있습니다.</ul>
<br>iOS &amp; Android &amp; Mac: <ul style="margin:0">오디오 모듈을 최적화했습니다. <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a>를 사용해 수집한 오디오 데이터를 SDK에 전송하여 처리할 경우 SDK에서 에코 억제 및 노이즈 감소 효과가 유지됩니다.</ul>
<br>iOS &amp; Android: <ul style="margin:0">TRTC SDK를 기반으로 오디오 특수 효과 및 오디오 처리 로직을 계속 추가해야 할 경우, 8.3 버전을 사용하면 더욱 간편합니다. 8.3 버전에서는 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86">setCapturedRawAudioFrameDelegateFormat</a> 등의 인터페이스를 통해 오디오 샘플링 레이트, 오디오 사운드 채널 수, 샘플링 포인트 수 등 오디오 데이터 콜백 포맷을 설정할 수 있기 때문에 사용자가 선호하는 오디오 포맷으로 해당 오디오 데이터를 처리할 수 있습니다.</ul>
<br>Windows: <ul style="margin:0">Windows 버전 SDK에 도메인 포맷의 Socks5 프록시 주소 지원 추가</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 다운로드</a></td>
</tr></table>


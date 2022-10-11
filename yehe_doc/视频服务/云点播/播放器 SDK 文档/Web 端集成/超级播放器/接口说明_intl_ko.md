
본 문서는 라이브 및 VOD 재생을 위한 Web ( TCPlayer )의 관련 매개변수 및 API를 소개합니다. 본 문서는 JavaScript에 대한 기본 지식이 있는 개발자를 대상으로 합니다.

## 초기화 매개변수
플레이어를 초기화하기 위해 두 개의 매개변수, 즉 플레이어 컨테이너 ID와 함수 매개변수 객체를 전달해야 합니다.
```
var player = TCPlayer('player-container-id', options);
```

### options 매개변수 목록
options 객체에 대해 구성할 수 있는 매개변수는 다음과 같습니다.

| 이름    | 유형                      | 기본값                        |설명 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  appID|  String |   없음 |필수.|
|  fileID|  String|없음|필수.|
|  sources|  Array|없음|플레이어 재생 주소, 형식: [{ src: '//path/to/video.mp4', type: 'video/mp4' }]|
|  width|  String/Number|  없음| 플레이어 영역 너비(픽셀). 필요에 따라 설정해야 하며 CSS를 통해 플레이어 크기를 제어할 수 있습니다.|
|  height |  String/Number|  없음|  플레이어 영역 높이(픽셀). 필요에 따라 설정해야 하며 CSS를 통해 플레이어 크기를 제어할 수 있습니다.|
|  controls|  Boolean|  true|  플레이어의 컨트롤 바 표시 여부입니다.|
|  poster|  String|  없음|  커버 이미지의 전체 주소를 설정합니다. 업로드된 비디오에 이미 생성된 커버가 있는 경우 우선 사용됩니다. 자세한 내용은 [VOD - 비디오 관리](https://intl.cloud.tencent.com/document/product/266/33896)를 참고하십시오.|
|  autoplay|  Boolean|  false|  자동 재생 여부입니다.|
|  playbackRates|  Array| [0.5, 1, 1.25, 1.5, 2]|  HTML5에서만 사용할 수 있는 조정 가능한 속도 재생 옵션을 설정합니다.|
|  loop|Boolean|  false|  비디오 반복 재생 여부입니다.|
|  muted|  Boolean|  false|  비디오 음소거 여부입니다.|
|  preload|  String|  auto|  사전 로딩 필요 여부입니다. "auto", "meta" 및 "none"의 세 가지 속성이 있습니다. 시스템 제한으로 인해 auto는 모바일 장치에 적용되지 않습니다.|
|  swf|  String|  없음|  Flash 플레이어에 있는 swf 파일의 URL입니다.|
|  posterImage|  Boolean|  true|  커버 표시 여부입니다.|
|  bigPlayButton|  Boolean|  true|  중앙에 있는 재생 버튼 표시 여부(브라우저 하이재킹에 의해 포함된 재생 버튼은 제거할 수 없음)입니다.|
|  language|  String|  "zh-CN" |  언어 설정, 옵션 값: "zh-CN"/"en" |
|  languages|  Object|  없음|  다국어 사전을 설정합니다.|
|  controlBar|  Object|  없음|  아래에 자세히 설명된 대로 컨트롤 바 속성의 매개변수 조합을 설정합니다.|
|  reportable|  Boolean |  true | 데이터 리포트 활성화 여부를 설정합니다.|
|  plugins|  Object|  없음|  플러그인 기능 속성의 매개변수 조합을 아래와 같이 설정합니다.|
|  hlsConfig|  Object|  없음|  hls.js 시작 구성입니다. 자세한 내용은 [hls.js](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning)를 참고하십시오.|
|  webrtcConfig|  Object|  없음|  webrtc의 시작 구성, 아래 자세한 소개가 있습니다.|


>! 브라우저 하이재킹 재생 중에는 controls, playbackRates, loop, preload, posterImage 매개변수가 적용되지 않습니다.

#### controlBar 매개변수 목록
controlBar 매개변수는 플레이어의 컨트롤 바 기능을 구성할 수 있습니다. 지원되는 속성은 다음과 같습니다.

| 이름    | 유형                      | 기본값                        |설명 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  playToggle| Boolean|  true|  재생/일시 정지 토글 버튼 표시 여부입니다.|
|  progressControl|  Boolean| true|  진행률 표시 바 표시 여부입니다.|
|  volumePanel|  Boolean|  true|  볼륨 컨트롤 표시 여부입니다.|
|  currentTimeDisplay|  Boolean|  true|  비디오의 현재 시간 표시 여부입니다.|
|  durationDisplay|  Boolean|  true|  비디오 길이 표시 여부입니다.|
|  timeDivider|  Boolean|  true|  시간 구분 기호 표시 여부입니다.|
|  playbackRateMenuButton|  Boolean|  true|  재생 속도 선택 버튼 표시 여부입니다.|
|  fullscreenToggle|  Boolean|  true|  전체 화면 토글 버튼 표시 여부입니다.|
|  QualitySwitcherMenuButton|  Boolean|  true|  해상도 전환 메뉴 표시 여부입니다.|

>! 브라우저 하이재킹 재생 중에는 controlBar 매개변수가 적용되지 않습니다.

#### plugins 매개변수 목록
plugins 매개변수는 플레이어 플러그 인의 기능을 구성할 수 있습니다. 지원되는 속성은 다음과 같습니다.

| 이름    | 유형                      | 기본값                        |설명 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  ContinuePlay|  Object|  없음|  재생 재개 기능을 제어합니다. 지원되는 속성은 다음과 같습니다: <br><li>auto: Boolean 재생 중에 자동 재개 여부<br><li>text: String 프롬프트 텍스트<br><li>btnText: String 버튼 텍스트|
| VttThumbnail | Object | 없음 | 썸네일 표시를 제어합니다. 지원되는 속성은 다음과 같습니다: <br><li>vttUrl: String vtt 파일 절대 주소, 필수<br><li>basePath: String 이미지 경로, 옵션, 전달되지 않은 경우 vttUrl의 path 사용<br><li>imgUrl: String 이미지 절대 주소, 옵션 |
| ProgressMarker | Boolean | 없음 | 진행률 표시 제어 |
| DynamicWatermark | Object | 없음 | 동적 워터마크 표시를 제어합니다. 지원되는 속성은 다음과 같습니다: <br><li>content: String 텍스트 워터마크 콘텐츠, 필수<br><li>speed: Number 워터마크 이동 속도, 값 범위 0-1, 옵션 |
| ContextMenu | Object | 없음 | 옵션값은 다음과 같습니다: <br><li>mirror: Boolean 미러 표시 지원 여부 제어<br><li>statistic: Boolean 데이터 패널 표시 지원 여부 제어<br><li>levelSwitch: Object 해상도 전환 시 텍스트 프롬프트 제어<br><li>&emsp;{<br><li>&emsp;&emsp;open: Boolean 프롬프트 활성화 여부<br><li>&emsp;&emsp;switchingText: String, 해상도 전환 시 프롬프트 텍스트<br><li>&emsp;&emsp;switchedText: String, 전환 성공 시 프롬프트 텍스트<br><li>&emsp;&emsp;switchErrorText: String, 전환 실패 시 프롬프트 텍스트<br><li>&emsp;}|


#### webrtcConfig 매개변수 리스트
webrtcConfig 매개변수는 webrtc 재생 중 동작을 제어합니다. 지원되는 속성은 다음과 같습니다.

| 이름    | 유형                      | 기본값                        |설명 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  connectRetryCount| Number|  3|  SDK와 서버 간 재접속 시도 횟수|
|  connectRetryDelay|  Number| 1|  SDK와 서버 간 재접속 딜레이|
|  receiveVideo|  Boolean|  true|  비디오 스트림 풀링 여부|
|  receiveAudio|  Boolean|  true|  오디오 스트림 풀링 여부|
|  showLog|  Boolean|  false|  콘솔에 로그 출력 여부|


<br>

## 객체 메소드
다음은 플레이어 초기화에서 반환된 객체의 메소드 목록입니다.

| 이름    | 매개변수 및 유형                 | 반환 값 및 유형                        |설명 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  src()|  (String)|  없음|  재생 주소를 설정합니다.|
|  ready(function)|  (Function)|  없음|  플레이어가 초기화된 후 콜백을 설정합니다.|
|  play()|  없음|  없음|  비디오를 재생하고 다시 시작합니다.|
|  pause()|  없음|  없음|  비디오를 일시 중지합니다.|
|  currentTime(seconds)|  (Number)|  (Number)|  현재 재생 시점을 가져오거나 비디오 지속 시간을 초과할 수 없는 재생 시점을 설정합니다.|
|  duration()|  없음|  (Number)|  비디오 길이를 가져옵니다.|
|  volume(percent)|  (Number)[0, 1][옵션]|  (Number)/설정 시 반환되지 않음|  플레이어 볼륨을 가져오거나 설정합니다.|
|  poster(src)|  (String)|  (String)/설정 시 반환되지 않음|  플레이어 커버를 가져오거나 설정합니다.|
|  requestFullscreen()|  없음|  없음|  전체 화면 모드로 들어갑니다.|
|  exitFullscreen()|  없음|  없음|  전체 화면 모드를 종료합니다.|
|  isFullscreen()|  없음|  Boolean|  전체 화면 모드로 전환되었는지 여부를 반환합니다.|
|  on(type, listener)|  (String, Function)|  없음|  이벤트를 수신합니다.|
|  one(type, listener)|  (String, Function)|  없음|  이벤트를 수신합니다. 이벤트 핸들러는 최대 한 번만 실행할 수 있습니다.|
|  off(type, listener)|  (String, Function)|  없음|  이벤트 수신을 바인딩 해제합니다.|
|  buffered()|  없음|  TimeRanges|  비디오 버퍼링의 시간 범위를 반환합니다.|
|  bufferedPercent()|  없음|  값 범위[0, 1]|  비디오 지속 시간에서 버퍼링된 길이의 백분율을 반환합니다.|
|  width()|  (Number)[옵션]|  (Number)/설정 시 반환되지 않음|  플레이어 영역의 너비를 가져오거나 설정합니다. CSS를 통해 플레이어 크기를 설정하면 이 방법이 적용되지 않습니다.|
|  height()|  (Number)[옵션]|  (Number)/설정 시 반환되지 않음|  플레이어 영역의 높이를 가져오거나 설정합니다. CSS를 통해 플레이어 크기를 설정하면 이 방법이 적용되지 않습니다.|
|  videoWidth()|  없음|  (Number)|  비디오 해상도의 너비를 가져옵니다.|
|  videoHeight()|  없음|  (Number)|  비디오 해상도의 높이를 가져옵니다.|
|  dispose()|  없음|  없음|  플레이어를 종료합니다.|

>! 객체 메소드는 동기식으로 호출할 수 없지만 ready, on, one 및 off를 제외하고 해당 이벤트(예: loadedmetadata)가 트리거된 후에만 호출할 수 있습니다.

## 이벤트
플레이어는 초기화에서 반환된 객체를 통해 이벤트 수신을 수행할 수 있습니다. 예를 들면 다음과 같습니다.
```
var player = TCPlayer('player-container-id', options);
// player.on(type, function);
player.on('error', function(error) {
   // 프로세스
});
```
여기서 type은 이벤트 유형입니다. 지원되는 이벤트는 다음과 같습니다.

| 이름    | 설명                    |
|------------|---------------------------------|
|  play|  재생이 시작되었습니다. play() 메소드가 호출되거나 autoplay가 true로 설정되고 적용되면 트리거됩니다. 이 때 paused 속성은 false입니다.|
|  playing|  버퍼링으로 인해 재생이 일시 중지되거나 일시 중지 후 다시 시작될 때 트리거됩니다. paused 속성은 false입니다. 일반적으로 이 이벤트는 play 이벤트가 재생을 시작하고 이미지가 렌더링을 시작하지 않았기 때문에 비디오 재생이 실제로 시작되었음을 표시하는 데 사용됩니다.|
|  loadstart|  데이터 로딩가 시작될 때 트리거됩니다.|
|  durationchange|  비디오의 지속 시간 데이터가 변경될 때 트리거됩니다.|
|  loadedmetadata|  비디오 metadata가 로딩되었습니다.|
|  loadeddata|  이 이벤트는 현재 프레임의 데이터가 로딩되었지만 비디오의 다음 프레임을 재생할 데이터가 충분하지 않을 때 트리거됩니다.|
|  progress|  미디어 데이터를 얻을 때 트리거됩니다.|
|  canplay|  플레이어가 비디오 재생을 시작할 수 있을 때 트리거됩니다.|
|  canplaythrough|  플레이어가 버퍼링 없이 지정된 비디오를 계속 재생할 수 있을 것으로 예상되면 트리거됩니다.|
|  error|  비디오 재생에서 오류가 발생하면 트리거됩니다.|
|  pause|  비디오가 일시 중지되면 트리거됩니다.|
|  ratechange|  재생 속도가 변경되면 트리거됩니다.|
|  seeked|  지정된 재생 위치 탐색이 종료되면 트리거됩니다.|
|  seeking|  지정된 재생 위치 탐색이 시작될 때 트리거됩니다.|
|  timeupdate|  현재 재생 위치가 변경되었으며 이는 currentTime이 변경되었음을 알 수 있습니다.|
|  volumechange|  볼륨이 설정되거나 muted 속성 값이 변경될 때 트리거됩니다.|
|  waiting|  비디오가 중지되고 콘텐츠의 다음 프레임을 사용할 수 없을 때 트리거됩니다.|
|  ended|  비디오 재생이 끝나면 트리거됩니다. 이 경우 currentTime 값은 미디어 리소스의 최대값과 같습니다.|
|  resolutionswitching|  해상도 전환이 진행 중입니다.|
|  resolutionswitched|  해상도 전환이 완료되었습니다.|
|  fullscreenchange| 전체 화면 모드가 전환될 때 트리거됩니다.|
|  webrtcevent | webrtc 재생 시 이벤트 컬렉션입니다.|
|  webrtcstats | webrtc 재생 시 통계 데이터입니다.|


### WebrtcEvent 리스트

플레이어는 webrtcevent를 통해 webrtc 재생 과정에서 모든 이벤트를 가져올 수 있습니다. 예시는 다음과 같습니다.
```
var player = TCPlayer('player-container-id', options);
player.on('webrtcevent', function(event) {
   // 콜백 매개변수 event에서 이벤트 상태 코드 및 관련 데이터 가져오기
});
```
webrtcevent 상태 코드는 다음과 같습니다

| 상태 코드 | 콜백 매개변수 | 소개 |
|------|-------|-------|
| 1001 | 없음 | 풀 스트림 시작 |
| 1002 | 없음 | 서버에 연결됨 |
| 1003 | 없음 | 비디오 재생 시작 |
| 1004 | 없음 | 풀 스트림 중지, 비디오 재생 종료 |
| 1005 | 없음 | 서버 접속 실패, 자동 재접속 복구가 시작됨 |
| 1006 | 없음 | 가져온 스트림 데이터가 비어 있음 |
| 1007 | localSdp | 신호 서버 요청 시작 |
| 1008 | remoteSdp | 신호 서버 요청 성공 |
| 1009 | 없음 | 버퍼링 대기 중 풀 스트림 랙 |
| 1010 | 없음 | 풀 스트림 랙 종료 및 재생 복구 |


## 오류 코드
플레이어가 error 이벤트를 트리거하면 리스너가 오류 코드를 반환합니다. 3자리 이상의 오류 코드는 미디어 데이터 API용입니다. 다음은 오류 코드 목록입니다.

| 이름 | 설명                                           |
|------|----------------------------------------------|
| -1   | 플레이어가 사용 가능한 비디오 주소를 감지하지 못했습니다.                  |
| -2   | 비디오 데이터 가져오기 시간이 초과되었습니다.                               |
| 1    | 로딩하는 동안 비디오 데이터가 중단되었습니다. <br>가능한 원인:<br><li> 네트워크가 중단되었습니다.<br><li> 브라우저가 중단되었습니다. <br>솔루션:<br><li> 네트워크 콘솔에서 네트워크 요청 정보를 확인하여 네트워크 요청이 정상인지 확인합니다.<br><li>재생 프로세스를 다시 시작합니다.                             |
| 2    | 네트워크 문제로 인해 비디오를 로딩하지 못했습니다. <br>가능한 원인: 네트워크가 중단되었습니다. <br>솔루션:<br><li> 네트워크 콘솔에서 네트워크 요청 정보를 확인하여 네트워크 요청이 정상인지 확인합니다.<br><li> 재생 프로세스를 다시 시작합니다.                     |
| 3    | 비디오를 디코딩하는 동안 오류가 발생했습니다. <br>가능한 원인: 비디오 데이터가 예외적이고 디코더가 디코딩하지 못했습니다. <br>솔루션:<br><li> 트랜스코딩을 시도하고 비디오를 다시 재생하여 트랜스코딩 프로세스로 인해 발생하는 문제를 해결합니다.<br><li> 원본 영상이 정상인지 확인합니다. <br><li> 기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.                                |
| 4    | 지원되지 않는 형식이나 서버 또는 네트워크 문제로 인해 동영상을 로딩할 수 없습니다. <br>가능한 원인:<br><li> 비디오 데이터를 가져올 수 없거나 CDN 리소스가 없거나 비디오 데이터가 반환되지 않았습니다.<br><li> 현재 재생 환경이 이 비디오 형식을 지원하지 않습니다. <br>솔루션:<br><li> 네트워크 콘솔에서 네트워크 요청 정보를 확인하여 영상 데이터 요청이 정상인지 확인하십시오.<br><li> 사용자 가이드에 따라 이 비디오 형식에 해당하는 재생 스크립트가 로딩되었는지 확인하십시오.<br><li> 현재 브라우저와 웹페이지 환경이 이 동영상 형식을 지원하는지 확인합니다. <br><li> 기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.     |
| 5    | 동영상을 복호화하는 중에 오류가 발생했습니다. <br>가능한 원인:<br><li> 암호 해독 키가 잘못되었습니다.<br><li> API 요청 키 반환 예외가 발생했습니다.<br><li> 현재 재생 환경이 동영상 복호화 기능을 지원하지 않습니다. <br>솔루션:<br><li> 키 및 키 API 정상 반환 여부를 확인합니다.<br><li> 기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.<br>                                  |
| 10   | VOD 미디어 데이터 API 요청 시간이 초과되었습니다. 미디어 데이터를 가져오려고 할 때 플레이어가 3번의 재시도 후에도 응답이 없으면 이 오류가 발생합니다. <br>가능한 원인:<br><li> 현재 네트워크가 미디어 데이터 API에 연결할 수 없거나 미디어 데이터 API가 하이재킹되었습니다.<br><li> 미디어 데이터 API 예외가 발생하였습니다. <br>솔루션:<br><li> 당사가 제공하는 Demo 페이지를 열어서 동영상이 정상적으로 재생되는지 확인합니다. <br><li>기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.<br>                           |
| 11   | VOD 미디어 데이터 API가 데이터를 반환하지 않았습니다. 미디어 데이터를 가져오려고 할 때 플레이어가 3번의 재시도 후에도 데이터를 받지 못하면 이 오류가 발생합니다. <br>가능한 원인:<br><li> 현재 네트워크가 미디어 데이터 API에 연결할 수 없거나 미디어 데이터 API가 하이재킹되었습니다.<br><li> 미디어 데이터 API 예외가 발생하였습니다. <br>솔루션:<br><li> 당사가 제공하는 Demo 페이지를 열어서 동영상이 정상적으로 재생되는지 확인합니다. <br><li> 기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.<br>                        |
| 12   | VOD 미디어 데이터 API가 예외 데이터를 반환했습니다. 미디어 데이터를 가져오려고 할 때 플레이어가 3번의 재시도 후에도 구문 분석할 수 없는 데이터를 계속 수신하면 이 오류가 발생합니다. <br>가능한 원인:<br><li> 현재 네트워크가 미디어 데이터 API에 연결할 수 없거나 미디어 데이터 API가 하이재킹되었습니다.<br><li> 재생 매개변수가 올바르지 않아 미디어 데이터 API에서 처리할 수 없습니다.<br><li> 미디어 데이터 API 예외가 발생하였습니다. <br>솔루션:<br><li> 당사가 제공하는 Demo 페이지를 열어서 동영상이 정상적으로 재생되는지 확인합니다. <br><li> 기술 지원에 문의하고 문제 해결을 위한 재생 매개변수를 제공합니다.<br>                   |
| 13   | 플레이어가 현재 플레이어에서 재생할 수 있는 비디오 데이터를 감지하지 못했습니다. 동영상을 트랜스코딩하십시오. |
| 14   | HTML5 + hls.js 모드에서 hls 비디오를 재생하는 동안 네트워크 예외가 발생했습니다. 예외 세부 정보는 event.source에서 볼 수 있습니다. 자세한 내용은 [Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors)를 참고하십시오. |
| 15   | HTML5 + hls.js 모드에서 hls 비디오를 재생하는 동안 미디어 예외가 발생했습니다. 예외 세부 정보는 event.source에서 볼 수 있습니다. 자세한 내용은 [Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors)를 참고하십시오.   |
| 16   | HTML5 + hls.js 모드에서 hls 비디오를 재생하는 동안 리먹싱 예외가 발생했습니다. 예외 세부 정보는 event.source에서 볼 수 있습니다. 자세한 내용은 [Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors)를 참고하십시오.     |
| 17   | HTML5 + hls.js 모드에서 hls 비디오를 재생하는 동안 다른 유형의 예외가 발생했습니다. 예외 세부 정보는 event.source에서 볼 수 있습니다. 자세한 내용은 [Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors)를 참고하십시오.     |
| 10008| 미디어 데이터 서비스가 재생 매개변수에 해당하는 미디어 데이터를 찾지 못했습니다. 요청 매개변수 appID와 fileID가 올바른지, 해당 미디어 데이터가 삭제되었는지 확인하십시오. |


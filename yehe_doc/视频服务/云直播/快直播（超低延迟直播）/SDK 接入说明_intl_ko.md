LEB는 LVB를 초저지연 재생 시나리오에 적용한 것으로, 기존 라이브 방송 프로토콜보다 딜레이가 훨씬 낮은 밀리초 단위의 고품질**라이브 방송 시청**경험을 선사합니다.

> ! LEB는 저지연을 특징으로 하는 WebRTC 프로토콜을 사용하기 때문에, 기본적으로 B-프레임을 지원하지 않으며, 오디오 코딩/디코딩 방식으로 opus 코덱을 채택합니다. 원본 스트림에 B-프레임이 포함되어 있거나 코덱이 Opus가 아닌 경우, CSS 백엔드는 B-프레임을 제거하고 스트림을 Opus 형식으로 트랜스코딩하므로 [표준 트랜스 코딩 요금](https://intl.cloud.tencent.com/document/product/267/39604)이 발생합니다.

[](id:app)
## App 구현
iOS, Android의 애플리케이션은 MLVB SDK를 통합하여 App의 라이브 방송 푸시 스트리밍 및 재생 기능을 구현합니다.

- **App 라이브 방송 푸시 스트림**: 카메라 화면 및 휴대폰 인터페이스 수집을 지원하며, RTMP 프로토콜을 통해 빠르게 CSS 서비스로 푸시 스트리밍합니다. 자세한 내용은 [카메라 푸시 스트림](https://intl.cloud.tencent.com/document/product/1071/38157) 및 [화면 녹화 푸시 스트림](https://intl.cloud.tencent.com/document/product/1071/41878)을 참고하십시오.
- **App 라이브 방송 재생**: WebRTC 재생 프로토콜을 지원하며, LEB와 연동하여 저지연 라이브 방송 경험을 빠르게 구현합니다. 자세한 내용은 [LEB 풀 스트림](https://intl.cloud.tencent.com/document/product/1071/41875)을 참고하십시오.

>? MLVB SDK는 CSS, 인스턴트 메시지 IM, TRTC 및 기타 서비스를 통해 다중 사용자 멀티미디어 저지연 상호 연결 및 통신 효과를 구현하였으며, 다중 인터렉티브 마이크 연결 효과를 구현하였습니다. 마이크를 연결하지 않는 시청자도 라이브 방송 서비스를 통해 시청할 수 있습니다. 자세한 내용은 [라이브 방송 마이크 연결 인터랙션](https://intl.cloud.tencent.com/document/product/1071/39888)을 참고하십시오.

[](id:web)
## Web 구현
라이브 방송 푸시 스트림 및 재생이 필요한 웹 사이트가 있는 경우 다음 방법을 사용하여 구현하는 것을 권장합니다.

- **Web 라이브 방송 푸시 스트림**: 브라우저의 범용 WebRTC 표준을 기반으로 설계 및 캡슐화되었으며, 코드 스니펫을 도입하여 브라우저에서 라이브 방송 푸시 스트림을 구현할 수 있습니다. 자세한 내용은 [WebRTC 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/41620)을 참고하십시오.
> ! WebRTC 푸시 스트림 오디오 인코딩은 opus 코덱만 지원합니다. LVB의 재생 프로토콜(RTMP, FLV, HLS)을 사용하여 재생하는 경우, 정상적인 시청을 보장하기 위해 CSS 백그라운드는 자동으로 오디오 트랜스 코딩을 aac 인코딩으로 전환합니다. 이로 인해 오디오 트랜스 코딩 요금이 발생됩니다. 자세한 내용은 [오디오 트랜스 코딩 과금 설명](https://intl.cloud.tencent.com/document/product/267/39604#a_trans)을 참고하십시오(LEB만 사용하는 경우 오디오 트랜스 코딩이 시작되지 않습니다.).
- **Web 라이브 방송 재생**: 플레이어 SDK의 TCPlayerLite를 사용할 것을 권장하며 휴대폰 브라우저 및 PC 브라우저에서 재생할 수 있습니다.**LEB WebRTC 프로토콜**라이브 방송 스트림은 기존 라이브 방송 프로토콜보다 딜레이 시간이 짧아 밀리초 단위의 고품질 라이브 방송 시청 경험을 선사합니다.
> ! WebRTC를 지원하지 않는 브라우저 환경에서, 플레이어에 전달된 WebRTC 주소는 미디어 재생을 더 잘 지원하기 위해 자동으로 프로토콜 변환을 진행합니다. 모바일 브라우저는 기본적으로 HLS로, PC 브라우저는 기본적으로 FLV로 변환됩니다.

[](id:obs)
## OBS WebRTC 프로토콜 푸시 스트림 구현
webRTC 프로토콜 푸시 스트림은 비디오 클라우드 LEB(초저지연 라이브 방송) 푸시 스트림에 주로 사용되며, 수집한 멀티미디어 화면 및 비디오 파일을 WebRTC 프로토콜을 통해 라이브 방송 서버로 푸시하는 역할을 합니다. OBS 툴을 사용하여 webRTC 프로토콜 푸시 스트림 기능을 구현하는 방법은 다음 내용을 참고하십시오.

### 주의사항
OBS 버전은 26 버전 또는 상위 버전을 사용해야 합니다.

[](id:set)
### OBS 플러그 인 설정
1. **플러그 인 데이터 설정**.
[OBS 플러그 인](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip)을 다운로드하고, data 파일의 `services.json` 및 `package.json` 파일을 해당 **obs-studio** > **rtmp-service** > **data** 디렉터리로 옮겨 덮어쓰기합니다. (`obs-studio`는 기본적으로 C 드라이버에 설치되고 해당 디렉터리는 `C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`입니다. 실제 비즈니스 상황에 따라 설정하십시오.)
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **플러그 인 동적 라이브러리 설정**.
`obs-plugins\64bit`의 dll 및 pdb 파일을 해당 **obs-studio** > **obs-plugins** > **64bit** 디렉터리로 옮깁니다.(`obs-studio`는 기본적으로 C 드라이버에 설치되고 해당 디렉터리는 `C:\Program Files\obs-studio\obs-plugins\64bit`입니다. 실제 비즈니스 상황에 따라 설정하십시오.)
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### 푸시 스트림 링크 설정
[](id:push)
1. **webRTC 푸시 스트림 주소 생성**.
	1. Tencent Cloud CSS 콘솔에 로그인하고, **라이브 방송 툴 킷**>**[주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)**에서 푸시 스트림 주소를 생성합니다. 작업에 대한 자세한 내용은 [주소 생성기](https://intl.cloud.tencent.com/document/product/267/31084)를 참고하십시오.
	2. 생성한 `rtmp` 접두사를 `webrtc`로 변경합니다. 사용 관련 자세한 설명은 [라이브 방송 URL 직접 조합](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.
![](https://main.qcloudimg.com/raw/43330aaa66610d7884f9dc02bd931dd1.png)    
2. **OBS 푸시 스트림 서비스 설정**.[](id:set_obs)
	1. OBS를 활성화하면 하단 툴바의 **컨트롤러**>**설정**버튼을 통해 인터페이스를 설정할 수 있습니다.
	2. **푸시 스트림**을 클릭하여 스트림 설정 탭으로 이동합니다. 서비스 유형은 `Tenent webrtc`, 서버는 `Default`를 선택하고, 스트림 키에 사전에 생성한 [WebRTC 푸시 스트림 주소](#push)를 입력한 후 뒷부분에 `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`을 조합합니다.
	**스트림 키 예시: **
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
참고 이미지:
![](https://main.qcloudimg.com/raw/2ecd72b3b97389a1f40941d04760119e.png)     

[](id:play)
### LEB 풀 스트림 재생
LEB SDK를 통합하여 풀 스트림 재생을 진행하는 자세한 내용은 [LEB 풀 스트림](https://intl.cloud.tencent.com/document/product/1071/41875)을 참고하십시오.

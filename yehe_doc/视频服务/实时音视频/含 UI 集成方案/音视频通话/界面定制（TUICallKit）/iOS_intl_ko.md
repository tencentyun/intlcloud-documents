본문은 TUICallKit의 UI를 사용자 정의하는 방법을 설명하고 사용자 정의를 위한 두 가지 방식을 제공합니다: **UI 세밀 조정** 및 **사용자 정의 UI 구현**.

## 방법1: UI 세밀 조정

[Github](https://github.com/tencentyun/TUICalling)의 'iOS/TUICallKit' 폴더에서 UI 소스 코드를 직접 수정하여 TUICallKit의 UI를 조정할 수 있습니다.

**아이콘 교체:** `Resources\Calling.xcassets` 폴더의 아이콘을 직접 교체하여 app에 있는 모든 아이콘의 색조와 스타일을 사용자 지정할 수 있습니다. 아이콘을 바꿀 때 파일 이름이 원래 아이콘과 동일한지 확인하십시오.

![img](https://qcloudimg.tencent-cloud.cn/image/document/f2c76a093afce40a97a8d1d5ff281fef.png)


**벨소리 교체:** `Resources\AudioFile` 폴더에 있는 3개의 오디오 파일을 교체하여 벨소리를 교체할 수 있습니다.

| 파일명             | 설명             |
| ------------------ | ---------------- |
| phone_dialing.m4a  | 전화를 거는 소리 |
| phone_hangup.mp3   | 전화 끊어지는 소리     |
| phone_ringing.flac | 수신 전화의 벨소리 |

**텍스트 바꾸기:** zh-Hans.lproj 및 en.lproj의 `CallingLocalized.strings` 파일을 수정하여 화상 통화 UI에서 문자열을 수정할 수 있습니다.

## 방법2: 사용자 정의 UI 구현

TUICallKit의 전체 호출 기능은 UI가 없는 컴포넌트 TUICallEngine을 기반으로 구현됩니다. tuicallkit 폴더를 삭제하고 전적으로 TUICallEngine을 기반으로 고유한 UI를 구현할 수 있습니다.

### TUICallEngine

TUICallEngine은 전체 TUICallKit 컴포넌트의 기본 API입니다. 일대일 음성/영상 및 그룹 통화 걸기, 받기, 거절하기, 끊기 및 기기 작업 등 주요 API를 제공합니다.

| API                                                          | 설명                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51012#createinstance) | TUICallEngine 인스턴스 생성(싱글톤)                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51012#destroyinstance) | TUICallEngine 인스턴스(싱글톤) 종료                         |
| [init](https://www.tencentcloud.com/document/product/647/51012#init) | 기본적인 음성/영상 통화 기능 인증 완료                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51012#addobserver) | 이벤트 리스너 등록                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51012#removeobserver) | 이벤트 리스너 등록 취소                                                |
| [call](https://www.tencentcloud.com/document/product/647/51012#call) | 1v1 통화 걸기                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51012#groupcall) | 그룹 통화 걸기                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51012#accept) | 통화 하기                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51012#reject) | 통화를 거부함                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51012#hangup) | 전화를 끊음                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51012#ignore) | 호출 무시                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51012#inviteuser) | 그룹 통화 중에 사용자 초대                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51012#joiningroupcall) | 현재 그룹 통화 참가                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51012#switchcallmediatype) | 영상 통화에서 음성 통화로 통화 미디어 유형 전환                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51012#startremoteview) | 원격 사용자의 비디오 스트림 구독                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51012#stopremotereview) | 원격 사용자의 비디오 스트림 구독 취소                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51012#opencamera) | 카메라 활성화                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51012#closecamera) | 카메라 비활성화                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51012#switchcamera) | 전면 및 후면 카메라 간 전환                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51012#openmicrophone) | 마이크 활성화                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51012#closemicrophone) | 마이크 비활성화                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51012#selectaudioplaybackdevice) | 오디오 재생 장치(수신기/스피커) 선택                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51012#setselfinfo) | 사용자 닉네임과 프로필 사진 설정                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51012#enablemultideviceability) | TUICallEngine의 다중 장치 로그인 모드를 활성화/비활성화(프리미엄 플랜에서 지원) |

### TUICallObserver

TUICallObserver는 TUICallEngine의 콜백 이벤트 클래스입니다. 이를 사용하여 원하는 콜백 이벤트를 수신할 수 있습니다.

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51013#onerror) | 통화 중 오류 발생           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51013#oncallreceived) | 통화가 수신됨               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51013#oncallcancelled) | 통화가 취소됨               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51013#oncallbegin) | 통화가 연결됨               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51013#oncallend) | 통화가 종료됨               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51013#oncallmediatypechanged) | 통화 미디어 유형이 변경됨 |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51013#onuserreject) | xxxx 사용자가 통화를 거부함      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51013#onusernoresponse) | xxxx 사용자가 응답하지 않음        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51013#onuserlinebusy) | xxxx 사용자가 통화 중임          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51013#onuserjoin) | xxxx 사용자가 통화에 참여함      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51013#onuserleave) | xxxx 사용자가 통화를 종료함      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51013#onuservideoavailable) | xxx 사용자에게 비디오 스트림이 있는지 여부   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51013#onuseraudioavailable) | xxx 사용자에게 오디오 스트림이 있는지 여부   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51013#onuservoicevolumechanged) | 모든 사용자의 볼륨 수준   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51013#onusernetworkqualitychanged) | 모든 사용자의 네트워크 품질   |

### 주요 클래스의 정의

| API                    | 설명                                         |
| ---------------------- | -------------------------------------------- |
| TUICallMediaType       | 통화 미디어 유형. 열거: 영상 통화 및 음성 통화 |
| TUICallRole            | 통화 역할. 열거: 호출자 및 호출 수신자             |
| TUICallStatus          | 통화 상태. 열거: 유휴, 대기 및 응답 중   |
| TUIRoomId              | 오디오/비디오 방 ID. 숫자 또는 문자열      |
| TUICallCamera          | 카메라 유형. 열거: 전면 카메라 및 후면 카메라         |
| TUIAudioPlaybackDevice | 오디오 재생 장치 유형. 열거: 스피커 및 수신기       |
| TUINetworkQualityInfo  | 현재 네트워크 품질에 대한 정보                           |
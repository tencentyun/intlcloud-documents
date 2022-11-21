## TUICallKit (UI 포함)

TUICallKit은 **UI 요소를 포함**하는 음성/영상 통화 컴포넌트입니다. API를 사용하여 WeChat과 유사한 음성/영상 통화 애플리케이션을 빠르게 구현할 수 있습니다.

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51011#createinstance) | TUICallKit 인스턴스 생성(싱글톤 모드) |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51011#setselfinfo) | 사용자 대화명과 프로필 사진 설정             |
| [call](https://www.tencentcloud.com/document/product/647/51011#call) | 1v1 통화 호출                    |
| [groupCall](https://www.tencentcloud.com/document/product/647/51011#groupcall) | 그룹 통화를 함                     |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51011#joiningroupcall) | 그룹 통화에 참여함         |
| [setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell) | 벨소리를 설정함               |
| [enableMuteMode](https://www.tencentcloud.com/document/product/647/51011#enablemutemode) | 음소거 모드 활성화 여부를 설정함                |
| [enableFloatWindow](https://www.tencentcloud.com/document/product/647/51011#enablefloatwindow) | 플로팅 창 활성화 여부를 설정함              |

## TUICallEngine (UI 없음)

TUICallEngine은 **UI 요소를 포함하지 않는** 오디오/비디오 통화 컴포넌트입니다. TUICallKit이 요구 사항을 충족하지 않는 경우 TUICallEngine의 API를 사용하여 프로젝트를 사용자 정의할 수 있습니다.

| API                                                          | 설명                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51012#createinstance) | TUICallEngine 인스턴스 생성(싱글톤 모드)                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51012#destroyinstance) | TUICallEngine 인스턴스 종료(싱글톤)                         |
| [init](https://www.tencentcloud.com/document/product/647/51012#init) | 기본 음성/영상 통화 기능 인증                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51012#addobserver) | 이벤트 리스너 등록                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51012#removeobserver) | 이벤트 리스너 등록 취소                                                |
| [call](https://www.tencentcloud.com/document/product/647/51012#call) | 1v1 전화 걸기                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51012#groupcall) | 그룹 통화 하기                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51012#accept) | 통화에 응답                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51012#reject) | 통화 거절                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51012#hangup) | 통화 종료                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51012#ignore) | 통화 무시                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51012#inviteuser) | 현재 그룹 통화에 사용자 초대                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51012#joiningroupcall) | 그룹 통화에 참여                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51012#switchcallmediatype) | 영상 통화에서 음성 통화로의 통화 유형 변경                    |
| [setRenderView](https://www.tencentcloud.com/document/product/647/51012#setrenderview) | 비디오를 표시하도록 View 객체 설정                                |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51012#startremoteview) | 비디오를 표시하도록 View 객체 설정                                |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51012#stopremoteview) | 원격 사용자의 비디오 스트림 구독 취소                                |
| [openCamera](https://www.tencentcloud.com/document/product/647/51012#opencamera) | 카메라 켬                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51012#closecamera) | 카메라 끔                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51012#switchcamera) | 전면 및 후면 카메라 전환                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51012#openmicrophone) | 마이크 활성화                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51012#closemicrophone) | 마이크 비활성화                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51012#selectaudioplaybackdevice) | 오디오 재생 장치 선택(핸드셋/핸즈프리)                               |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51012#setselfinfo) | 대화명 및 프로필 사진 설정                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51012#enablemultideviceability) | TUICallEngine 에 대한 다중 장치 로그인 활성화 여부 설정(프리미엄 패키지에서 지원) |

## TUICallObserver

TUICallObserver는 TUICallEngine의 콜백 클래스입니다. 이벤트를 수신하는 데 사용할 수 있습니다.

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51013#onerror) | 통화하는 동안 오류 발생           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51013#oncallreceived) | 통화가 수신됨               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51013#oncallcancelled) | 통화가 취소됨               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51013#oncallbegin) | 통화가 연결됨               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51013#oncallend) | 통화 종료               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51013#oncallmediatypechanged) | 통화 유형이 변경됨 |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51013#onuserreject) | xxxx 사용자가 통화를 거부함      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51013#onusernoresponse) | xxxx 사용자가 응답하지 않음        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51013#onuserlinebusy) | xxxx 사용자가 통화 중          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51013#onuserjoin) | xxxx 사용자가 통화에 참여함      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51013#onuserleave) | xxxx 사용자가 통화를 종료함      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51013#onuservideoavailable) | xxx 사용자가 비디오 스트림을 가지고 있는지 여부   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51013#onuseraudioavailable) | xxx 사용자에게 오디오 스트림이 있는지 여부   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51013#onuservoicevolumechanged) | 모든 사용자의 볼륨 수준   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51013#onusernetworkqualitychanged) | 모든 사용자의 네트워크 품질   |

## 주요 클래스의 정의

| API                    | 설명                                         |
| ---------------------- | -------------------------------------------- |
| TUICallMediaType       | 통화 유형. 열거: 영상 통화 및 음성 통화 |
| TUICallRole            | 통화 역할. 열거: 호출자 및 호출 수신자             |
| TUICallStatus          | 통화 상태. 열거: 유휴, 대기 중 및 응답 중   |
| TUIRoomId              | 방 Id. 숫자 또는 문자열       |
| TUICallCamera          | 카메라 유형. 열거: 전면 카메라 및 후면 카메라           |
| TUIAudioPlaybackDevice | 오디오 재생 장치 유형. 열거: 스피커 및 수신기       |
| TUINetworkQualityInfo  | 현재 네트워크 품질                           |
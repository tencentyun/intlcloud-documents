## TUICallKit (UI 포함)

TUICallKit은 **UI 요소를 포함**하는 음성/영상 통화 컴포넌트입니다. API를 사용하여 WeChat과 유사한 음성/영상 통화 애플리케이션을 빠르게 구현할 수 있습니다.

| API                                             | 설명                                                         |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51005#createinstance) | TUICallKit 인스턴스 생성(싱글톤 모드) |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51005#setselfinfo) | 사용자 대화명과 프로필 사진 설정             |
| [call](https://www.tencentcloud.com/document/product/647/51005#call) | 1v1 통화 호출                    |
| [groupCall](https://www.tencentcloud.com/document/product/647/51005#groupcall) | 그룹 통화 호출                     |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51005#joiningroupcall) | 그룹 통화 참여         |
| [setCallingBell](https://www.tencentcloud.com/document/product/647/51005#setcallingbell) | 벨소리 설정               |
| [enableMuteMode](https://www.tencentcloud.com/document/product/647/51005#enablemutemode) | 음소거 모드 활성화 여부 설정                |
| [enableFloatWindow](https://www.tencentcloud.com/document/product/647/51005#enablefloatwindow) | 플로팅 창 활성화 여부 설정              |

## TUICallEngine (UI 없음)

TUICallEngine은 **UI 요소를 포함하지 않는** 오디오/비디오 통화 컴포넌트입니다. TUICallKit이 요구 사항을 충족하지 않는 경우 TUICallEngine의 API를 사용하여 프로젝트를 사용자 정의할 수 있습니다.

| API                                                          | 설명                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51006#createinstance) | TUICallEngine 인스턴스 생성(싱글톤 모드)                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51006#destroyinstance) | TUICallEngine 인스턴스 종료(싱글톤 모드)                         |
| [init](https://www.tencentcloud.com/document/product/647/51006#init) | 기본 음성/영상 통화 기능 인증                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51006#addobserver) | 이벤트 리스너 등록                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51006#removeobserver) | 이벤트 리스너 등록 취소                                                |
| [call](https://www.tencentcloud.com/document/product/647/51006#call) | 1v1 통화 호출                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51006#groupcall) | 그룹 통화 호출                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51006#accept) | 통화 수신                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51006#reject) | 통화 거절                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51006#hangup) | 통화 종료                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51006#ignore) | 통화 무시                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51006#inviteuser) | 현재 그룹 통화에 사용자 초대                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51006#joiningroupcall) | 그룹 통화에 참여                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51006#switchcallmediatype) | 화상 통화에서 음성 통화로 통화 미디어 유형 전환                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51006#startremoteview) | 원격 사용자의 비디오 스트림 구독                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51006#stopremoteview) | 원격 사용자의 비디오 스트림 구독 취소                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51006#opencamera) | 카메라를 켬                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51006#closecamera) | 카메라 끔                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51006#switchcamera) | 전면 및 후면 카메라 간 전환                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51006#openmicrophone) | 마이크 활성화                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51006#closemicrophone) | 마이크 비활성화                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51006#selectaudioplaybackdevice) | 오디오 재생 장치(수신기/스피커) 선택                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51006#setselfinfo) | 사용자 대화명과 프로필 사진 설정                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51006#enablemultideviceability) | TUICallEngine에 대한 다중 장치 로그인 활성화 여부 설정(프리미엄 패키지에서 지원) |

## TUICallObserver

TUICallObserver는 TUICallEngine의 콜백 클래스입니다. 이벤트를 수신하는 데 사용할 수 있습니다.

| API                                                          | 설명                       |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51007#onerror) | 통화 중 오류 발생           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51007#oncallreceived) | 통화 수신               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51007#oncallcancelled) | 통화 취소               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51007#oncallbegin) | 통화 연결               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51007#oncallend) | 통화 종료               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51007#oncallmediatypechanged) | 통화 유형 변경 |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51007#onuserreject) | xxxx 사용자가 통화를 거부함      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51007#onusernoresponse) | xxxx 사용자가 응답하지 않음        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51007#onuserlinebusy) | xxxx 사용자가 통화 중          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51007#onuserjoin) | xxxx 사용자가 통화에 참여함      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51007#onuserleave) | xxxx 사용자가 통화를 종료함      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51007#onuservideoavailable) | xxx 사용자에게 비디오 스트림이 있는지 여부   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51007#onuseraudioavailable) | xxx 사용자에게 오디오 스트림이 있는지 여부   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51007#onuservoicevolumechanged) | 모든 사용자의 볼륨 수준   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51007#onusernetworkqualitychanged) | 모든 사용자의 네트워크 품질   |

## 주요 클래스의 정의

| API                                 | 설명                                         |
| ----------------------------------- | -------------------------------------------- |
| TUICallDefine.MediaType             | 통화 유형, 열거: 영상 통화 및 음성 통화 |
| TUICallDefine.Role                  | 통화 역할, 열거: 호출자 및 호출 수신자             |
| TUICallDefine.Status                | 통화 상태, 열거: 유휴, 대기 및 응답 중   |
| TUICommonDefine.RoomId              | 오디오/비디오 방 Id, 숫자 또는 문자열       |
| TUICommonDefine.Camera              | 카메라 유형, 열거: 전면 카메라 및 후면 카메라           |
| TUICommonDefine.AudioPlaybackDevice | 오디오 재생 장치 유형, 열거: 스피커 및 수신기       |
| TUICommonDefine.NetworkQualityInfo  | 현재 네트워크 품질                           |
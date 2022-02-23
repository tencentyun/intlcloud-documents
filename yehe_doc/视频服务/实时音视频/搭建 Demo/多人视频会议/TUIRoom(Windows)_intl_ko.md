TUIRoom은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM)을 기반으로 하며, 다음 기능을 지원합니다.
- 호스트가 방을 생성하고 참석자가 방 번호를 입력한 후 참여.
- 참석자 간 화면 공유.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 발송 지원.

TUIRoom은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [그룹 멀티미디어 룸(Windows and macOS)](https://intl.cloud.tencent.com/document/product/647/44071)을 참고하십시오.
- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 사용하는 저지연 화상 회의 컴포넌트입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 채팅방 기능을 구현합니다(**IM SDK는 C++ 버전 사용**).


## TUIRoom API 개요[](id:TUIRoom)

### TUIRoomCore 기본 함수

| API                                 | 설명           |
|-----|-----|
| [GetInstance](#getinstance)         | 싱글톤 객체 가져오기. |
| [DestroyInstance](#destroyinstance) | 싱글톤 객체 폐기. |
| [SetCallback](#setcallback)         | 이벤트 콜백 설정. |

### 방 관련 API

| API      | 설명   |
|-----|-----|
| [login](#login)                           | 로그인.                             |
| [logout](#logout)                         | 로그아웃.                             |
| [CreateRoom](#createroom)                 | 방 생성(호스트 호출).           |
| [DestroyRoom](#destroyroom)               | 방 폐기(호스트 호출).           |
| [EnterRoom](#enterroom)                   | 방 입장(참석자 호출).         |
| [LeaveRoom](#leaveroom)                   | 방 퇴장(참석자 또는 호스트 호출). |
| [GetRoomInfo](#getroominfo)               | 방 정보 가져오기.                     |
| [GetRoomUsers](#getroomusers)             | 방에 있는 모든 참석자 정보 가져오기.           |
| [GetUserInfo](#getuserinfo)               | 특정 사용자 정보 가져오기.               |
| [TransferRoomMaster](#transferroommaster) | 호스트 권한 이전(호스트 호출).     |

### 로컬 멀티미디어 작업 인터페이스

| API                                                   | 설명                       |
|-----|-----|
| [StartCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작.|
| [StopCameraPreview](#stopcamerapreview) | 로컬 비디오 수집 및 미리보기 중지.|
| [UpdateCameraPreview](#updatecamerapreview)           | 로컬 비디오 렌더링 창 변경.     |
| [StartLocalAudio](#startlocalaudio)                   | 마이크 수집 활성화.            |
| [StopLocalAudio](#stoplocalaudio)                     | 마이크 수집 정지.           |
| [StartSystemAudioLoopback](#startsystemaudioloopback) | 시스템 사운드 수집 활성화/비활성화.  |
| [StopSystemAudioLoopback](#stopsystemaudioloopback)   | 시스템 사운드 수집 활성화/비활성화.  |
| [SetVideoMirror](#setvideomirror)                     | 로컬 화면 이미지 미리보기 모드 설정. |

### 원격 사용자 관련 인터페이스

| API                                   | 설명                               |
|-----|-----|
| [StartRemoteView](#startremoteview)   | 지정된 참석자의 원격 비디오 화면 구독 및 재생. |
| [StopRemoteView](#stopremoteview)     | 구독 취소 및 원격 비디오 화면 재생 중지.   |
| [UpdateRemoteView](#updateremoteview) | 원격 사용자의 비디오 렌더링 창 변경.       |

### 채팅 메시지 발송 인터페이스

| API                                     | 설명             |
|-----|-----|
| [SendChatMessage](#sendchatmessage)     | 채팅 메시지 발송.   |
| [SendCustomMessage](#sendcustommessage) | 사용자 정의 메시지 발송. |

### 필드 제어 관련 인터페이스

| API                                                 | 설명                                                    |
|-----|-----|
| [MuteUserMicrophone](#muteusermicrophone)           | 사용자의 마이크 비활성화/복구.                               |
| [MuteAllUsersMicrophone](#muteallusersmicrophone)   | 모든 사용자의 마이크 비활성화/복원, 상태를 회의실 정보에 동기화. |
| [MuteUserCamera](#muteusercamera)                   | 사용자 카메라 비활성화/복원.                               |
| [MuteAllUsersCamera](#mutealluserscamera)           | 모든 사용자의 카메라 비활성화/복원, 상태를 방 정보에 동기화. |
| [MuteChatRoom](#mutechatroom)                       | 채팅방 음소거 활성화/비활성화(호스트 호출).                     |
| [KickOffUser](#kickoffuser)                         | 방에서 특정인 강제 퇴장(호스트 호출).                        |
| [StartCallingRoll](#startcallingroll)               | 호스트 통화 시작.                                        |
| [StopCallingRoll](#stopcallingroll)                 | 호스트 지명 종료.                                        |
| [ReplyCallingRoll](#replycallingroll)               | 참석자가 호스트의 지명에 응답.                                    |
| [SendSpeechInvitation](#sendspeechinvitation)       | 호스트의 참석자 발언 초대.                                    |
| [CancelSpeechInvitation](#cancelspeechinvitation)   | 호스트의 참석자 발언 초대 취소.                                |
| [ReplySpeechInvitation](#replyspeechinvitation)     | 참석자가 호스트의 발언 요청 동의/거절.                         |
| [SendSpeechApplication](#sendspeechapplication)     | 참석자 발언 신청.                                          |
| [CancelSpeechApplication](#cancelspeechapplication) | 참석자 발언 신청 취소.                                      |
| [ReplySpeechApplication](#replyspeechapplication)   | 호스트의 참석자 발언 신청 동의/거부.                         |
| [ForbidSpeechApplication](#forbidspeechapplication) | 호스트의 발언 신청 금지.                                    |
| [SendOffSpeaker](#sendoffspeaker)                   | 호스트의 참석자 발언 금지.                                  |
| [SendOffAllSpeakers](#sendoffallspeakers)           | 호스트의 전원 발언 금지.                                  |
| [ExitSpeechState](#exitspeechstate)                 | 참석자 발언 중지, 시청자로 전환.                               |

### 기본 컴포넌트 인터페이스 함수

| API                                             | 설명                                       |
|-----|-----|
| [GetDeviceManager](#getdevicemanager)           | 로컬 설정 관리 객체 ITXDeviceManager 가져오기.    |
| [GetScreenShareManager](#getscreensharemanager) | 화면 공유 관리 객체 IScreenShareManager 가져오기. |

### 클라우드 녹화 인터페이스 함수

| API                                   | 설명          |
|-----|-----|
| [StartCloudRecord](#startcloudrecord) | 클라우드 녹화 시작. |
| [StopCloudRecord](#stopcloudrecord)   | 클라우드 녹화 중지. |

### 뷰티 필터 관련 인터페이스 함수

| API      | 설명   |
|-----|-----|
| [SetBeautyStyle](#setbeautystyle) | 뷰티필터 설정.|

### 관련 설정 인터페이스

| API      | 설명   |
|-----|-----|
| [SetVideoQosPreference](#setvideoqospreference) | 네트워크 트래픽 제어 관련 매개변수 설정.|

### SDK 버전 인터페이스 함수 가져오기

| API      | 설명   |
|-----|-----|
| [GetSDKVersion](#getsdkversion) | SDK 버전 가져오기.|

## TUIRoomCoreCallback API 개요[](id:TUIRoomCoreCallback)

### 오류 이벤트 콜백

| API      | 설명   |
|-----|-----|
| [OnError](#OnError) | 오류 콜백.|

### 기본 이벤트 콜백

| API                                         | 설명               |
|-----|-----|
| [OnLogin](#onlogin)                         | 로그인 콜백.         |
| [OnLogout](#onlogout)                       | 로그아웃 콜백.         |
| [OnCreateRoom](#oncreateroom)               | 방 생성 콜백.     |
| [OnDestroyRoom](#ondestroyroom)             | 방 해산 콜백.     |
| [OnEnterRoom](#onenterroom)                 | 방 입장 콜백.     |
| [OnExitRoom](#onexitroom)                   | 방 퇴장 콜백.     |
| [OnFirstVideoFrame](#onfirstvideoframe)     | 첫 번째 화면 콜백.     |
| [OnUserVoiceVolume](#onuservoicevolume)     | 볼륨 크기 콜백 콜백. |
| [OnRoomMasterChanged](#onroommasterchanged) | 호스트 변경 콜백.   |

### 원격 사용자 이벤트 콜백

| API                                             | 설명                                                         |
|-----|-----|
| [OnRemoteUserEnter](#onremoteuserenter)                      | 원격 사용자 방 입장 콜백.           |
| [OnRemoteUserLeave](#onremoteuserleave)                      | 원격 사용자 방 퇴장 콜백.           |
| [OnRemoteUserCameraAvailable](#onremoteusercameraavailable)  | 원격 사용자 카메라 활성화 여부 콜백. |
| [OnRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | 원격 사용자 화면 공유 활성화 여부 콜백.   |
| [OnRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | 원격 사용자의 오디오 업스트림 활성화 여부 콜백.   |
| [OnRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | 원격 사용자 발언 시작 콜백.           |
| [OnRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | 원격 사용자가 발언 종료 콜백.           |

### 메시지 이벤트 콜백

| API                                               | 설명               |
|-----|-----|
| [OnReceiveChatMessage](#onreceivechatmessage)     | 텍스트 메시지 수신 콜백. |
| [OnReceiveCustomMessage](#onreceivecustommessage) | 텍스트 메시지 수신 콜백. |

### 필드 제어 이벤트 콜백

| API                                             | 설명                                                         |
|-----|-----|
| [OnReceiveSpeechInvitation](#onreceivespeechinvitation)      | 사용자가 호스트의 발언 초대 수신 콜백.       |
| [OnReceiveInvitationCancelled](#onreceiveinvitationcancelled) | 사용자가 호스트의 발언 초대 취소 수신 콜백.   |
| [OnReceiveReplyToSpeechInvitation](#onreceivereplytospeechinvitation) | 호스트가 사용자의 발언 초대 동의 수신 콜백. |
| [OnReceiveSpeechApplication](#onreceivespeechapplication)    | 호스트가 사용자의 발언 요청 수신 콜백.     |
| [OnSpeechApplicationCancelled](#onspeechapplicationcancelled) | 사용자의 발언 신청 취소 콜백.             |
| [OnReceiveReplyToSpeechApplication](#onreceivereplytospeechapplication) | 호스트는 발언 신청 동의 콜백.           |
| [OnSpeechApplicationForbidden](#onspeechapplicationforbidden) | 사회자 발언 신청 금지 콜백.           |
| [OnOrderedToExitSpeechkState](#onorderedtoexitspeechkstate)  | 참석자가 발언 중단 요청 수신 콜백.         |
| [OnCallingRollStarted](#oncallingrollstarted)                | 호스트 지명 시작 시 참석자가 수신하는 콜백.   |
| [OnCallingRollStopped](#oncallingrollstopped)                | 호스트 지명 종료 시 참석자가 수신하는 콜백.   |
| [OnMemberReplyCallingRoll](#onmemberreplycallingroll)        | 참석자의 지명 응답 시 호스트가 수신하는 콜백.   |
| [OnChatRoomMuted](#onchatroommuted)                          | 호스트의 채팅방 음소거 상태 변경 콜백.     |
| [OnMicrophoneMuted](#onmicrophonemuted)                      | 호스트의 마이크 비활성화 설정 콜백.         |
| [OnCameraMuted](#oncameramuted)                              | 호스트의 카메라 비활성화 설정 콜백.         |

### 통계 및 품질 콜백

| API      | 설명   |
|-----|-----|
| [OnStatistics](#onstatistics)         | 기술 지표 통계 콜백. |
| [OnNetworkQuality](#onnetworkquality) | 네트워크 품질 콜백.     |

### 화면 공유 관련 콜백

| API                                               | 설명               |
|-----|-----|
| [OnScreenCaptureStarted](#onscreencapturestarted) | 화면 공유 콜백 시작. |
| [OnScreenCaptureStopped](#onscreencapturestopped) | 화면 공유 콜백 중지. |

### 비디오 녹화 콜백

| API                                   | 설명           |
|-----|-----|
| [OnRecordError](#onrecorderror)       | 녹화 오류 콜백. |
| [OnRecordComplete](#onrecordcomplete) | 녹화 완료 콜백. |
| [OnRecordProgress](#onrecordprogress) | 녹화 진행률 콜백. |


### 로컬 장치 테스트 콜백

| API                                                          | 설명                  |
|-----|-----|
| [OnTestSpeakerVolume](#ontestspeakervolume)                  | 스피커 볼륨 콜백.       |
| [OnTestMicrophoneVolume](#ontestmicrophonevolume)            | 마이크 볼륨 콜백.       |
| [OnAudioDeviceCaptureVolumeChanged](#onaudiodevicecapturevolumechanged) | 시스템 수집 볼륨 조정 콜백. |
| [OnAudioDevicePlayoutVolumeChanged](#onaudiodeviceplayoutvolumechanged) | 시스템 재생 볼륨 조정 콜백. |

## TUIRoomCore 기본 함수

### GetInstance

[TUIRoomCore](https://cloud.tencent.com/document/product/647/63494) 싱글톤 객체 가져오기.
```C++
 static TUIRoomCore* GetInstance();
```

### DestroyInstance

```C++
static void DestroyInstance();
```

### SetCallback

[TUIRoomCore](https://cloud.tencent.com/document/product/647/63494) 이벤트 콜백. TUIRoomCoreCallback을 통해 [TUIRoomCore](https://cloud.tencent.com/document/product/647/63494) 에서 다양한 상태 알림을 받을 수 있습니다.

```C++
virtual void SetCallback(const TUIRoomCoreCallback* callback) = 0;
```

### Login

로그인합니다.
```C++
virtual int Login(int sdk_appid, const std::string& user_id, const std::string& user_sig) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| sdk_appid | int |  TRTC 콘솔 > **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**> 애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| user_id | string | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| user_sig | string | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |

### Logout

로그아웃합니다.
```C++
virtual int Logout() = 0;
```

### CreateRoom

방을 생성합니다(호스트 호출).
```C++
virtual int CreateRoom(const std::string& room_id, TUISpeechMode speech_mode) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| room_id | string | 방 식별 번호이며, 귀하가 직접 할당하고 통합 관리합니다. |
| speech_mode | TUISpeechMode | 발언 모드. |

호스트 정상 호출 프로세스는 다음과 같습니다.
1. **호스트**는 'CreateRoom()'을 호출하여 방을 만들고, 방 생성 성공 여부는 OnCreateRoom을 통해 호스트에게 공지됩니다.
2. **호스트**는 'EnterRoom()'을 호출하여 방에 입장합니다.
3. **호스트**는 'StartCameraPreview()'를 호출하여 카메라 캡처 및 미리보기를 시작합니다.
4. **호스트**는 'StartLocalAudio()'를 호출하여 로컬 마이크를 켭니다.

### DestroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.
```C++
virtual int DestroyRoom() = 0;
```

### EnterRoom

방에 입장합니다(참석자 호출).
```C++
virtual int EnterRoom(const std::string& room_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| room_id | string | 방 식별 번호. |

참석자의 방 입장 정상 호출 프로세스는 다음과 같습니다.
1. **참석자**는 'EnterRoom'을 호출하고 room_id를 입력하여 방에 입장합니다.
2. **참석자**는 `startCameraPreview()`를 호출하여 카메라 미리보기를 열고 `StartLocalAudio()`를 호출하여 마이크 수집을 시작합니다.
3. **참석자**는 `OnRemoteUserCameraAvailable` 이벤트를 수신하고 `StartRemoteView()`를 호출하여 비디오 재생을 시작합니다.

### LeaveRoom

방에서 퇴장합니다(참석자 호출).
```C++
virtual int LeaveRoom() = 0;
```

### GetRoomInfo

방 정보 가져오기.
```C++
virtual TUIRoomInfo GetRoomInfo() = 0;
```

### GetRoomUsers

방의 모든 구성원에 대한 정보를 가져옵니다.
```C++
virtual std::vector<TUIUserInfo> GetRoomUsers() = 0;
```

### GetUserInfo

방 참석자 정보를 가져옵니다.
```C++
virtual const TUIUserInfo* GetUserInfo(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 표식. |

### SetSelfProfile

사용자 속성을 설정합니다.
```C++
virtual int SetSelfProfile(const std::string& user_name, const std::string& avatar_url) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| user_name | string | 사용자 이름. |
| avatar_url | string | 사용자 프로필 URL. |

### TransferRoomMaster

그룹을 다른 사용자에게 이전합니다.
```C++
virtual int TransferRoomMaster(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 표식. |

## 로컬 푸시 스트림 인터페이스

### StartCameraPreview

로컬 카메라 미리보기를 시작합니다.
```C++
virtual int StartCameraPreview(const liteav::TXView& view) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| view | liteav::TXView | 창 핸들. |

### StopCameraPreview

로컬 카메라 미리보기를 중지합니다.
```C++
virtual int StopCameraPreview() = 0;
```

### UpdateCameraPreview

로컬 비디오 미리보기 화면의 창을 업데이트합니다.
```C++
virtual int UpdateCameraPreview(const liteav::TXView& view) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| view | liteav::TXView | 창 핸들. |

### StartLocalAudio

로컬 오디오 장치를 켭니다.
```C++
virtual int StartLocalAudio(const liteav::TRTCAudioQuality& quality) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| view | liteav::TXView | 창 핸들. |

### StopLocalAudio

로컬 오디오 장치를 끕니다.
```C++
virtual int StopLocalAudio() = 0;
```

### StartSystemAudioLoopback

시스템 사운드 수집을 활성화합니다.
```C++
virtual int StartSystemAudioLoopback() = 0;
```

### StopSystemAudioLoopback

시스템 사운드 수집을 비활성화합니다.
```C++
virtual int StopSystemAudioLoopback() = 0;
```

### SetVideoMirror

이미지를 설정합니다.
```C++
virtual int SetVideoMirror(bool mirror) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| mirror | bool | 이미지 여부. |

## 원격 사용자 관련 인터페이스

### StartRemoteView
원격 사용자의 비디오 스트림을 구독합니다.

```C++
virtual int StartRemoteView(const std::string& user_id, const liteav::TXView& view,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 재생할 사용자 ID. |
| liteav::TXView | TXView | 영상 화면을 탑재한 view 컨트롤러.|
| type | TUIStreamType | 스트림 유형.|

### StopRemoteView

구독을 취소하고 원격 영상 화면 재생을 중지합니다.
```C++
virtual int StopRemoteView(const std::string& user_id,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 재생을 중지할 사용자 ID. |
| type | TUIStreamType | 스트림 유형.|

### UpdateRemoteView

원격 비디오 렌더링 창을 업데이트합니다.
```C++
virtual int UpdateRemoteView(const std::string& user_id, TUIStreamType type, liteav::TXView& view) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| type | TUIStreamType | 스트림 유형.|
| view | liteav::TXView | 렌더링 창 핸들.|

## 메시지 인터페이스 보내기

### SendChatMessage

텍스트 메시지를 발송합니다.
```C++
virtual int SendChatMessage(const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| message | string | 메시지 내용. |

### SendCustomMessage

사용자 정의 메시지 발송.
```C++
virtual int SendCustomMessage(const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| message | string | 메시지 내용. |

## 필드 제어 관련 인터페이스

### MuteUserMicrophone

사용자의 마이크를 비활성화/복구합니다.
```C++
virtual int MuteUserMicrophone(const std::string& user_id, bool mute, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| mute | bool | 비활성화 여부. |
| callback | Callback | 인터페이스 콜백. |

### MuteAllUsersMicrophone

모든 사용자의 마이크를 비활성화/복구합니다.
```C++
virtual int MuteAllUsersMicrophone(bool mute) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| mute | bool | 비활성화 여부. |

### MuteUserCamera

사용자의 카메라를 비활성화/복구합니다.
```C++
virtual int MuteUserCamera(const std::string& user_id, bool mute, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| mute | bool | 비활성화 여부. |
| callback | Callback | 인터페이스 콜백. |

### MuteAllUsersCamera

모든 사용자의 카메라를 비활성화/복구합니다.
```C++
virtual int MuteAllUsersCamera(bool mute) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| mute | bool | 비활성화 여부. |

### MuteChatRoom

채팅방 음소거를 활성화/비활성화합니다.
```C++
virtual int MuteChatRoom(bool mute) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| mute | bool | 비활성화 여부. |

### KickOffUser

호스트의 내보내기.
```C++
virtual int KickOffUser(const std::string& user_id, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| callback | Callback | 인터페이스 콜백. |

### StartCallingRoll

호스트가 지명을 시작합니다.
```C++
virtual int StartCallingRoll() = 0;
```

### StopCallingRoll

호스트가 지명을 종료합니다.
```C++
virtual int StopCallingRoll() = 0;
```

### ReplyCallingRoll

참석자가 호스트의 지명에 응답합니다.
```C++
virtual int ReplyCallingRoll(Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| callback | Callback | 인터페이스 콜백. |

### SendSpeechInvitation

호스트가 참석자에게 발언 초대합니다.
```C++
virtual int SendSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| callback | Callback | 인터페이스 콜백. |

### CancelSpeechInvitation

호스트가 참석자의 발언 초대를 취소합니다.
```C++
virtual int CancelSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| callback | Callback | 인터페이스 콜백. |

### ReplySpeechInvitation

참석자는 호스트의 발언 초대에 동의/거절합니다.
```C++
virtual int ReplySpeechInvitation(bool agree, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| agree | bool | 동의 여부. |
| callback | Callback | 인터페이스 콜백. |

### SendSpeechApplication

참석자가 발언을 신청합니다.
```C++
virtual int SendSpeechApplication(Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| callback | Callback | 인터페이스 콜백. |

### CancelSpeechApplication

참석자가 발언 신청을 취소합니다.
```C++
virtual int CancelSpeechApplication(Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| callback | Callback | 인터페이스 콜백. |

### ReplySpeechApplication

호스트가 참석자의 발언 신청에 동의/거부합니다.
```C++
virtual int ReplySpeechApplication(const std::string& user_id, bool agree, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| callback | Callback | 인터페이스 콜백. |

### ForbidSpeechApplication

호스트가 발언 신청을 금지합니다.
```C++
virtual int ForbidSpeechApplication(bool forbid) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| forbid | bool | 금지 여부. |

### SendOffSpeaker

호스트가 참석자 발언을 금지합니다.
```C++
virtual int SendOffSpeaker(const std::string& user_id, Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| callback | Callback | 인터페이스 콜백. |

### SendOffAllSpeakers

호스트가 모든 참석자의 발언을 금지합니다.
```C++
virtual int SendOffAllSpeakers(Callback callback) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| callback | Callback | 인터페이스 콜백. |

### ExitSpeechState

참석자는 발언을 중지하고 시청자로 전환합니다.
```C++
virtual int ExitSpeechState() = 0;
```

## 기본 컴포넌트 인터페이스

### GetDeviceManager

장치 관리 객체 포인터를 가져옵니다.
```C++
virtual liteav::ITXDeviceManager* GetDeviceManager() = 0;
```

### GetScreenShareManager

화면 공유 관리 객체 포인터를 가져옵니다.
```C++
virtual IScreenShareManager* GetScreenShareManager() = 0;
```

## 클라우드 녹화 인터페이스

### StartCloudRecord

클라우드 녹화를 시작합니다.
```C++
virtual int StartCloudRecord() = 0;
```

### StopCloudRecord

클라우드 녹화를 중지합니다.
```C++
virtual int StopCloudRecord() = 0;
```

## 뷰티 필터 관련 인터페이스 함수

### SetBeautyStyle

뷰티 필터, 미백, 안색 보정 효과 단계 설정.
```C++
virtual int SetBeautyStyle(liteav::TRTCBeautyStyle style, uint32_t beauty_level,
        uint32_t whiteness_level, uint32_t ruddiness_level) = 0;
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
- ‘뷰티필터 스타일’을 설정하면 매끄럽거나 자연스럽고 매끄러운 스타일의 미세 피부 보정 효과가 더 분명합니다.
- ‘뷰티필터 레벨’은 0 - 9 레벨로 나뉘며, 0은 효과 없음, 1 - 9는 숫자가 커질수록 효과가 더 뚜렷합니다.
- ‘미백 레벨’은 0 - 9레벨로 나뉘며, 0은 효과 없음, 1 - 9는 숫자가 커질수록 효과가 더 뚜렷합니다.

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| style | liteav::TRTCBeautyStyle | 뷰티필터 스타일. |
| beauty_level | uint32_t | 뷰티필터 레벨. |
| whiteness_level | uint32_t | 미백 레벨. |
| ruddiness_level | uint32_t | 안색 보정 레벨. |

## 관련 설정 인터페이스

### SetVideoQosPreference

네트워크 트래픽 제어와 관련된 매개변수를 설정합니다.
```C++
virtual int SetVideoQosPreference(TUIVideoQosPreference preference) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| preference | TUIVideoQosPreference | 네트워크 트래픽 제어 정책. |

## SDK 버전 인터페이스 가져오기

### GetSDKVersion

SDK 버전 정보를 가져옵니다.
```C++
virtual const char* GetSDKVersion() = 0;
```

## 오류 이벤트 콜백
### OnError

```C++
void OnError(int code, const std::string& message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 오류 정보. |

## 기본 이벤트 콜백
### OnLogin

```C++
virtual void OnLogin(int code, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 로그인 정보 또는 로그인 실패 오류 정보. |

### OnLogout

```C++
virtual void OnLogout(int code, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 오류 정보. |

### OnCreateRoom

방 생성 콜백입니다.
```C++
virtual void OnCreateRoom(int code, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 오류 정보. |

### OnDestroyRoom

방 해산 콜백입니다.
```C++
virtual void OnDestroyRoom(int code, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 오류 정보. |

### OnEnterRoom

방 입장 콜백입니다.
```C++
virtual void OnEnterRoom(int code, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| code    | int    | 오류 코드.|
| message | string | 오류 정보. |

### OnExitRoom

방 퇴장 콜백입니다.
```C++
virtual void OnExitRoom(TUIExitRoomType type, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| type | TUIExitRoomType | 방 퇴장 유형. |
| message | string | 오류 정보. |

### OnFirstVideoFrame

로컬 또는 원격 사용자의 첫 번째 화면 렌더링을 시작합니다.
```C++
virtual void OnFirstVideoFrame(const std::string& user_id, const TUIStreamType stream_type) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| stream_type | TUIStreamType | 스트림 유형. |

### OnUserVoiceVolume

사용자 볼륨 크기 콜백입니다.
```C++
virtual void OnUserVoiceVolume(const std::string& user_id, int volume)
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| volume | int | 사용자의 볼륨 크기, 범위: 0 - 100. |

### OnRoomMasterChanged

호스트 변경 콜백입니다.
```C++
virtual void OnRoomMasterChanged(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

## 원격 사용자 콜백 이벤트

### OnRemoteUserEnter

원격 사용자 방 입장 콜백입니다.
```C++
virtual void OnRemoteUserEnter(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnRemoteUserLeave

원격 사용자 방 퇴장 콜백입니다.
```C++
virtual void OnRemoteUserLeave(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnRemoteUserCameraAvailable

원격 사용자 카메라 활성화 여부입니다.
```C++
virtual void OnRemoteUserCameraAvailable(const std::string& user_id, bool available) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| available | bool | true: 동영상 스트리밍 데이터 있음, false: 동영상 스트리밍 데이터 없음. |

### OnRemoteUserScreenVideoAvailable

원격 사용자 카메라 활성화 여부입니다.
```C++
virtual void OnRemoteUserScreenVideoAvailable(const std::string& user_id, bool available) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| available | bool | true: 동영상 스트리밍 데이터 있음, false: 동영상 스트리밍 데이터 없음. |

### OnRemoteUserAudioAvailable

원격 사용자 카메라 활성화 여부입니다.
```C++
virtual void OnRemoteUserAudioAvailable(const std::string& user_id, bool available) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| available | bool | true: 동영상 스트리밍 데이터 있음, false: 동영상 스트리밍 데이터 없음. |

### OnRemoteUserEnterSpeechState

원격 사용자가 발언을 시작합니다.
```C++
virtual void OnRemoteUserEnterSpeechState(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnRemoteUserExitSpeechState

원격 사용자가 발언을 종료합니다.
```C++
virtual void OnRemoteUserExitSpeechState(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |


## 채팅방 메시지 이벤트 콜백

### OnReceiveChatMessage

텍스트 메시지를 수신합니다.
```C++
virtual void OnReceiveChatMessage(const std::string& user_id, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| message | string | 텍스트 메시지.|

### OnReceiveCustomMessage

사용자 정의 메시지를 수신합니다.
```C++
virtual void OnReceiveCustomMessage(const std::string& user_id, const std::string& message) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| message | string | 사용자 정의 메시지.|

## 필드 제어 메시지 콜백

### OnReceiveSpeechInvitation

사용자가 호스트로부터 발언 초대를 받았을 때의 콜백입니다.
```C++
virtual void OnReceiveSpeechInvitation() = 0;
```

### OnReceiveInvitationCancelled

사용자가 호스트로부터 발언 초대 취소를 받았을 때의 콜백입니다.
```C++
virtual void OnReceiveInvitationCancelled() = 0;
```

### OnReceiveReplyToSpeechInvitation

호스트가 사용자로부터 발언 초대 동의를 받았을 때의 콜백입니다.
```C++
virtual void OnReceiveReplyToSpeechInvitation(const std::string& user_id, bool agree) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |
| agree | bool | 동의 여부.|

### OnReceiveSpeechApplication

호스트가 사용자의 발언 요청를 받았을 때의 콜백입니다.
```C++
virtual void OnReceiveSpeechApplication(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnSpeechApplicationCancelled

사용자가 발언 신청을 취소하는 콜백입니다.
```C++
virtual void OnSpeechApplicationCancelled(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnReceiveReplyToSpeechApplication

사회자가 발언 신청에 동의하는 콜백입니다.
```C++
virtual void OnReceiveReplyToSpeechApplication(bool agree) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| agree | bool | 동의 여부. |

### OnSpeechApplicationForbidden

호스트가 발언 신청을 금지하는 콜백입니다.
```C++
virtual void OnSpeechApplicationForbidden(bool forbidden) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| forbidden | bool | 금지 여부. |

### OnOrderedToExitSpeechkState

참석자가 발언 중지를 요청받은 콜백입니다.
```C++
virtual void OnOrderedToExitSpeechkState() = 0;
```

### OnCallingRollStarted

호스트가 지명을 시작하면 참석자가 수신하는 콜백입니다.
```C++
virtual void OnCallingRollStarted() = 0;
```

### OnCallingRollStopped

호스트가 지명을 종료하면 참석자가 수신하는 콜백입니다.
```C++
virtual void OnCallingRollStopped() = 0;
```

### OnMemberReplyCallingRoll

참석자가 지명에 응답하면 호스트가 수신하는 콜백입니다.
```C++
virtual void OnMemberReplyCallingRoll(const std::string& user_id) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| user_id | string | 사용자 ID. |

### OnChatRoomMuted

호스트의 채팅방 음소거 여부 변경에 대한 콜백입니다.
```C++
virtual void OnChatRoomMuted(bool muted) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| muted | bool | 음소거 여부. |

### OnMicrophoneMuted

호스트의 마이크 음소거 설정에 대한 콜백입니다.
```C++
virtual void OnMicrophoneMuted(bool muted) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| muted | bool | 음소거 여부. |

### OnCameraMuted

호스트의 카메라 음소거 설정에 대한 콜백입니다.
```C++
virtual void OnCameraMuted(bool muted) = 0;
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| muted | bool | 음소거 여부. |

## 통계 및 품질 콜백

### OnStatistics

기술 지표 통계 콜백입니다.
```C++
virtual void OnStatistics(const liteav::TRTCStatistics& statis) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| statis | liteav::TRTCStatistics | 통계 데이터. |

### OnNetworkQuality

네트워크 상태 콜백입니다.
```C++
virtual void OnNetworkQuality(const liteav::TRTCQualityInfo& local_quality, liteav::TRTCQualityInfo* remote_quality,
        uint32_t remote_quality_count) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미   |
|-----|-----|-----|
| local_quality | liteav::TRTCQualityInfo | 로컬 사용자 품질 정보. |
| remote_quality | liteav::TRTCQualityInfo* | 원격 사용자 품질 정보 포인터. |
| remote_quality_count | uint32_t | 원격 사용자 수. |

## 녹화 이벤트 콜백

### OnScreenCaptureStarted

화면 공유 시작 콜백입니다.

```C++
virtual void OnScreenCaptureStarted() {}
```

### OnScreenCaptureStopped

화면 공유 중지 콜백입니다.

```C++
void OnScreenCaptureStopped(int reason) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | 중지 사유입니다. 0: 사용자가 중지, 1: 다른 애플리케이션으로 인한 강제 중지. |

## 비디오 녹화 콜백

### OnRecordError

녹화 오류 콜백입니다.

```C++
virtual void OnRecordError(TXLiteAVLocalRecordError error, const std::string& messgae) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| error | TXLiteAVLocalRecordError  | 오류 정보. |
| messgae | string  | 오류 설명. |

### OnRecordComplete

녹화 완료 콜백입니다.

```C++
virtual void OnRecordComplete(const std::string& path) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| path | string  | 오류 설명. |

### OnRecordProgress

녹화 진행률 콜백입니다.

```C++
virtual void OnRecordProgress(int duration, int file_size) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| duration | int  | 파일 길이. |
| file_size | int  | 파일 크기. |

## 로컬 디바이스 테스트 콜백

### OnTestSpeakerVolume

스피커 볼륨 크기 콜백입니다.

```C++
virtual void OnTestSpeakerVolume(uint32_t volume) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 볼륨 크기. |

### OnTestMicrophoneVolume

마이크 볼륨 크기 콜백입니다.

```C++
virtual void OnTestMicrophoneVolume(uint32_t volume) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 볼륨 크기. |

### OnAudioDeviceCaptureVolumeChanged

시스템 수집 볼륨 조정 콜백입니다.

```C++
virtual void OnAudioDeviceCaptureVolumeChanged(uint32_t volume, bool muted) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 볼륨 크기. |
| muted | bool  | 비활성화 여부. |

### OnAudioDevicePlayoutVolumeChanged

시스템 재생 볼륨 조정에 대한 콜백입니다.

```C++
virtual void OnAudioDevicePlayoutVolumeChanged(uint32_t volume, bool muted) {}
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                               |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | 볼륨 크기. |
| muted | bool  | 비활성화 여부. |

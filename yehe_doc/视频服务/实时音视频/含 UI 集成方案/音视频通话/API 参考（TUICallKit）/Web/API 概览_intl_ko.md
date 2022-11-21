## TUICallEngine (UI 없음)

TUICallEngine은 **UI 요소를 포함하지 않는** 오디오/비디오 통화 컴포넌트입니다. API를 사용하여 프로젝트를 사용자 지정할 수 있습니다.

| API                                                          | 설명                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance)                            | TUICallEngine 인스턴스 생성(싱글톤 모드) |
| [destroyInstance](#destroyinstance)                          | TUICallEngine 인스턴스 종료(싱글톤 모드) |
| [on](#on) | 이벤트 수신                            |
| [off](#off) | 이벤트 수신 중지                        |
| [login](#login) | 로그인                            |
| [logout](#logout) | 로그아웃                            |
| [setSelfInfo](#setselfinfo) | 대화명 및 프로필 사진 설정                  |
| [call](#call) | C2C 통화 걸기                         |
| [groupCall](#groupcall) | 그룹 통화 걸기                        |
| [accept](#accept) | 통화 수락                            |
| [reject](#reject) | 통화 거절                            |
| [hangup](#hangup) | 통화 종료                            |
| [switchCallingType](#switchcallingtype) | 통화 유형 변경                      |
| [startRemoteView](#startremoteview) | 원격 비디오 렌더링 시작                    |
| [stopRemoteView](#stopremoteview) | 원격 비디오 렌더링 중지                    |
| [startLocalView](#startlocalview) | 로컬 비디오 렌더링 시작                    |
| [stopLocalView](#stoplocalview) | 로컬 비디오 렌더링 중지                    |
| [openCamera](#opencamera) | 카메라 켜기                          |
| [closeCamara](#closecamara) | 카메라 끄기                          |
| [openMicrophone](#openmicrophone) | 마이크 켜기                          |
| [closeMicrophone](#closemicrophone) | 마이크 끄기                          |
| [setMicMute](#setmicmute) | 마이크 음소거 여부 설정                  |
| [setVideoQuality](#setvideoquality) | 비디오 품질 설정                        |
| [getDeviceList](#getdevicelist) | 장치 목록 가져오기                        |
| [switchDevice](#switchdevice) | 다른 카메라/마이크로 변경              |

## 이벤트 유형

TUICallEvent는 TUICallEngine의 콜백 클래스입니다. 이벤트를 수신하는 데 사용할 수 있습니다.

| EVENT                                                        | 설명                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | SDK 내부 오류 발생                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | SDK는 ready 상태임                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | 반복된 로그인으로 인해 현재 사용자가 방에서 제거됨                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | 사용자가 전화를 수락함                     |
| [TUICallEvent.USER_ENTER](#user_enter) | 사용자가 통화 참여에 동의함             |
| [TUICallEvent.USER_LEAVE](#user_leave) | 사용자가 통화를 종료하는 데 동의함             |
| [TUICallEvent.REJECT](#reject) | 사용자가 통화를 거부함                                         |
| [TUICallEvent.NO_RESP](#no_resp) | 초대된 사용자가 응답하지 않음                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | 초대자가 통화 중임                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | 통화 시간 초과(초대 대상자가 수신) |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | 원격 사용자가 카메라를 켜고 끔              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | 원격 사용자가 마이크 켜기/끄기              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | 원격 사용자가 통화 볼륨을 조정함                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | 그룹 통화 초대 목록이 업데이트됨                           |
| [TUICallEvent.INVITED](#invited) | 통화에 초대됨                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | 통화가 취소됨(초대받은 사람이 수신함)   |
| [TUICallEvent.CALLING_END](#calling_end) | 통화가 종료됨                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | 장치 목록이 업데이트됨                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | 통화 유형이 변경됨                               |

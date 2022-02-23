## 오류 코드
### 기본 오류 코드

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_NULL|0|오류 없음|

### 방 입장 오류 코드

TRTCCloud.enterRoom()은 방 입장이 실패하면 이러한 유형의 오류 코드를 트리거합니다. 콜백 API TRTCCloudDelegate.onEnterRoom() 및 TRTCCloudDelegate.OnError()를 사용하여 회의실 입장 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_ROOM_ENTER_FAIL|-3301|방 입장 실패|
|ERR_ENTER_ROOM_PARAM_NULL|-3316|빈 방 입장 매개변수. TRTCCloud.enterRoom(): API 호출 시 유효한 param 전달 여부 확인|
|ERR_SDK_APPID_INVALID|-3317|잘못된 sdkAppId 값|
|ERR_ROOM_ID_INVALID|-3318|잘못된 roomId 값|
|ERR_USER_ID_INVALID|-3319|잘못된 사용자 ID 값|
|ERR_USER_SIG_INVALID|-3320|잘못된 userSig 값|
|ERR_ROOM_REQUEST_ENTER_ROOM_TIMEOUT|-3308|방 입장 요청 시간 초과. 네트워크를 확인하십시오.|
|ERR_SERVER_INFO_SERVICE_SUSPENDED|-100013|서비스 이용 불가. Tencent Cloud 계정 연체 여부를 확인하십시오.|


### 방 퇴장 오류 코드

TRTCCloud.exitRoom()은 방 종료가 실패하면 이 오류 코드를 트리거합니다. 콜백 API TRTCCloudDelegate.OnError()를 사용하여 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_ROOM_REQUEST_QUIT_ROOM_TIMEOUT|-3325|방 퇴장 요청 시간 초과|


### 장치(카메라, 마이크, 스피커) 오류 코드

콜백 API TRTCCloudDelegate.OnError()를 사용하여 장치 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_CAMERA_START_FAIL|-1301|카메라 활성화 실패. 예: Windows 또는 MacOS에서 카메라 구성 프로그램(드라이버)에 문제. 카메라를 껐다가 다시 켜거나 카메라를 다시 시작하거나 구성 프로그램을 업데이트합니다.|
|ERR_CAMERA_NOT_AUTHORIZED|-1314|카메라 권한 오류. 이 오류는 일반적으로 모바일 장치에서 발생하며 사용자가 카메라 권한을 거부했기 때문일 수 있습니다.|
|ERR_CAMERA_SET_PARAM_FAIL|-1315|잘못된 카메라 매개변수 설정(지원되지 않는 값 또는 기타)|
|ERR_CAMERA_OCCUPY|-1316|카메라가 점유됨. 다른 카메라로 시도해보십시오.|
|ERR_MIC_START_FAIL|-1302|마이크 활성화 실패. 예: Windows 또는 MacOS에서 마이크 구성 프로그램(드라이버)에 문제. 마이크를 껐다가 다시 켜거나 마이크를 다시 시작하거나 구성 프로그램을 업데이트합니다.|
|ERR_MIC_NOT_AUTHORIZED|-1317|마이크 권한 오류. 이 오류는 일반적으로 모바일 장치에서 발생하며 사용자가 마이크 권한을 거부했기 때문일 수 있습니다.|
|ERR_MIC_SET_PARAM_FAIL|-1318|마이크 매개변수 설정 실패|
|ERR_MIC_OCCUPY|-1319|마이크가 점유됨. 예: 사용자가 모바일 장치에서 통화 중일 때 발생합니다.|
|ERR_MIC_STOP_FAIL|-1320|마이크 끄기 실패|
|ERR_SPEAKER_START_FAIL|-1321|스피커 활성화 실패. 예: Windows 또는 MacOS에서 스피커 구성 프로그램(드라이버) 문제. 스피커를 껐다가 다시 켜거나 스피커를 다시 시작하거나 구성 프로그램을 업데이트합니다.|
|ERR_SPEAKER_SET_PARAM_FAIL|-1322|스피커 매개변수 설정 실패|
|ERR_SPEAKER_STOP_FAIL|-1323|스피커 끄기 실패|


### 화면 공유 오류 코드

콜백 API TRTCCloudDelegate.OnError()를 사용하여 화면 공유 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_SCREEN_CAPTURE_START_FAIL|-1308|모바일 장치에서 사용자가 화면 공유 권한을 거부했기 때문일 수 있습니다. Windows 또는 MacOS인 경우, 화면 캡처 API의 매개변수가 요구 조건에 부합하는지 확인합니다.|
|ERR_SCREEN_CAPTURE_UNSURPORT|-1309|화면 캡처 실패. 버전을 확인하십시오(Android 5.0 이상, iOS 11.0 이상).|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_SUB_VIDEO|-102015|서브스트림 비디오 이미지 발송 권한 없음|
|ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO|-102016|다른 사용자가 서브스트림 비디오 이미지를 보내는 중|
|ERR_SCREEN_CAPTURE_STOPPED|-7001|시스템에서 화면 캡처 중지|


### 인코딩 및 디코딩 오류 코드

콜백 API TRTCCloudDelegate.OnError()를 사용하여 인코딩 및 디코딩 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_VIDEO_ENCODE_FAIL|-1303|비디오 프레임 인코딩 실패. 예: iOS 사용자가 다른 앱으로 전환할 때 발생하며, 시스템에서 하드웨어 인코더가 해제될 수 있습니다. 사용자가 재전환하면 하드웨어 인코더가 재시작 전에 이 오류가 발생할 수 있습니다.|
|ERR_UNSUPPORTED_RESOLUTION|-1305|지원되지 않는 비디오 해상도|
|ERR_AUDIO_ENCODE_FAIL|-1304|오디오 프레임 인코딩 실패. 예: SDK가 전달된 사용자 지정 오디오 데이터를 처리할 수 없을 때 발생합니다.|
|ERR_UNSUPPORTED_SAMPLERATE|-1306|지원되지 않는 오디오 샘플 속도|


### 사용자 정의 캡처에 대한 오류 코드

콜백 API TRTCCloudDelegate.OnError()를 사용하여 사용자 지정 캡처 오류에 대한 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_PIXEL_FORMAT_UNSUPPORTED|-1327|지원되지 않는 pixel format|
|ERR_BUFFER_TYPE_UNSUPPORTED|-1328|지원되지 않는 buffer type|


### CDN 바인딩 및 혼합 스트림 오류 코드

콜백 API TRTCCloudDelegate.onStartPublishing() 및 TRTCCloudDelegate.onSetMixTranscodingConfig()를 사용하여 관련 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_PUBLISH_CDN_STREAM_REQUEST_TIME_OUT|-3321|릴레이된 푸시 요청 시간 초과|
|ERR_CLOUD_MIX_TRANSCODING_REQUEST_TIME_OUT|-3322|On-Cloud MixTranscoding 요청 시간 초과|
|ERR_PUBLISH_CDN_STREAM_SERVER_FAILED|-3323|릴레이된 푸시에 대한 비정상적인 응답 패킷|
|ERR_CLOUD_MIX_TRANSCODING_SERVER_FAILED|-3324|On-Cloud MixTranscoding에 대한 응답 패킷 예외 |
|ERR_ROOM_REQUEST_START_PUBLISHING_TIMEOUT|-3333|Tencent Cloud의 라이브 스트리밍 CDN 푸시 시작 신호 시간 초과|
|ERR_ROOM_REQUEST_START_PUBLISHING_ERROR|-3334|Tencent Cloud의 라이브 스트리밍 CDN에 대한 푸시 신호 예외|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_TIMEOUT|-3335|Tencent Cloud의 라이브 스트리밍 CDN에 대한 푸시 중지 신호 시간 초과|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_ERROR|-3336|Tencent Cloud의 라이브 스트리밍 CDN으로 푸시를 중지 신호 예외|


### 크로스 룸 공동 앵커 관련 오류 코드

TRTCCloud.ConnectOtherRoom()은 크로스 룸 공동 앵커링이 실패하는 경우 이러한 유형의 오류 코드를 트리거합니다. 콜백 API TRTCCloudDelegate.onConnectOtherRoom()을 사용하여 관련 알림을 캡처할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|ERR_ROOM_REQUEST_CONN_ROOM_TIMEOUT|-3326|공동 앵커 요청 시간 초과|
|ERR_ROOM_REQUEST_DISCONN_ROOM_TIMEOUT|-3327|공동 앵커 종료 요청 시간 초과|
|ERR_ROOM_REQUEST_CONN_ROOM_INVALID_PARAM|-3328|잘못된 매개 변수|
|ERR_CONNECT_OTHER_ROOM_AS_AUDIENCE|-3330|현재 시청자 역할이므로 공동 앵커링을 시작하거나 종료할 수 없습니다. 먼저 switchRole()를 통해 앵커 역할로 전환해야 합니다.|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_SUPPORT|-102031|크로스룸 공동 앵커링 미지원|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_NUM|-102032|공동 앵커 통화의 최댓값에 도달|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_RETRY_TIMES|-102033|크로스 룸 공동 앵커링에 대한 재시도 횟수 소진|
|ERR_SERVER_CENTER_CONN_ROOM_REQ_TIMEOUT|-102034|크로스 룸 공동 앵커 요청 시간 초과|
|ERR_SERVER_CENTER_CONN_ROOM_REQ|-102035|잘못된 크로스 룸 공동 앵커 요청 형식|
|ERR_SERVER_CENTER_CONN_ROOM_NO_SIG|-102036|크로스 룸 공동 앵커링에 대한 서명 없음|
|ERR_SERVER_CENTER_CONN_ROOM_DECRYPT_SIG|-102037|크로스 룸 공동 앵커 서명 복호화 실패|
|ERR_SERVER_CENTER_CONN_ROOM_NO_KEY|-102038|크로스 룸 공동 앵커 서명 복호화 키 찾을 수 없음|
|ERR_SERVER_CENTER_CONN_ROOM_PARSE_SIG|-102039|크로스 룸 공동 앵커링 서명 구문 분석 오류|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SIG_TIME|-102040|잘못된 크로스 룸 공동 앵커 서명 타임스탬프|
|ERR_SERVER_CENTER_CONN_ROOM_SIG_GROUPID|-102041|잘못된 크로스 룸 공동 앵커 서명|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_CONNED|-102042|이 방에는 공동 앵커가 없음|
|ERR_SERVER_CENTER_CONN_ROOM_USER_NOT_CONNED|-102043|사용자가 공동 앵커를 시작하지 않았음|
|ERR_SERVER_CENTER_CONN_ROOM_FAILED|-102044|크로스 룸 공동 앵커를 시작 실패|
|ERR_SERVER_CENTER_CONN_ROOM_CANCEL_FAILED|-102045|크로스 룸 공동 앵커 취소 실패|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_ROOM_NOT_EXIST|-102046|공동 앵커링을 위해 연결된 방 없음|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_REACH_MAX_ROOM|-102047|공동 앵커 룸의 최댓값에 도달|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_NOT_EXIST|-102048|공동 앵커를 요청한 사용자 없음|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_DELETED|-102049|공동 앵커를 요청한 사용자 삭제|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_FULL|-102050|공동 앵커링을 위해 호출되는 사용자의 모든 리소스가 점유됨|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SEQ|-102051|순차 순서가 아닌 공동 앵커의 순번|


## 경고 코드

경고 코드는 특별한 주의가 필요하지 않습니다. 상황에 따라 사용자에게 메시지를 표시할지 여부를 선택할 수 있습니다.

| 코드 | 값 | 설명 |
|---|---|---|
|WARNING_HW_ENCODER_START_FAIL|1103|하드웨어 인코더 시작 실패. SDK가 자동으로 소프트웨어 인코더로 전환합니다.|
|WARNING_VIDEO_ENCODER_SW_TO_HW|1107|소프트웨어 인코더용 CPU가 충분하지 않음. SDK가 자동으로 하드웨어 인코더로 전환합니다.|
|WARNING_INSUFFICIENT_CAPTURE_FPS|1108|카메라가 캡처한 비디오의 프레임 속도가 충분하지 않음. 이 오류는 뷰티 필터 알고리즘이 내장된 Android 기기에서 발생할 수 있습니다.|
|WARNING_SW_ENCODER_START_FAIL|1109|소프트웨어 인코딩 실행 실패|
|WARNING_REDUCE_CAPTURE_RESOLUTION|1110|프레임 속도와 성능 간의 균형을 위해 카메라 해상도 낮춤.|
|WARNING_CAMERA_DEVICE_EMPTY|1111|감지된 카메라 없음|
|WARNING_CAMERA_NOT_AUTHORIZED|1112|사용자가 애플리케이션 카메라 액세스 권한을 부여하지 않았음|
|WARNING_MICROPHONE_DEVICE_EMPTY|1201|마이크가 감지되지 않음|
|WARNING_SPEAKER_DEVICE_EMPTY|1202|스피커가 감지되지 않음|
|WARNING_MICROPHONE_NOT_AUTHORIZED|1203|사용자가 애플리케이션 마이크 액세스 권한 미부여|
|WARNING_MICROPHONE_DEVICE_ABNORMAL|1204|오디오 캡처 장치를 사용 불가(예: 장치 사용 중)|
|WARNING_SPEAKER_DEVICE_ABNORMAL|1205|사용 가능한 오디오 재생 장치가 없음(예: 장치 사용 중)|
|WARNING_VIDEO_FRAME_DECODE_FAIL|2101|현재 비디오 프레임 디코딩 실패|
|WARNING_AUDIO_FRAME_DECODE_FAIL|2102|현재 오디오 프레임 디코딩 실패|
|WARNING_VIDEO_PLAY_LAG|2105|비디오 재생 지연|
|WARNING_HW_DECODER_START_FAIL|2106|하드웨어 디코더 시작 실패. 소프트웨어 디코더가 사용됩니다.|
|WARNING_VIDEO_DECODER_HW_TO_SW|2108|하드웨어 디코더의 현재 스트림의 첫 번째 I-프레임 디코딩 실패. SDK가 자동으로 소프트웨어 디코더로 전환합니다.|
|WARNING_SW_DECODER_START_FAIL|2109|소프트웨어 디코더 실행 실패|
|WARNING_VIDEO_RENDER_FAIL|2110|비디오 렌더링 실패|
|WARNING_START_CAPTURE_IGNORED|4000|동영상 캡처가 이미 시작됨. 요청이 무시됩니다.|
|WARNING_AUDIO_RECORDING_WRITE_FAIL|7001|녹음된 오디오 파일에 쓰기 실패|
|WARNING_ROOM_DISCONNECT|5101|네트워크 연결 끊김|
|WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE|6001|현재 시청자 역할이므로 오디오/비디오 데이터 전송 요청이 무시됩니다.|
|WARNING_NET_BUSY|1101|잘못된 네트워크 연결. 제한된 업스트림 대역폭으로 인해 데이터 업로드가 차단됩니다.|
|WARNING_RTMP_SERVER_RECONNECT|1102|푸시 오류. 네트워크 재연결이 시도됩니다(최대 시도 횟수: 3).|
|WARNING_LIVE_STREAM_SERVER_RECONNECT|2103|풀 스트림 오류. 네트워크 재연결이 시도됩니다(최대 시도 횟수: 3).|
|WARNING_RECV_DATA_LAG|2104|불안정한 수신 패킷. 불충분한 다운스트림 대역폭 또는 앵커의 불안정한 스트림으로 인해 발생할 수 있습니다.|
|WARNING_RTMP_DNS_FAIL|3001|라이브 스트리밍 오류. DNS 확인 실패|
|WARNING_RTMP_SEVER_CONN_FAIL|3002|라이브 스트리밍 오류. 서버 연결 실패.|
|WARNING_RTMP_SHAKE_FAIL|3003|라이브 스트리밍 오류. RTMP 서버와의 핸드셰이크 실패|
|WARNING_RTMP_SERVER_BREAK_CONNECT|3004|라이브 스트리밍 오류. 서버에 의해 연결이 끊어짐.|
|WARNING_RTMP_READ_WRITE_FAIL|3005|라이브 스트리밍 오류. RTMP 읽기/쓰기 실패. 연결이 해제됩니다.|
|WARNING_RTMP_WRITE_FAIL|3006|라이브 스트리밍 오류. RTMP 쓰기 실패. SDK의 내부 오류 코드이며 외부에 노출되지 않습니다.|
|WARNING_RTMP_READ_FAIL|3007|라이브 스트리밍 오류. RTMP 읽기 실패. SDK의 내부 오류 코드이며 외부에 노출되지 않습니다.|
|WARNING_RTMP_NO_DATA|3008|라이브 스트리밍 오류. 30초 이상 데이터가 전송되지 않아 서버 연결이 끊깁니다.|
|WARNING_PLAY_LIVE_STREAM_INFO_CONNECT_FAIL|3009|라이브 스트리밍 오류. 서버에 연결하기 위한 connect 호출 실패. SDK의 내부 오류 코드이며 외부에 노출되지 않습니다.|
|WARNING_NO_STEAM_SOURCE_FAIL|3010|라이브 스트리밍 오류. 스트림 주소에 비디오가 없어 연결에 실패했습니다. SDK의 내부 오류 코드이며 외부에 노출되지 않습니다.|
|WARNING_ROOM_RECONNECT|5102|네트워크 연결 끊김. 재연결 중입니다.|
|WARNING_ROOM_NET_BUSY|5103|잘못된 네트워크 연결: 제한된 업스트림 대역폭으로 인해 데이터 업로드가 차단되었습니다.|
    

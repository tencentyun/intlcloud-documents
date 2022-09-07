본문에서는 개발자가 GME API를 쉽게 디버그하고 액세스할 수 있도록 Tencent Cloud GME(게임 멀티미디어 엔진) 개발 중에 보고될 수 있는 오류 코드를 제공합니다.

## 일반적인 에러

| 에러 코드 이름                    | 에러 코드 값 | 원인 및 제안 솔루션                                               |
| ----------------------------- | -------- | ------------------------------------------------------------ |
| AV_ERR_3DVOICE_ERR_NOT_INITED | 7003     | InitSpatializer API를 먼저 호출해야 함                              |
| AV_ERR_NET_REQUEST_FALLED     | 7004     | 주로 불안정한 네트워크 연결로 인한 네트워크 요청 실패, 문제 해결은 [FAQ > Sound and Audio](https://intl.cloud.tencent.com/document/product/607/35611) 참고 |
|AV_ERR_CHARGE_OVERDUE         | 7005     | 연체로 인한 작업 실패, Tencent Cloud 콘솔에서 계정이 연체되었는지 확인 필요           |
|AV_ERR_AUTH_FIALD             | 7006     | 인증 실패, 가능한 원인: 1. 'AppID'가 존재하지 않거나 올바르지 않음 2. 'authbuff' 인증 중 오류 발생 3. 인증 만료 |
| AV_ERR_IN_OTHER_ROOM          | 7007     | 이미 다른 방에 있음                                               |
| AV_ERR_NO_PERMISSION          | 7009     | 작업을 수행할 권한이 없음                               |
| AV_ERR_FILE_CANNOT_ACCESS     | 7010     | 파일에 액세스할 수 없음                                                 |
| AV_ERR_FILE_DAMAGED           | 7011     | 파일 손상                                                   |
| AV_ERR_SERVICE_NOT_OPENED     | 7012     | 사용하기 전에 콘솔에서 이 기능을 활성화하십시오                     |
| AV_ERR_USER_CANCELED          | 7013     | 사용자가 방에 들어가는 등의 작업을 성공하기 전에 취소했음             |
|AV_ERR_LOAD_LIB_FAILED       |7014|라이브러리 파일이 제대로 로드되지 않았음, 누락되었는지 확인하십시오|k
|AV_ERR_SDK_NOT_FULL_UPDATE       |7015|SDK를 업그레이드할 때 모든 파일이 업그레이드되지 않아 일부 모듈 불일치 발생, SDK를 완전히 업그레이드하십시오|
|AV_ERR_3DVOICE_ERR_FILE_DAMAGED       |7002|3D 사운드 파일 로딩에 실패하였습니다|

## 클라이언트 오류

<table>
<thead>
<tr>
<th>에러 코드 이름</th>
<th>에러 코드 값</th>
<th>의미</th>
<th>원인</th>
<th>권장 솔루션 &nbsp;&nbsp;&nbsp;&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_REPEATED<br>_OPERATION</td>
<td>1001</td>
<td>반복 작업</td>
<td>작업이 진행 중일 때 다시 동일한 작업을 실행 시 발생합니다. 작업 유형에는 AVContext, 방, 장치 및 구성원 관련 작업이 포함됩니다. AVContext 유형의 작업: StartContext/StopContext. 방 유형의 작업: EnterRoom/ExitRoom. 장치 유형의 작업: 장치를 시작/종료합니다.</td>
<td>마지막 작업이 완료된 후 작업을 수행하십시오.</td>
</tr>
<tr>
<td>AV_ERR_EXCLUSIVE<br>_OPERATION</td>
<td>1002</td>
<td>독점 작업</td>
<td>동일한 유형의 다른 작업이 진행 중일 때 다시 같은 유형의 작업을 실행 시 해당 에러가 발생됩니다.</td>
<td>마지막 작업이 완료된 후 작업을 수행하십시오.</td>
</tr>
<tr>
<td>AV_ERR_HAS_IN<br>_THE_STATE</td>
<td>1003</td>
<td>반복 작업</td>
<td>대상이 어느 상태에 있을 때 다시 해당 상태로 변경하는 작업 시 해당 에러가 발생됩니다. 예를 들어, 이미 방에 있는 상태에서 다시 방 입장 작업을 실행.</td>
<td>이미 해당 상태이므로 작업 결과를 성공한 것으로 처리합니다.</td>
</tr>
<tr>
<td>AV_ERR_INVALID<br>_ARGUMENT</td>
<td>1004</td>
<td>잘못된 매개변수</td>
<td>SDK API 호출 시 잘못된 매개변수가 전달되면 해당 에러가 발생됩니다. 예를 들어 방에 입장하려 할 때 전달 방 유형이 AVRoom::ROOM_TYPE_PAIR 또는 AVRoom::ROOM_TYPE_MULTI가 아닐 시 에러가 발생됩니다.</td>
<td>각 API의 각 매개변수에 대한 유효한 값 범위를 얻으려면 관련 API 문서를 주의 깊게 읽으십시오. 입력 매개변수의 정확성을 보장하기 위해 예방 조치를 취하십시오.</td>
</tr>
<tr>
<td>AV_ERR_TIMEOUT</td>
<td>1005</td>
<td>시간 초과</td>
<td>지정된 시간 내에 작업 결과가 반환되지 않을 시 해당 에러가 발생합니다. 이 에러는 주로 시그널 전송 관련된 네트워크 문제가 발생될 때 발생합니다. 예를 들어 방에 들어가기 위한 작업을 수행한 후 30s 이내에 작업 결과가 반환되지 않을 시 에러가 발생합니다.</td>
<td>네트워크가 정상인지, 외부 네트워크 연결이 가능한지 확인한 후 다시 시도하십시오.</td>
</tr>
<tr>
<td>AV_ERR_NOT<br>_IMPLEMENTED</td>
<td>1006</td>
<td>구현되지 않음</td>
<td>SDK API 호출 시 해당 기능이 지원되지 않는다면 해당 기능을 사용할 수 없습니다.</td>
<td>지원되지 않는 기능입니다. 다른 방법을 찾으십시오.</td>
</tr>
<tr>
<td>AV_ERR_NOT_IN<br>_MAIN_THREAD</td>
<td>1007</td>
<td>메인 스레드에 없음</td>
<td>SDK 외부 API는 메인 스레드에서 호출해야 합니다. 만약 메인 스레드에서 호출하지 않으면 해당 에러가 발생합니다.</td>
<td>SDK API가 메인 스레드에서 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_RESOURCE<br>_IS_OCCUPIED</td>
<td>1008</td>
<td>리소스 점유됨</td>
<td>필요한 카메라 또는 화면과 같은 필수 리소스가 이미 사용 중 일 때 해당 에러가 발생합니다.</td>
<td>필요한 특정 리소스를 파악하고 이러한 리소스가 사용되고 있는 이유를 확인하여 리소스 충돌 없이 SDK 기능이 사용되도록 하십시오.</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_EXIST</td>
<td>1101</td>
<td>AVContext 상태 문제</td>
<td>AVContext 객체가 CONTEXT_STATE_STARTED 상태가 아닐 때 AVContext 객체가 이 상태에 있을 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_CONTEXT<br>_NOT_STOPPED</td>
<td>1102</td>
<td>AVContext 상태 문제</td>
<td>AVContext 객체가 CONTEXT_STATE_STOPPED 상태가 아닐 때 해당 상태에 있을 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다. AVContext::DestroyContext와 같이 AVContext 객체가 해당 상태일 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXIST</td>
<td>1201</td>
<td>AVRoom 상태 문제</td>
<td>AVRoom 객체가 ROOM_STATE_ENTERED 상태가 아닐 때 AVRoom 객체가 이 상태일 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_ROOM<br>_NOT_EXITED</td>
<td>1202</td>
<td>AVRoom 상태 문제</td>
<td>AVRoom 객체가 ROOM_STATE_EXITED 상태가 아닐 때 해당 상태에 있을 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다. AVContext::StopContext와 같이 AVRoom 객체가 해당 상태일 때만 호출할 수 있는 API를 호출하면 에러가 발생합니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_NOT_EXIST</td>
<td>1301</td>
<td>장치가 존재하지 않음</td>
<td>장치가 존재하지 않거나 초기화되지 않은 장치를 사용 시 에러가 발생합니다.</td>
<td>장치가 있는지 확인하고 장치 ID가 올바르게 입력되었는지 확인하고 성공적으로 초기화된 후 장치를 사용하십시오.</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_NOT_EXIST</td>
<td>1401</td>
<td>AVEndpoint 객체가 존재하지 않음</td>
<td>구성원이 음성 채팅 또는 영상 채팅을 시작하지 않은 상태에서 구성원의 AVEndpoint 객체를 얻으려고 시도하였습니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_ENDPOINT<br>_HAS_NOT_VIDEO</td>
<td>1402</td>
<td>구성원이 영상 채팅을 시작하지 않음</td>
<td>구성원이 영상 채팅을 시작하지 않은 상태에서 영상이 시작된 후에만 완료할 수 있는 작업을 실행했습니다. 예를 들어, 구성원이 화상 채팅을 시작하지 않은 상태에서 구성원의 화면을 요청했습니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_TINYID_TO<br>_OPENID_FAILED</td>
<td>1501</td>
<td>tinyid를 identifier로 변환 실패</td>
<td>구성원의 정보 업데이트를 나타내는 신호를 수신한 후 tinyid를 identifier로 변환해야 합니다. 그러나 IMSDK 라이브러리 또는 네트워크의 로직 문제로 인해 변환에 실패하였습니다.</td>
<td>네트워크가 잘 작동하는지 확인하고 IMSDK 라이브러리의 로직에 문제가 있는지 로그를 확인하십시오.</td>
</tr>
<tr>
<td>AV_ERR_OPENID_TO<br>_TINYID_FAILED</td>
<td>1502</td>
<td>identifier를 tinyid로 변환 실패</td>
<td>StartContext API를 호출할 때 클라이언트는 identifier를 tinyid로 변환해야 합니다. 그러나 IMSDK 라이브러리의 로직 문제, 네트워크 문제 또는 미로그인 상태로 인해 변환이 실패하였습니다.</td>
<td>네트워크가 제대로 작동하는지 확인하고, IMSDK 라이브러리 로직에 문제가 있는지 로그를 확인하고, IMSDK 로그인 API가 성공적으로 호출되었는지 확인합니다.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_EXIST</td>
<td>1601</td>
<td>AVDeviceTest 상태 문제</td>
<td>AVDeviceTest 객체가 DEVICE_TEST_STATE_STARTED 상태가 아닐 때 AVDeviceTest 객체가 이 상태일 때만 호출할 수 있는 API를 호출했습니다.</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_DEVICE<br>_TEST_NOT_STOPPED</td>
<td>1602</td>
<td>AVDeviceTest 상태 문제</td>
<td>AVDeviceTest 객체가 DEVICE_TEST_STATE_STOPPED 상태가 아닐 때 AVDeviceTest 객체가 이 상태일 때만 호출할 수 있는 API를 호출했습니다.(예: API AVContext::StopContext).</td>
<td>SDK API가 적시에 호출되도록 서비스 로직을 수정하십시오.</td>
</tr>
<tr>
<td>AV_ERR_INVITET<br>_FAILED</td>
<td>1801</td>
<td>초대장 발송 실패</td>
<td>초대를 보내려고 하면 실패가 발생합니다.</td>
<td>초대 모듈은 DEMO용으로만 사용되며 초대 기능은 아직 사용할 수 없습니다. 따라서 이 오류 코드는 무시할 수 있습니다.</td>
</tr>
<tr>
<td>AV_ERR_ACCEPTT<br>_FAILED</td>
<td>1802</td>
<td>초대 수락 실패</td>
<td>클라이언트가 초대를 수락하려고 하면 실패가 발생합니다.</td>
<td>초대 모듈은 DEMO용으로만 사용되며 초대 기능은 아직 사용할 수 없습니다. 따라서 이 오류 코드는 무시할 수 있습니다.</td>
</tr>
<tr>
<td>AV_ERR_REFUSE<br>_FAILED</td>
<td>1803</td>
<td>초대 거부 실패</td>
<td>클라이언트가 초대를 거부하려고 하면 실패가 발생합니다.</td>
<td>초대 모듈은 DEMO용으로만 사용되며 초대 기능은 아직 사용할 수 없습니다. 따라서 이 오류 코드는 무시할 수 있습니다.</td>
</tr>
<tr>
<td>QAV_ERR_NOT_TRY<br>_NEW_ROOM</td>
<td>2001</td>
<td>새 방에 들어가지 못하고 원래 방에 남아 있습니다.</td>
<td>새 방으로 전환하는 데 실패하고 현재 방에 남아 있음</td>
<td>현재 방에 남아 있습니다.</td>
</tr>
<tr>
<td>QAV_ERR_TRY_NEW<br>_ROOM_FAILED</td>
<td>2002</td>
<td>새 방에 들어가려고 시도하지만 실패하고 원래 방을 나갑니다.</td>
<td>새 방으로 전환하는 데 실패하고 원래 방을 나감</td>
<td>다시 방으로 들어갑니다.</td>
</tr>
</tbody></table>

## 서버 오류

<table>
<thead>
<tr>
<th width="30%">에러 코드 이름</th>
<th width="11%">에러 코드 값</th>
<th width="15%">설명</th>
<th width="22%">원인</th>
<th width="22%">제안된 솔루션</th>
</tr>
</thead>
<tbody><tr>
<td>AV_ERR_SERVER_FAILED</td>
<td>10001</td>
<td>일반적인 오류</td>
<td>백엔드에서 클라이언트로 반환된 실제 오류 코드(로그 내)를 기반으로 특정 원인을 찾습니다.</td>
<td>AppID, UIN 및 AuthBuffer와 같은 방 입장을 위한 API 매개변수의 유효성을 확인합니다(문서 참고). 콘솔에서 관련 매개변수가 로컬 매개변수와 일치하는지 확인하고, 연체된 계정이 있는지 확인합니다. 개발자의 테스트 장치가 내부 네트워크 또는 외부 네트워크에서 실행되고 있는지 확인하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ARGUMENT</td>
<td>10002</td>
<td>잘못된 매개변수</td>
<td>SDK API가 호출되거나 SDK 내부 신호가 백엔드로 전송될 때 하나 이상의 잘못된 매개변수가 전달됬습니다.</td>
<td>SDK API 호출에서 전달된 매개변수의 정확성을 확인하십시오. 로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 에러 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NO_PERMISSION</td>
<td>10003</td>
<td>권한 없음</td>
<td>기능을 사용할 권한이 없습니다. 예를 들어, 방에 들어가려고 할 때 올바르지 않거나 만료된 서명을 제공했습니다.</td>
<td>올바른 권한 매개변수를 제공한 후에만 기능을 사용하십시오. AppID와 권한 키가 맞는지 확인하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER_TIMEOUT</td>
<td>10004</td>
<td>시간 초과</td>
<td>지정된 시간 내에 작업 결과가 반환되지 않았습니다.</td>
<td>로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER_ALLOC<br>_RESOURCE_FAILED</td>
<td>10005</td>
<td>네트워크 오류</td>
<td>클라이언트가 작업을 수행할 때 네트워크 오류 발생</td>
<td>AppID, UIN 및 AuthBuffer와 같은 방 입장을 위한 API 매개변수의 유효성을 확인합니다(문서 참고). 유효한 경우 개발자의 테스트 장치가 내부 네트워크 또는 외부 네트워크에서 실행되고 있는지 확인하십시오. 내부 네트워크인 경우 개발자에게 url: openmsf.3g.qq.com:15000에 연결할 수 있는지 확인하도록 요청하십시오. 만약 그렇다면 url: cloud.tim.qq.com:15000에 연결할 수 있는지 확인하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ID_NOT_IN_ROOM</td>
<td>10006</td>
<td>방에 없음</td>
<td>클라이언트는 방에 없을 때 일부 작업을 수행했습니다.</td>
<td>SDK 기능이 적시에 사용되는지 확인</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_NOT_IMPLEMENT</td>
<td>10007</td>
<td>구현되지 않음</td>
<td>SDK API 호출 시 해당 기능을 사용할 수 없습니다.</td>
<td>다른 대체 방법을 찾으십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_REPEATED_OPERATION</td>
<td>10008</td>
<td>반복 작업</td>
<td>동일한 유형의 다른 작업이 진행 중일 때 작업을 실행했습니다.</td>
<td>마지막 작업이 완료된 후 작업을 실행합니다.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ROOM_NOT_EXIST</td>
<td>10009</td>
<td>방이 존재하지 않음</td>
<td>존재하지 않는 방에서 작업을 실행했습니다.</td>
<td>SDK 기능이 적시에 사용되는지 확인</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_ENDPOINT_NOT_EXIST</td>
<td>10010</td>
<td>구성원이 존재하지 않음</td>
<td>존재하지 않는 구성원과 관련된 일부 작업이 실행됬습니다.</td>
<td>로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오.</td>
</tr>
<tr>
<td>AV_ERR_SERVER<br>_INVALID_ABILITY</td>
<td>10011</td>
<td>잘못된 기능</td>
<td>백엔드에서 클라이언트로 반환된 실제 오류 코드(로그 내)를 기반으로 특정 원인을 찾습니다.</td>
<td>로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오.</td>
</tr>
</tbody></table>

## 음성 메시지 오류

| 에러 코드 이름                                         | 에러 코드 값 | 설명               | 원인                                                       | 제안된 솔루션                                                     |
| -------------------------------------------------- | -------- | ------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| QAVPTTERROR_RECORDER<br>\_PARAM_NULL                    | 4097     | 녹음 오류           | 매개변수가 비어 있음                                                   | 코드의 API 매개변수가 올바른지 확인하십시오.                                 |
| QAVPTTERROR_RECORDER<br>\_INIT_ERROR                    | 4098     | 녹음 오류           | 초기화 오류                                                 | 장치가 점유되어 있는지, 권한이 정상인지, 초기화가 정상인지 확인하십시오.       |
| QAVPTTERROR_RECORDER<br>\_RECORDING_ERR                 | 4099     | 녹음 오류           | 녹음 진행 중                                                 | SDK 기록 기능이 적시에 사용되는지 확인하십시오.                          |
| QAVPTTERROR_RECORDER<br>\_NODATA_ERR                    | 4100     | 녹음 오류           | 오디오 데이터 수집되지 않음                                         | 마이크가 제대로 작동하는지 확인하십시오.                                     |
| QAVPTTERROR_RECORDER<br>\_OPENFILE_ERR                  | 4101     | 녹음 오류           | 녹화 파일 액세스 중 오류 발생                                   | 파일의 존재와 파일 경로의 유효성을 확인하십시오.                             |
| QAVPTTERROR_RECORDER<br>\_PERMISSION_MIC_ERR            | 4102     | 녹음 오류           | 마이크가 인증되지 않았음                                           | SDK를 사용하기 위해서는 마이크 권한이 필요합니다. 권한을 추가하려면 특정 엔진 또는 플랫폼에 대한 SDK 프로젝트 구성 문서를 참고하십시오. |
| QAVPTTERROR_RECORDER<br>\_AUDIO_TOO_SHORT               | 4103     | 녹음 오류           | 녹음 시간이 너무 짧음                                           | 기록 시간은 ms 단위로 1000밀리초 이상이어야 합니다. |
| QAVPTTERROR_RECORDER<br>\_RECORD_NOT_START              | 4104     | 녹음 오류           | 녹음 작업이 시작되지 않음                                           | 녹화 시작을 위한 API가 호출되었는지 확인합니다.                               |
| QAVPTTERROR_UPLOAD<br>\_FILE_ACCESSERROR                | 8193     | 업로드 오류           | 파일 액세스 중 오류 발생                                   | 파일의 존재와 파일 경로의 유효성을 확인하십시오.                             |
| QAVPTTERROR_UPLOAD<br>\_SIGN_CHECK_FAIL                 | 8194     | 업로드 오류           | 서명 확인 실패                                           | 인증 키가 맞는지, 음성메시지가 초기화 되었는지 확인하십시오.             |
| QAVPTTERROR_UPLOAD<br>\_COS_INTERNAL_FAIL               | 8195     | 업로드 오류           | 네트워크 오류 발생                                                   | 장치가 인터넷에 액세스할 수 있는지 확인합니다. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_UPLOAD<br>\_GET_TOKEN_NETWORK_FAIL          | 8196     | 업로드 오류           | 업로드 매개변수를 가져오는 동안 네트워크에 오류 발생                                 | 인증이 올바른지, 기기가 인터넷에 접속할 수 있는지 확인하십시오. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_UPLOAD<br>\_SYSTEM_INNER_ERROR              | 8197     | 업로드 오류           | 업로드 매개변수를 가져오는 동안 반환된 패킷이 비어 있음                             | 인증이 올바른지, 디바이스 네트워크가 외부 네트워크 환경에 정상적으로 접근할 수 있는지 확인하십시오. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_UPLOAD<br>\_RSP_DATA_DECODE_FAIL            | 8198     | 업로드 오류           | 업로드 매개변수를 가져오는 동안 반환된 패킷 디코딩 실패                             | 인증이 올바른지, 기기가 인터넷에 접속할 수 있는지 확인하십시오. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_UPLOAD<br>\_APPINFO_UNSET                   | 8200     | 업로드 오류           | appinfo가 설정되지 않았음                                           | apply API가 호출되었는지 또는 입력 매개변수가 비어 있는지 확인합니다.                |
| QAVPTTERROR_DOWNLOAD<br>\_FILE_ACCESSERROR              | 12289    | 다운로드 오류           | 파일 액세스 중 오류 발생                                   | 파일 경로가 유효한지 확인하십시오.                                       |
| QAVPTTERROR_DOWNLOAD<br>\_SIGN_CHECK_FAIL               | 12290    | 다운로드 오류           | 서명 확인 실패                                               | 인증키가 맞는지, 음성메시지가 초기화 되었는지 확인하십시오.             |
| QAVPTTERROR_DOWNLOAD<br>\_COS_INTERNAL_FAIL             | 12291    | 다운로드 오류           | 네트워크 오류                                                   | 서버가 오디오 파일을 가져오지 못했습니다. API 매개변수 fileid가 올바른지, 네트워크가 정상인지 확인하십시오. |
| QAVPTTERROR_DOWNLOAD<br>\_REMOTEFILE_ACCESSERROR        | 12292    | 다운로드 오류           | 서버 파일 시스템 오류                                         | 장치가 인터넷에 액세스할 수 있는지 확인하고 파일이 서버에 있는지 확인하십시오. |
| QAVPTTERROR_DOWNLOAD<br>\_GET_SIGN_NETWORK_FAIL         | 12293    | 다운로드 오류           | 다운로드 매개변수를 가져오는 동안 HTTP 네트워크 실패                          | 장치가 인터넷에 액세스할 수 있는지 확인합니다. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_DOWNLOAD<br>\_SYSTEM_INNER_ERROR            | 12294    | 다운로드 오류           | 다운로드 매개변수를 가져오는 동안 반환된 패킷이 비어 있음                           | 장치가 인터넷에 액세스할 수 있는지 확인하십시오. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_DOWNLOAD_GET<br>\_SIGN_RSP_DATA_DECODE_FAIL | 12295    | 다운로드 오류           | 다운로드 매개변수를 가져오는 동안 반환된 패킷 디코딩 실패                           | 장치가 인터넷에 액세스할 수 있는지 확인하십시오. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_DOWNLOAD<br>\_APPINFO_UNSET                 | 12297    | 다운로드 오류           | appinfo가 설정되지 않았음                                           | 인증키가 맞는지, 음성메시지가 초기화 되었는지 확인하십시오.             |
| QAVPTTERROR_PLAYER_INIT_ERR                        | 20481    | 재생 오류           | 초기화 오류                                                 | 디바이스가 사용 중인지, 권한이 정상인지, 초기화가 정상인지 확인하십시오.       |
| QAVPTTERROR_PLAYER<br>\_PLAYING_ERR                     | 20482    | 재생 오류           | 재생 중에 중단하고 다음을 재생하려고 했지만 실패했습니다(정상적으로 성공해야 함). | 코드 로직이 올바른지 확인하십시오.                                       |
| QAVPTTERROR_PLAYER<br>\_PARAM_NULL                      | 20483    | 재생 오류           | 매개변수가 비어 있음                                                   | 코드의 API 매개변수가 올바른지 확인하십시오.                                 |
| QAVPTTERROR_PLAYER<br>\_OPENFILE_ERR                    | 20484    | 재생 오류           | 파일 액세스 중 재생 오류 발생                                       | 파일의 존재와 파일 경로의 유효성을 확인하십시오.                             |
| QAVPTTERROR_PLAYER<br>\_PLAYER_NOT_START_ERR            | 20485    | 재생 오류           | 재생이 시작되지 않음                                                 | 파일의 존재와 파일 경로의 유효성을 확인하십시오.                             |
| QAVPTTERROR_S2T<br>\_INTERNAL_ERROR                     | 32769    | 음성-텍스트 변환 오류     | 내부 오류 발생                                                   | 로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오. [다운로드 및 사용 문제](https://intl.cloud.tencent.com/document/product/607/30256)를 참고하십시오. |
| QAVPTTERROR_S2T<br>\_NETWORK_FAIL                       | 32770    | 음성-텍스트 변환 오류     | 네트워크 실패                                                   | 장치가 인터넷에 액세스할 수 있는지 확인합니다. [네트워크 확인 방법](https://intl.cloud.tencent.com/document/product/607/35611#.E5.87.BA.E7.8E.B0.E7.BD.91.E7.BB.9C.E9.97.AE.E9.A2.98.EF.BC.8C.E8.AF.A5.E5.A6.82.E4.BD.95.E6.8E.92.E6.9F.A5.EF.BC.9F)을 참고하십시오. |
| QAVPTTERROR_S2T<br>\_RSP_DATA_DECODE_FAIL               | 32772    | 음성-텍스트 변환 오류     | 응답 패킷 파싱 실패                                               | 로그를 분석하고 백엔드에서 클라이언트로 반환된 실제 오류 코드를 얻은 다음 백엔드 담당자에게 도움을 요청하십시오. [다운로드 및 사용 문제](https://intl.cloud.tencent.com/document/product/607/30256)를 참고하십시오. |
| QAVPTTERROR_S2T<br>\_APPINFO_UNSET                      | 32774    | 음성-텍스트 변환 오류     | appinfo가 설정되지 않음                                           | 인증키가 맞는지, 오프라인 음성채팅이 초기화 되었는지 확인하십시오.             |
| QAVPTTERROR_STREAMIN<br>\_RECORD_SUC_REC_FAIL           | 32775    | 스트리밍 음성 텍스트 변환 오류 | 스트리밍 음성-텍스트 변환은 실패하지만 녹음은 성공함                         | 네트워크가 올바르게 연결되었는지 확인하고 권한 키가 올바른지 확인하십시오.                 |
| QAVPTTERROR_S2T<br>\_SIGN_CHECK_FAIL                    | 32776    | authbuffer 인증 실패 | authbuffer 인증 실패                                        | authbuffer가 올바른지 확인하십시오.                                   |
| QAVPTTERROR_STREAMIN<br>\_UPLOADANDRECORD_SUC_REC_FAIL  | 32777    | 스트리밍 음성 텍스트 변환 오류 | 스트리밍 음성-텍스트 변환은 실패하지만 녹음 및 업로드는 성공했습니다.         | 코드에 오류가 있는지 확인하십시오.                                         |
| QAVPTTERROR_S2T_PARAM_NULL                         | 32784    | 음성-텍스트 변환 오류     | 잘못된 음성-텍스트 변환 매개변수                                         | 코드의 API 매개변수 fileid가 비어 있는지 확인하십시오.                         |
| QAVPTTERROR_S2T<br>\_AUTO_SPEECH_REC_ERROR              | 32785    | 음성-텍스트 변환 오류     | 음성-텍스트 번역에서 오류가 반환됨                                     | 음성 메시징 및 음성 텍스트 변환 기능의 백엔드에 오류가 있습니다. 로그를 분석하고, 백엔드에서 클라이언트로 반환된 실제 오류 코드를 가져오고, 백엔드 담당자에게 도움을 요청하십시오. [다운로드 및 사용 문제](https://intl.cloud.tencent.com/document/product/607/30256)를 참고하십시오. |
| QAVPTTERROR_ERR<br>\_VOICE_STREAMIN_RUNING_ERROR        | 32786    | 스트리밍 음성-텍스트 변환 오류 | 스트리밍 음성-텍스트 변환 실패                                         | 스트리밍 녹화 중 스트리밍 녹화 API의 실행 결과가 반환될 때까지 기다립니다.         |
| QAVPTTERROR_ERR_VOICE<br>\_STREAMING_ASR_ERROR          | 50012    | 스트리밍 음성-텍스트 변환 오류 | 요청 ASR 오류                                                | 녹화 파일을 다시 업로드(UploadRecordedFile)한 후 텍스트 변환 API(SpeechToText)를 호출합니다. 로그를 분석하고, 백엔드에서 클라이언트로 반환된 실제 오류 코드를 가져오고, 백엔드 담당자에게 도움을 요청하십시오. [다운로드 및 사용 문제](https://intl.cloud.tencent.com/document/product/607/30256)를 참고하십시오. |

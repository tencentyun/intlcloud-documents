## 적용 시나리오
원격 교육, 뷰티 라이브 방송, 화상 회의, 원격 손해사정, 금융 업무 녹음 및 녹화, 온라인 진료와 같은 응용 시나리오에서는 증거 수집, 품질 검사, 심사, 파일 보관, 재생 등의 업무를 위해 영상 통화 또는 라이브 스트리밍 세션을 녹화 및 저장해야 하는 경우가 많습니다.

TRTC의 클라우드 녹화는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장할 수 있습니다.
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

방 안 여러 채널의 멀티미디어에 대해 먼저 [클라우드 혼합 스트리밍 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)을 진행한 후, 혼합된 멀티미디어 스트림을 한 파일로 레코딩하는 방법도 있습니다.
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## 콘솔 가이드
[ ](id:open)
### 녹화 서비스 활성화
1. TRTC 콘솔에 로그인한 후 왼쪽 사이드바에서 **[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 선택합니다**.
2. 타깃 애플리케이션 행의 **기능 설정**을 클릭하여 기능 설정 페이지로 이동합니다. 애플리케이션을 생성하지 않은 경우 **애플리케이션 생성**을 클릭하여 애플리케이션 이름을 입력하고 **확인**을 클릭하면 새로운 애플리케이션이 생성됩니다.
3. **클라우드 녹화 활성화** 오른쪽에 있는 <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png">을(를) 클릭하면 클라우드 레코딩 설정 페이지가 팝업됩니다.


[ ](id:recordType)

### 녹화 방식 선택

TRTC의 클라우드 녹화 서비스는 '전역 자동 녹화'와 '특정 사용자 녹화' 방식을 제공합니다.
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **전역 자동 녹화**
  TRTC 방별로 각 사용자의 멀티미디어 업스트림을 모두 자동 녹화합니다. 녹화 작업의 실행 및 중지 또한 자동으로 진행되므로 별도로 신경 쓸 필요가 없어 조작이 간단하고 사용이 편리합니다. 자세한 사용 방법은 [방법1: 전역 자동 녹화](#autoRecord)를 참고하십시오.

- **특정 사용자 녹화**
  일부 사용자의 멀티미디어 스트림을 지정하여 녹화할 수 있습니다. 클라이언트의 SDK API 또는 서버의 REST API를 이용해 제어할 수 있으며, 추가적인 개발 작업이 필요합니다. 자세한 사용 방법은 [방법2: 특정 사용자 녹화(SDK API)](#recordSDKAPI) 또는 [방법3: 특정 사용자 녹화(REST API)](#recordRESTAPI)를 참고하십시오.


[ ](id:fileFormat)

### 파일 포맷 선택

클라우드 녹화는 HLS, MP4, FLV, AAC의 네 가지 파일 포맷을 지원하며 비즈니스 수요에 따라 선택할 수 있습니다. 포맷별 차이점 및 적용 시나리오는 아래 표를 참고하십시오.

<table>
<tr><th>매개변수</th><th>매개변수 설명</th></tr>
<tr>
<td>파일 유형</td>
<td>다음과 같은 파일 유형을 지원합니다. <ul style="margin:0"><li><b>HLS</b>: 대부분의 브라우저에서 온라인 재생을 지원하며, 비디오 재생 시나리오에 적합합니다. 또한 중단된 시점부터 계속 녹화가 가능하며 단일 파일 최장 시간 제한이 없습니다. </li><li><b>FLV</b>: 브라우저에서 온라인 재생을 지원하지 않으나 포맷이 간단하고 오류 발생률이 적습니다. 녹화 파일을 VOD 플랫폼에 저장할 필요가 없는 경우 해당 파일 유형을 선택할 수 있으며, 녹화 완료 후 바로 녹화 파일이 다운로드되고 원본 파일은 삭제됩니다. </li><li><b>MP4</b>: Web 브라우저에서 온라인 재생을 지원합니다. 그러나 오류 발생률이 높아 영상 통화 중 패킷 손실이 발생할 경우 최종 파일의 재생 품질에 영향을 줍니다. </li><li><b>AAC</b>: 오디오 녹음만 필요한 경우 해당 파일 유형을 선택할 수 있습니다.</li></td>
</tr>
<tr>
<td nowrap="nowrap">단일 파일 최장 시간(분)</td>
<td><ul style="margin:0"><li/>필요에 따라 레코딩 파일의 최대 길이를 설정할 수 있습니다. 시스템은 제한을 초과하는 파일을 자동으로 분할합니다. 값 범위는 1 - 120(분)입니다. <li/><b>파일 유형</b>으로 <b>HLS</b>를 선택하면 레코딩 파일 길이에 제한이 없으며 이 매개변수는 무효가 됩니다.</td>
</tr>
<tr>
<td>파일 저장 기간(일)</td>
<td>실제 비즈니스 수요에 따라 비디오 파일을 VOD 플랫폼에 저장하는 기간을 설정할 수 있습니다. 단위는 일이며 설정 가능한 범위는 0~1500입니다. 기간이 만료되면 파일은 VOD 플랫폼에서 자동으로 삭제되고 복구할 수 없습니다. 0으로 설정하면 영구 저장됩니다.</td>
</tr>
<tr>
<td>재개 시간 초과(초)</td>
<td><ul style="margin:0"><li/>기본적으로 네트워크 지터 또는 기타 이유로 통화/라이브 스트리밍 세션이 중단되면 통화가 여러 파일에 레코딩됩니다. <li/>’각 통화/라이브 스트리밍 세션에 대해 하나의 재생 링크만 생성’하려는 경우 이 매개변수를 설정할 수 있습니다. 지정된 시간 이내로 레코딩이 끊기면 하나의 파일만 생성되며, 해당 시간이 경과한 후에만 받을 수 있습니다. <li/>값 범위: 1 - 1800(초). 0은 재개 가능한 레코딩 기능을 비활성화하는 것을 의미합니다.</ul></td>
</tr>
</table>



>? HLS는 최대 30분까지 지속 녹화를 지원하여 '1교시당 1개의 재생 링크 생성'을 할 수 있습니다. 또한 대다수의 브라우저에서 온라인으로 시청할 수 있어 온라인 교육 시나리오의 비디오 재생 시나리오에 매우 적합합니다.

[ ](id:storageLocation)

### 저장 위치 선택

TRTC 클라우드 녹화 파일은 Tencent Cloud의 VOD 플랫폼에 저장되도록 기본 설정되어 있습니다. 만약 프로젝트에서 여러 비즈니스가 하나의 Tencent Cloud VOD 계정을 공유해서 사용하고 있다면 녹화 파일을 분리해서 저장해야 할 수 있습니다. Tencent Cloud VOD의 '서브 애플리케이션' 기능을 사용하면 TRTC 녹화 파일을 다른 비즈니스 파일과 분리하여 저장할 수 있습니다.

- **VOD 메인 애플리케이션과 서브 애플리케이션이란 무엇인가요?**
  메인 애플리케이션과 서브 애플리케이션은 일종의 VOD에서의 리소스 구분 방식입니다. 메인 애플리케이션은 VOD에서의 루트 계정이라고 볼 수 있으며, 서브 애플리케이션은 여러 개를 생성할 수 있고 루트 계정 하위에 있는 서브 계정이라고 볼 수 있습니다. 서브 애플리케이션은 독립적인 리소스 관리 권한을 가지며 스토리지 영역에서 다른 서브 애플리케이션과 상호 분리되어 있습니다.

- **VOD 서비스의 서브 애플리케이션은 어떻게 활성화하나요?**
  [‘서브 애플리케이션 기능 활성화’](https://intl.cloud.tencent.com/document/product/266/33987)의 안내에 따라 [VOD 콘솔](https://console.cloud.tencent.com/vod)에서 새로운 서브 애플리케이션을 추가할 수 있습니다.

[ ](id:recordCallback)

### 녹화 콜백 설정
- **녹화 콜백 주소:**
  신규 파일 [생성 공지](#callback)를 실시간으로 받고 싶은 경우, 서버에서 녹화 파일 수신 콜백에 사용할 주소를 여기에 입력하십시오. 해당 주소는 HTTP(또는 HTTPS) 프로토콜에 부합해야 합니다. 신규 녹화 파일 생성 시 Tencent Cloud에서 해당 주소를 통해 귀하의 서버로 공지를 전송합니다.
![](https://main.qcloudimg.com/raw/9b9beab813d929a7a364eb2d8ab045ba.png)
	
- **녹화 콜백 키**
콜백 키는 콜백 이벤트 수신 시 서명 인증 생성에 사용됩니다. 해당 키는 알파벳 대소문자 및 숫자로 구성되며 최대 32자까지 입력할 수 있습니다. 사용 관련 자세한 내용은 [녹화 이벤트 매개변수 설명](https://intl.cloud.tencent.com/document/product/267/38082)을 참고하십시오.
![](https://main.qcloudimg.com/raw/9fa611019c25e3c073683bc4e3ec38ae.png)

>? 자세한 녹화 콜백 수신 및 해석 방법은 문서 후반부에 있는 [레코딩 파일 수신](https://intl.cloud.tencent.com/document/product/647/35426)을 참고하십시오.



[ ](id:startAndStop)

## 녹화 제어 방법

TRTC는 [전역 자동 레코딩](#autoRecord), [특정 사용자 레코딩(SDK API 제어)](#recordSDKAPI), [특정 사용자 레코딩(REST API 제어)](#recordRESTAPI)의 세 가지 클라우드 레코딩 제어 방법을 제공합니다. 자세한 내용은 다음 설명을 참고하십시오.

- 해당 방법은 콘솔에서 어떻게 설정하나요?
- 녹화 작업은 어떻게 시작하나요?
- 녹화 작업은 어떻게 종료하나요?
- 방 안 여러 채널의 화면을 어떻게 한 채널로 혼합하나요?
- 녹화한 파일은 어떤 포맷으로 이름이 생성되나요?
- 해당 방법을 지원하는 플랫폼에는 어떤 것이 있나요?


[](id:autoRecord)

### 방법1: 전역 자동 녹화

- **콘솔 설정**
  본 레코딩 방법을 사용하려면 콘솔의 [레코딩 방식 선택](#recordType)에서 '전역 자동 레코딩'로 설정하십시오.

- **녹화 작업 시작**
  TRTC는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장하며, 별도의 조작이 필요 없습니다.

- **녹화 작업 종료**
  자동으로 종료됩니다. 즉, 호스트가 멀티미디어 업스트림을 중단하면 해당 호스트의 클라우드 레코딩이 자동으로 종료됩니다. [파일 포맷 선택](#fileFormat) 시 '지속 레코딩 시간'을 설정했다면 지속 레코딩 설정 시간이 지난 후 레코딩 파일을 확인할 수 있습니다.

- **다중 화면 혼합**
  전역 자동 녹화 모드에서의 클라우드 혼합 스트림 방법은 '서버 REST API 방법'과 '클라이언트 SDK API 방법'이 있습니다. 두 방법은 동시에 사용할 수 없습니다.
  - [서버 REST API 혼합 스트림 방법](#recordRESTAPI): 사용자의 서버에서 API를 호출하며 클라이언트 플랫폼 버전에 제한을 받지 않습니다.
  - [클라이언트 SDK API 혼합 스트림 솔루션](#recordSDKAPI): 클라이언트에서 직접 혼합 스트림을 요청할 수 있습니다. iOS, Android, Windows, Mac, Electron 등 플랫폼을 지원하며, 현재 WeChat 미니프로그램 및 Web 브라우저는 지원되지 않습니다.

- **녹화 파일 이름 생성**
  - 앵커가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정한 경우, 녹화 파일 이름이 `userDefineRecordId_streamType_시작 시간_종료 시간` 형식으로(streamType에는 main, aux의 두 값이 있으며, main은 메인 채널, aux는 보조 채널을 의미하고 보조 채널은 일반적으로 화면 공유에 사용) 생성됩니다.
  - 앵커가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정하지 않았으나 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 지정한 경우 녹화 파일 이름이 `streamId_시작 시간_종료 시간` 형식으로 생성됩니다.
  - 앵커가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수와 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 모두 지정하지 않은 경우, 녹화 파일 이름은`sdkappid_roomid_userid_streamType_시작 시간_종료 시간` 형식으로(streamType에는 main, aux의 두 가지 값이 있으며, main은 메인 채널, aux는 보조 채널을 의미하고 보조 채널은 일반적으로 화면 공유에 사용) 생성됩니다.

- **현재 지원 플랫폼**
  사용자의 서버에서 제어되며 클라이언트 플랫폼의 제한을 받지 않습니다.

[](id:recordSDKAPI)

### 방법2: 특정 사용자 녹화(SDK API)

TRTC SDK에서 제공하는 일부 API 인터페이스 및 매개변수를 호출하여 클라우드 혼합 스트림, 클라우드 녹화, 릴레이 라이브 방송의 세 가지 기능을 실행할 수 있습니다.

| 클라우드 기능 | 시작 방법? | 종료 방법? |
| :------- | :------- | :------- |
| 클라우드 녹화 | 방 입장 시 매개변수 `TRTCParams`의 `userDefineRecordId` 필드 지정   | 앵커 퇴장 시 자동 종료 |
| 클라우드 혼합 스트림 | SDK API [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출해 클라우드 혼합 스트림 실행 | 혼합 스트림을 요청한 앵커가 퇴장하면 자동 종료되거나 도중에 [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출한 후 매개변수를 `null/nil`로 설정해 수동 종료 |
| 릴레이 라이브 방송 | 방 입장 시 매개변수 `TRTCParams`의 `streamId` 필드 설정 | 앵커 퇴장 시 자동 종료 |

![](https://main.qcloudimg.com/raw/7daf8430ca74adeec019c10fc384a48e.gif)

- **콘솔 설정**
  본 녹화 방법을 사용하려면 콘솔의 [녹화 방식 선택](#recordType)에서 '특정 사용자 녹화'로 설정하십시오.

- **녹화 작업 시작**
  앵커 입장 시 방 입장 매개변수 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)의 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 필드를 지정하면 해당 앵커의 업스트림 멀티미디어 데이터가 클라우드에 녹화됩니다. 앵커가 해당 매개변수를 지정하지 않으면 녹화 작업이 트리거되지 않습니다.
<dx-codeblock>
::: Objective-C Objective-C
//예시 코드: 사용자 rexchang의 멀티미디어 스트림 지정 녹화, 파일 id: 1001_rexchang
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC의 SDKAppID, 애플리케이션 생성 후 획득
param.roomId   = 1001;           // 방 번호
param.userId   = @"rexchang";    // 사용자 이름
param.userSig  = @"xxxxxxxx";    // 로그인 서명
param.role     = TRTCRoleAnchor; // 역할: 앵커
param.userDefineRecordId = @"1001_rexchang";  // 녹화 ID, 해당 사용자의 녹화 활성화 지정
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVE 모드 사용
:::
</dx-codeblock>

- **녹화 작업 종료**
  방 입장 중 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce)를 설정한 앵커가 오디오/비디오 전송을 중지하면 작업이 자동으로 중지됩니다. 단, [녹화 파일 형식 선택](#fileFormat) 시 ‘재개 타임아웃’ 매개변수를 설정한 경우 타임아웃 시간이 경과할 때까지 녹화 파일을 수신하지 않습니다.

- **스트림 혼합**
  SDK API  [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출하여 방에 있는 다른 사용자의 오디오/비디오 스트림을 현재 사용자의 오디오/비디오 스트림과 혼합할 수 있습니다.
>! TRTC 방에서 한 앵커(라이브 방송을 시작한 앵커 권장)가 `setMixTranscodingConfig`를 호출하면 됩니다. 여러 앵커가 호출할 경우 충돌 오류가 발생할 수 있습니다.

- **녹화 파일 이름 생성**
  녹화 파일 이름은 `userDefineRecordId_시작 시간_종료 시간` 포맷으로 생성됩니다.

- **현재 지원 플랫폼**
  녹화 작업은 [iOS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [Mac](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html) 및 [Web](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)에서 시작할 수 있지만 현재 WeChat Mini Program에서는 시작할 수 없습니다.

[](id:recordRESTAPI)

### 방법3: 특정 사용자 녹화(REST API)

TRTC의 서버는 한 세트의 REST API([StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)와 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760))를 제공하여 클라우드 혼합 스트림, 클라우드 녹화, 릴레이 라이브 방송 세 가지 기능을 실행할 수 있습니다.

| 클라우드 기능 | 시작 방법  | 종료 방법 |
| :------- | :------- | :------- |
| 클라우드 녹화 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.RecordId` 매개변수를 지정하여 녹화 시작 | 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 종료 |
| 클라우드 혼합 스트림 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `LayoutParams` 매개변수를 지정하여 레이아웃 템플릿 및 레이아웃 매개변수 설정 | 모든 사용자 퇴장 후 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 수동 종료 |
| 릴레이 라이브 방송 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.StreamId` 매개변수를 지정하여 CDN 릴레이 라이브 방송 실행 | 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 종료 |

>? REST API 세트는 TRTC 클라우드 서비스에서 핵심 혼합 스트림 모듈인 MCU를 제어하고, MCU의 혼합 스트림 결과를 녹화 시스템과 라이브 방송 CDN에 전송하기 때문에 API는 `Start/StopMCUMixTranscode`라고 불립니다. 따라서 기능적 측면에서 보면 `Start/StopMCUMixTranscode`는 혼합 스트림 기능뿐 아니라 클라우드 녹화 및 릴레이 라이브 방송의 CDN 기능까지 구현합니다.

![](https://main.qcloudimg.com/raw/65ef546c0e424af77f7d20f23aa1d363.gif)

- **콘솔 설정**
  본 녹화 방법을 사용하려면 콘솔의 [녹화 방식 선택](#recordType)에서 '특정 사용자 녹화'로 설정하십시오.

- **녹화 작업 시작**
  서버에서 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)를 호출한 후 `OutputParams.RecordId` 매개변수를 지정하면 혼합 스트림 및 녹화를 실행할 수 있습니다.
```
// 코드 예시: REST API로 클라우드 혼합 스트림 및 클라우드 녹화 작업 실행
https://trtc.tencentcloudapi.com/?Action=StartMCUMixTranscode
&SdkAppId=1400000123
&RoomId=1001
&OutputParams.RecordId=1400000123_room1001
&OutputParams.RecordAudioOnly=0
&EncodeParams.VideoWidth=1280
&EncodeParams.VideoHeight=720
&EncodeParams.VideoBitrate=1560
&EncodeParams.VideoFramerate=15
&EncodeParams.VideoGop=3
&EncodeParams.BackgroundColor=0
&EncodeParams.AudioSampleRate=48000
&EncodeParams.AudioBitrate=64
&EncodeParams.AudioChannels=2
&LayoutParams.Template=1
&<공통 요청 매개변수>
```

>! 
>- REST API는 방 안에 최소 1명 이상의 사용자가 입장(enterRoom)해야만 적용됩니다.
>- REST API는 단일 스트림 녹화는 지원하지 않으며, 단일 스트림 녹화가 필요한 경우 [방법1](#autoRecord) 또는 [방법2](#recordSDKAPI)를 선택하십시오.

- **녹화 작업 종료**
  자동 종료되며, 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 혼합 스트림과 녹화 작업을 종료할 수도 있습니다.

- **다중 화면 혼합**
  [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `LayoutParams` 매개변수를 설정하면 클라우드 혼합 스트림이 실행됩니다. 해당 API는 전체 라이브 방송 시간 동안 여러 번 호출하여 필요에 따라 `LayoutParams` 매개변수를 수정하거나 혼합 화면 레이아웃을 변경할 수 있습니다. 단, 여러 번 호출 시 매개변수 `OutputParams.RecordId`와 `OutputParams.StreamId`는 항상 동일해야 하며, 동일하지 않을 경우 스트림이 중단되어 여러 개의 녹화 파일이 생성될 수 있습니다.



- **녹화 파일 이름 생성**
  녹화 파일 이름은 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 지정한 `OutputParams.RecordId` 매개변수에 따라 생성되며, `OutputParams.RecordId_시작 시간_종료 시간` 포맷으로 생성됩니다.

- **현재 지원 플랫폼**
  사용자의 서버에서 제어되며 클라이언트 플랫폼의 제한을 받지 않습니다.

[](id:search)
## 녹화 파일 검색

녹화 기능을 활성화하면 TRTC 시스템에서 녹화한 파일은 Tencent Cloud VOD 플랫폼에서 확인할 수 있습니다. VOD 콘솔에서 직접 검색하거나 백그라운드 서버에서 REST API를 사용하여 시간대별로 필터링할 수 있습니다.

#### 방법1: VOD 콘솔에서 파일 검색
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/)에 로그인한 후 왼쪽 사이드바에서 **미디어 자산 관리**를 선택합니다.
2. 목록 위의 **접두사로 검색**을 클릭하고 **접두사로 검색**을 선택한 후 키워드를 입력합니다. 검색 상자에 `1400000123_1001_rexchang_main`을 입력하고 <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">을(를) 클릭하면 이름이 일치하는 파일이 표시됩니다.
3. 생성 시간별로 파일을 필터링할 수도 있습니다.

#### 방법2: VOD의 REST API를 통해 검색
Tencent Cloud VOD 시스템은 멀티미디어 파일 관리를 위한 일련의 REST API를 제공합니다. [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)의 REST API를 통해 VOD 시스템 상의 파일을 검색할 수 있습니다. 요청 매개변수 표에 있는 `Text` 매개변수로 퍼지 매칭하거나 `StreamId` 매개변수로 정확한 검색을 진행할 수도 있습니다.
REST 요청 예시:
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<공통 요청 매개변수>
```

[](id:callback)

## 녹화 파일 수신

[녹화 파일 검색](#search) 외에도 콜백 주소 설정을 통해 Tencent Cloud에서 신규 녹화 파일 정보를 사용자 서버로 전송하도록 설정할 수 있습니다.
방 안의 마지막 멀티미디어 스트림 사용자가 퇴장하면 Tencent Cloud에서 녹화를 종료하고 파일을 VOD 플랫폼에 저장하며, 이 과정은 약 30초~2분 정도 소요됩니다. 지속 녹화 시간을 300초로 설정한 경우 기본 시간에 300초를 더한 시간이 소요됩니다. 저장 완료 후 Tencent Cloud는 [녹화 콜백 설정](#recordCallback)에서 설정한 콜백 주소(HTTP/HTTPS)를 통해 사용자 서버로 공지를 발송합니다.

녹화 및 녹화 관련 이벤트는 설정한 콜백 주소를 통해 Tencent Cloud에서 사용자의 서버로 전송됩니다. 다음은 콜백 정보 예시입니다.
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
다음 테이블의 필드로 콜백하려는 통화(또는 라이브 방송)를 확인할 수 있습니다.

<table>
<tr>
<th>시리얼 넘버</th><th>필드명</th><th>설명</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>정보 유형이며, event_type이 100인 경우 해당 콜백 정보는 녹화 파일 생성 정보를 의미합니다.</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>라이브 방송 CDN의 streamId로, 방 입장 시 TRTCParams의 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> 필드를 설정해 지정하거나(권장), TRTCCloud의 startPublishing 인터페이스 호출 시 streamId 매개변수를 통해 지정할 수 있습니다.</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>사용자 이름의 Base64 인코딩</td>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>사용자 정의 필드이며, TRTCParams의 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> 필드를 설정해 지정할 수 있습니다.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>녹화 파일의 시청 주소이며, <a href="#play">VOD 재생</a>에 사용할 수 있습니다.</td>
</tr></table>

>? 콜백의 더 많은 필드는 [CSS-녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38082)을 참고하십시오.


[](id:delete)
## 녹화 파일 삭제

Tencent Cloud VOD 시스템은 멀티미디어 파일 관리를 위한 REST API를 제공합니다. [DeleteMedia](https://intl.cloud.tencent.com/document/product/266/37571)를 통해 지정한 파일을 삭제할 수 있습니다.
REST 요청 예시:
```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<공통 요청 매개변수>
```

[](id:play)
## 녹화 파일 재생

온라인 교육 등 시나리오의 경우, 보통 라이브 방송이 종료된 후에도 학습 자료의 활용을 위해 녹화 파일을 반복적으로 재생하게 됩니다.

#### 파일 포맷 선택(HLS)
[녹화 포맷 설정](#fileFormat)에서 파일 포맷을 HLS로 선택하십시오.
HLS는 최대 30분의 중단 시간 지속 녹화를 지원하여 '라이브 방송 1회(또는 1교시)당 1개의 재생 링크 생성'을 할 수 있습니다. 또한 HLS 파일은 대다수의 브라우저에서의 온라인 재생을 지원해 비디오 재생 시나리오에 매우 적합합니다.

#### VOD 주소(video_url) 획득
[녹화 파일 수신](#callback) 시 콜백 정보의 **video_url** 필드를 가져올 수 있으며, 해당 필드는 해당 녹화 파일의 Tencent Cloud VOD 주소입니다.

#### VOD 플레이어 연결
사용하는 플랫폼에 따라 VOD 플레이어를 연결하는 방법은 다음과 같습니다.
- [iOS 플랫폼](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__ios.html)
- [Android 플랫폼](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html)
- [Web 브라우저](https://intl.cloud.tencent.com/document/product/266/33977)

>! [Superplayer(Player+)](https://intl.cloud.tencent.com/document/product/266/7836), MLVB(Mobile Live Video Broadcasting) 기능 등을 통합한 [TRTC Professional](https://intl.cloud.tencent.com/document/product/647/34615)을 사용하는 것이 좋습니다. 이 통합 버전은 많은 기본 모듈이 서비스 간에 공유되기 때문에 두 개의 독립 SDK보다 애플리케이션 패키지의 크기를 더 적게 추가합니다. 또한 중복 기호(symbol duplicate) 문제를 방지할 수 있습니다.


## 관련 요금
클라우드 녹화 및 재생 기능은 온클라우드 녹화 및 VOD의 저장, 비디오 처리 및 재생 서비스를 포함한 클라우드 서비스에서 제공됩니다. 또한 모바일 SDK의 플레이어 기능에 의존합니다.

### 클라우드 서비스 요금
클라우드 서비스 요금에는 클라우드에 동영상을 녹화하고 녹화 파일을 재생하는 데 드는 비용이 포함됩니다.

>?본 문서의 가격은 예시이며 참고용으로만 제공됩니다. 실제와 금액이 상이한 경우 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385), [Cloud Streaming Services](https://buy.intl.cloud.tencent.com/pricing/css), [Video on Demand](https://buy.intl.cloud.tencent.com/pricing/vod)의 가격을 기준으로 합니다.


- **녹화 요금: 트랜스 코딩 또는 리먹싱 컴퓨팅 비용**
녹화 중 오디오/비디오 스트림을 트랜스 코딩하거나 리먹싱하려면 서버 컴퓨팅 리소스가 필요하기 때문에 녹화에 사용된 컴퓨팅 리소스에 따라 녹화 요금이 부과됩니다.
>!
> - 2020년 7월 1일 이후 처음으로 TRTC 애플리케이션을 생성한 Tencent Cloud 계정의 경우, [클라우드 녹화 과금](https://cloud.tencent.com/document/product/647/45892)에 설명된 대로 클라우드 녹화 요금이 부과됩니다.
> - 2020년 7월 1일 이전에 애플리케이션을 생성한 Tencent Cloud 계정에는 녹화 서비스 사용에 대한 **라이브 녹화** 요금이 계속 부과됩니다.
>
**실시간 녹화** 요금은 최대 동시 녹화 채널 수를 기준으로 산정됩니다. 숫자가 높을수록 수수료가 높아집니다. 자세한 내용은 [CSS > 라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/39605)를 참고하십시오.
> 1000개의 앵커가 있고 피크 시간에는 500개의 앵커의 오디오/비디오 스트림을 동시에 녹화해야 한다고 가정합니다. 서비스 가격이 채널당 월 5.2941 USD인 경우 `500개 채널 x 5.2941 USD/채널/월 = 2647.05 USD/월`이 청구됩니다.
> 2가지 [파일 형식](https://intl.cloud.tencent.com/document/product/647/35426)을 선택하면 녹화 비용과 스토리지 비용이 2배가 됩니다. 3개를 선택하면 3배가 됩니다. 비용을 줄이려면 하나의 파일 형식만 선택하는 것이 좋습니다.

- **트랜스 코딩 요금: On-Cloud 혼합 트랜스 코딩 사용 시 부과**
스트림 믹싱에는 인코딩 및 디코딩이 포함되므로 On-Cloud 혼합 트랜스 코딩을 활성화하면 추가 트랜스 코딩 요금이 부과됩니다. 수수료는 사용된 해상도와 트랜스 코딩 기간에 따라 다릅니다. 앵커에 사용되는 더 높은 해상도와 더 긴 공동 앵커(On-Cloud 혼합 트랜스 코딩에 대한 가장 일반적인 애플리케이션 시나리오)가 지속되면 비용이 높아집니다. 자세한 내용은 [라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.
> [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)를 호출하여 앵커의 비트 레이트(videoBitrate)를 1500Kbps로, 해상도를 720p로 설정하고 앵커가 [클라우드 혼합 스트리밍 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)이 활성화된 1시간 동안 시청자와 공동 앵커되었다고 가정합니다. 발생하는 트랜스 코딩 비용은 '0.0057 USD/분 x 60 분 = 0.342 USD'입니다.

- **스토리지 비용: VOD로 파일 보관 시 발생**
저장에는 디스크 리소스가 필요하기 때문에 VOD로 녹화 파일을 저장할 경우 사용된 디스크 리소스에 따라 저장 요금이 부과됩니다. 파일을 오래 저장할수록 비용이 높아집니다. 비용을 줄이려면 가능한 한 저장 기간을 짧게 유지하거나 자신의 서버에 녹음 파일을 저장하는 것이 좋습니다. 스토리지 요금은 [사용량 과금(후불 일 결산)](https://intl.cloud.tencent.com/document/product/266/14666)으로 청구됩니다.
>예를 들어, [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)을 통해 앵커의 비트 레이트(videoBitrate)를 1000kbps로 설정하고 해당 앵커의 라이브 방송 비디오(파일 포맷 한 가지 선택)를 1시간 동안 녹화하는 경우, `(1000 / 8)KBps × 3600 초 = 450000 KB = 0.45 GB` 크기의 비디오 파일이 생성되며 해당 파일로 인해 매일 발생하는 스토리지 요금은 약 `0.45 GB × 0.0009 USD/GB/일 = 0.000405 USD`입니다.

- **재생 요금**: 파일 재생에 대한 요금**
녹화 파일 재생은 VOD의 CDN 재생 기능에 의존하며 CDN 트래픽을 소비합니다. 기본적으로 비디오 가속 요금은 재생에 사용된 트래픽에 따라 부과됩니다. 서비스 대상이 많을수록 비용이 높아집니다. 재생 요금은 [사용량 과금(후불 일 결산)](https://intl.cloud.tencent.com/document/product/266/14666)으로 청구됩니다.
>클라우드에 1GB 파일을 기록하고 처음부터 끝까지 1000명의 사용자에게 재생했다고 가정합니다. 트래픽 소모량은 1TB이며, VOD의 차등 요금제에 따르면 `1000 x 1 GB x 0.0794 USD/GB = 79.4 USD`의 요금이 부과됩니다.
> Tencent Cloud에서 서버로 파일을 다운로드하면 상대적으로 적은 양의 트래픽도 소비되며 월 단위로 청구됩니다.

### 플레이어 License
TRTC Professional은 CDN으로 릴레이된 녹음 파일과 스트림을 재생할 수 있는 강력한 플레이어 기능을 제공합니다. 모바일 SDK를 사용 중이고 버전이 10.1 이상인 경우 플레이어 기능을 사용할 수 있는 License를 받으십시오.
> ! TRTC 내에서 재생하려면 License가 필요하지 않습니다.


## FAQ
#### 서버 측에서 스트림을 어떻게 녹화합니까?
서버 측 레코딩은 아직 상용화되지 않은 Linux용 SDK에 의존합니다. SDK에 대해 궁금한 사항이 있거나 사용을 원하시면 colleenyu@tencent.com 으로 연락주시기 바랍니다. 

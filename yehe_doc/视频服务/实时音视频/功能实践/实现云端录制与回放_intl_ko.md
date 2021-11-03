## 적용 시나리오
원격 교육, 뷰티 라이브 방송, 화상 회의, 원격 손해사정, 금융 업무 녹음 및 녹화, 온라인 진료와 같은 응용 시나리오에서는 증거 수집, 품질 검사, 심사, 파일 보관, 재생 등의 업무를 위해 영상 통화 또는 라이브 스트리밍 세션을 녹화 및 저장해야 하는 경우가 많습니다.

TRTC의 클라우드 녹화는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장할 수 있습니다.
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

방 안 여러 채널의 멀티미디어에 대해 먼저 [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/647/34618)을 진행한 후, 혼합된 멀티미디어 스트림을 한 파일로 녹화하는 방법도 있습니다.
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## 콘솔 가이드
[](id:open)

### 녹화 서비스 활성화
1. TRTC 콘솔에 로그인한 후 왼쪽 메뉴에서 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 선택합니다.
2. 타깃 애플리케이션 라인에서 [기능 설정]을 클릭하여 기능 설정 페이지로 이동합니다. 애플리케이션을 생성하지 않은 경우 [애플리케이션 생성]을 클릭하여 애플리케이션 이름을 입력하고 [확인]을 클릭하면 새로운 애플리케이션이 생성됩니다.
3. [클라우드 녹화 활성화] 오른쪽에 있는 <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png">를 클릭하면 클라우드 녹화 설정 페이지가 팝업됩니다.

[](id:recordType)

### 녹화 방식 선택

TRTC의 클라우드 녹화 서비스는 '전역 자동 녹화'와 '특정 사용자 녹화' 방식을 제공합니다.
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **전체 자동 녹화**
  TRTC 방별로 각 사용자의 멀티미디어 업스트림을 모두 자동 녹화합니다. 녹화 작업의 실행 및 중지 또한 자동으로 진행되므로 별도로 신경 쓸 필요가 없어 조작이 간단하고 사용이 편리합니다. 자세한 사용 방법은 [방법1: 전역 자동 녹화](#autoRecord)를 참고하십시오.

- **특정 사용자 녹화**
  일부 사용자의 멀티미디어 스트림을 지정하여 녹화할 수 있습니다. 클라이언트의 SDK API 또는 서버의 REST API를 이용해 제어할 수 있으며, 추가적인 개발 작업이 필요합니다. 자세한 사용 방법은 [방법2: 특정 사용자 녹화(SDK API)](#recordSDKAPI) 또는 [방법3: 특정 사용자 녹화(REST API)](#recordRESTAPI)를 참고하십시오.

[](id:fileFormat)

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
<td><ul style="margin:0"><li/>실제 비즈니스 수요에 따라 단일 비디오 파일의 최장 시간 제한을 설정할 수 있습니다. 최장 시간 제한을 초과하면 시스템에서 자동으로 비디오 파일을 분할하며, 단위는 분, 설정 가능 범위는 1~120입니다. <li/>[파일 유형]을 [HLS]로 설정한 경우, 단일 파일의 최장 시간 제한이 없으며, 해당 매개변수는 적용되지 않습니다.</td>
</tr>
<tr>
<td>파일 저장 기간(일)</td>
<td>실제 비즈니스 수요에 따라 비디오 파일을 VOD 플랫폼에 저장하는 기간을 설정할 수 있습니다. 단위는 일이며 설정 가능한 범위는 0~1500입니다. 기간이 만료되면 파일은 VOD 플랫폼에서 자동으로 삭제되고 복구할 수 없습니다. 0으로 설정하면 영구 저장됩니다.</td>
</tr>
<tr>
<td>지속 녹화 만료 시간(초)</td>
<td><li/>[파일 유형]을 [HLS]로 설정한 경우에만 해당 매개변수가 적용됩니다. <li/>일반적인 상황에서 네트워크 불안정 또는 기타 원인으로 통화(또는 라이브 방송)가 끊기는 경우 녹화 파일이 여러 개 파일로 분할됩니다. '통화(또는 라이브 방송)별로 1개의 재생 링크만 생성'하고 싶은 경우 실제 상황에 따라 지속 녹화 만료 시간을 설정할 수 있습니다. 통화가 끊긴 시간 간격이 설정한 지속 녹화 만료 시간보다 짧은 경우 통화(또는 라이브 방송)별로 파일이 1개만 생성됩니다. 단위는 초이며 설정 가능한 범위는 1~1800이고, 0으로 설정하면 끊긴 후 지속 녹화되지 않습니다.</td>
</tr>
</table>


>? HLS는 최대 30분까지 지속 녹화를 지원하여 '1교시당 1개의 재생 링크 생성'을 할 수 있습니다. 또한 대다수의 브라우저에서 온라인으로 시청할 수 있어 온라인 교육 시나리오의 비디오 재생 시나리오에 매우 적합합니다.

[](id:storageLocation)

### 저장 위치 선택

TRTC 클라우드 녹화 파일은 Tencent Cloud의 VOD 플랫폼에 저장되도록 기본 설정되어 있습니다. 만약 프로젝트에서 여러 비즈니스가 하나의 Tencent Cloud VOD 계정을 공유해서 사용하고 있다면 녹화 파일을 분리해서 저장해야 할 수 있습니다. Tencent Cloud VOD의 '서브 애플리케이션' 기능을 사용하면 TRTC 녹화 파일을 다른 비즈니스 파일과 분리하여 저장할 수 있습니다.

- **VOD 메인 애플리케이션과 서브 애플리케이션이란 무엇인가요?**
  메인 애플리케이션과 서브 애플리케이션은 일종의 VOD에서의 리소스 구분 방식입니다. 메인 애플리케이션은 VOD에서의 루트 계정이라고 볼 수 있으며, 서브 애플리케이션은 여러 개를 생성할 수 있고 루트 계정 하위에 있는 서브 계정이라고 볼 수 있습니다. 서브 애플리케이션은 독립적인 리소스 관리 권한을 가지며 스토리지 영역에서 다른 서브 애플리케이션과 상호 분리되어 있습니다.

- **VOD 서비스의 서브 애플리케이션은 어떻게 활성화하나요?**
  ['VOD 서브 애플리케이션 실행 방법'](https://intl.cloud.tencent.com/document/product/266/33987)에 따라 새로운 서브 계정을 추가할 수 있으며, 해당 방법은 VOD [콘솔](https://console.cloud.tencent.com/vod)로 이동하여 작업해야 합니다.

[](id:recordCallback)

###  녹화 콜백 설정
- **녹화 콜백 주소: **
  신규 파일 [생성 공지](#callback)를 실시간으로 받고 싶은 경우, 서버에서 녹화 파일 수신 콜백에 사용할 주소를 여기에 입력하십시오. 해당 주소는 HTTP(또는 HTTPS) 프로토콜에 부합해야 합니다. 신규 녹화 파일 생성 시 Tencent Cloud에서 해당 주소를 통해 귀하의 서버로 공지를 전송합니다.
![](https://main.qcloudimg.com/raw/9b9beab813d929a7a364eb2d8ab045ba.png)
	
- **녹화 콜백 키**
콜백 키는 콜백 이벤트 수신 시 서명 인증 생성에 사용됩니다. 해당 키는 알파벳 대소문자 및 숫자로 구성되며 최대 32자까지 입력할 수 있습니다. 사용 관련 자세한 내용은 [녹화 이벤트 매개변수 설명](https://intl.cloud.tencent.com/document/product/267/38082)을 참고하십시오.


>? 자세한 녹화 콜백 수신 및 해석 방법은 문서 후반부에 있는 [녹화 파일 수신](https://intl.cloud.tencent.com/document/product/647/35426)을 참고하십시오.



[](id:startAndStop)

## 녹화 제어 방법

TRTC는 [전역 자동 녹화](#autoRecord), [특정 사용자 녹화(SDK API 제어)](#recordSDKAPI), [특정 사용자 녹화(REST API 제어)](#recordRESTAPI)의 세 가지 클라우드 녹화 제어 방법을 제공합니다. 자세한 내용은 다음 설명을 참고하십시오.

- 해당 솔루션은 콘솔에서 어떻게 설정하나요?
- 녹화 작업은 어떻게 시작하나요?
- 녹화 작업은 어떻게 종료하나요?
- 방 안 여러 채널의 화면을 어떻게 한 채널로 혼합하나요?
- 녹화한 파일은 어떤 포맷으로 이름이 생성되나요?
- 해당 방법을 지원하는 플랫폼에는 어떤 것이 있나요?


[](id:autoRecord)

## 방법1: 전역 자동 녹화

- **콘솔 설정**
  본 녹화 방법을 사용하려면 콘솔의 [녹화 방식 선택](#recordType)에서 '전역 자동 녹화'로 설정하십시오.

- **녹화 작업 시작**
  TRTC는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장하며, 별도의 조작이 필요 없습니다.

- **녹화 작업 종료**
  자동으로 종료됩니다. 즉, 호스트가 멀티미디어 업스트림을 중단하면 해당 호스트의 클라우드 녹화가 자동으로 종료됩니다. [파일 포맷 선택](#fileFormat) 시 '지속 녹화 시간'을 설정했다면 지속 녹화 설정 시간이 지난 후 녹화 파일을 확인할 수 있습니다.

- **다중 화면 혼합**
  전역 자동 녹화 모드에서의 클라우드 혼합 스트림 방법은 '서버 REST API 방법'과 '클라이언트 SDK API 방법'이 있습니다. 두 방법은 동시에 사용할 수 없습니다.
  - [서버 REST API 혼합 스트림 방법](#recordRESTAPI): 사용자의 서버에서 API를 호출하며 클라이언트 플랫폼 버전에 제한을 받지 않습니다.
  - [클라이언트 SDK API 혼합 스트림 솔루션](#recordSDKAPI): 클라이언트에서 직접 혼합 스트림을 요청할 수 있습니다. iOS, Android, Windows, Mac, Electron 등 플랫폼을 지원하며, 현재 WeChat 미니프로그램 및 Web 브라우저는 지원되지 않습니다.

- **녹화 파일 이름 생성**
  - 호스트가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정한 경우, 녹화 파일 이름이 `userDefineRecordId_streamType_시작 시간_종료 시간` 형식으로(streamType에는 main, aux의 두 값이 있으며, main은 메인 채널, aux는 보조 채널을 의미하고 보조 채널은 일반적으로 화면 공유에 사용) 생성됩니다.
  - 호스트가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개 변수를 지정하지 않았으나 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 지정한 경우 녹화 파일 이름이 `streamId_시작 시간_종료 시간` 형식으로 생성됩니다.
  - 호스트가 방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수와 [streamId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 모두 지정하지 않은 경우, 녹화 파일 이름은`sdkappid_roomid_userid_streamType_시작 시간_종료 시간` 형식으로(streamType에는 main, aux의 두 가지 값이 있으며, main은 메인 채널, aux는 보조 채널을 의미하고 보조 채널은 일반적으로 화면 공유에 사용) 생성됩니다.

- **지원되는 플랫폼**
  사용자의 서버로 제어할 경우, 클라이언트 플랫폼의 제약을 받지 않습니다.

[](id:recordSDKAPI)

### 방법 2: 특정 사용자 녹화(SDK API)

TRTC SDK에서 제공하는 일부 API 인터페이스 및 매개변수를 호출하여 클라우드 혼합 스트림, 클라우드 녹화, 릴레이 라이브 방송의 세 가지 기능을 실행할 수 있습니다.

| 클라우드 기능 | 시작 방법? | 종료 방법? |
| :------- | :------- | :------- |
| 클라우드 녹화 | 방 입장 시 매개변수 `TRTCParams`의 `userDefineRecordId` 필드 지정   | 호스트 퇴장 시 자동 종료 |
| 클라우드 혼합 스트림 | SDK API [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출해 클라우드 혼합 스트림 실행 | 혼합 스트림을 요청한 호스트가 퇴장하면 자동 종료되거나 도중에 [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출한 후 매개변수를 `null/nil`로 설정해 수동 종료 |
| 릴레이 라이브 방송 | 방 입장 시 매개변수 `TRTCParams`의 `streamId` 필드 설정 | 호스트 퇴장 시 자동 종료 |

![](https://main.qcloudimg.com/raw/7daf8430ca74adeec019c10fc384a48e.gif)

- **콘솔에서 설정**
  본 녹화 방법을 사용하려면 콘솔의 [녹화 방식 선택](#recordType)에서 '특정 사용자 녹화'로 설정하십시오.

- **녹화 작업 시작**
  호스트 입장 시 방 입장 매개변수 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)의 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 필드를 지정하면 해당 호스트의 업스트림 멀티미디어 데이터가 클라우드에 녹화됩니다. 호스트가 해당 매개변수를 지정하지 않으면 녹화 작업이 트리거되지 않습니다.
<dx-codeblock>
::: Objective-C Objective-C
//예시 코드: 사용자 rexchang의 멀티미디어 스트림 지정 녹화, 파일 id: 1001_rexchang
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC의 SDKAppID, 애플리케이션 생성 후 획득
param.roomId   = 1001;           // 방 번호
param.userId   = @"rexchang";    // 사용자 이름
param.userSig  = @"xxxxxxxx";    // 로그인 서명
param.role     = TRTCRoleAnchor; // 역할: 호스트
param.userDefineRecordId = @"1001_rexchang";  // 녹화 ID, 해당 사용자의 녹화 활성화 지정
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVE 모드 사용
:::
</dx-codeblock>

- **녹화 작업 종료**
  방 입장 시 [userDefineRecordId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정한 호스트가 멀티미디어 업스트림을 중단하면 클라우드 녹화가 자동으로 종료됩니다. [파일 포맷 선택](#fileFormat) 시 '지속 녹화 시간'을 설정했다면 지속 녹화 설정 시간이 지난 후 녹화 파일을 확인할 수 있습니다.

- **다중 화면 혼합**
  SDK API [setMixTranscodingConfig()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) 호출을 통해 방 안에 있는 다른 사용자들의 화면과 음성을 현재 사용자의 멀티미디어 스트림 채널에 혼합할 수 있습니다. 자세한 설명은 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88) 문서를 참고하십시오.
>! TRTC 방에서 한 호스트(라이브 방송을 시작한 호스트 권장)가 `setMixTranscodingConfig`를 호출하면 됩니다. 여러 호스트가 호출할 경우 충돌 오류가 발생할 수 있습니다.

- **녹화 파일 이름 생성**
  녹화 파일 이름은 `userDefineRecordId_시작 시간_종료 시간` 포맷으로 생성됩니다.

- **현재 지원 플랫폼**
  [iOS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [Mac](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html) 등의 단말에서 요청하는 녹화 제어를 지원하며, 현재 Web 브라우저 및 WeChat 미니프로그램을 통한 제어는 지원되지 않습니다.

[](id:recordRESTAPI)

### 방법 3: 특정 사용자 녹화(REST API)

TRTC의 서버는 한 세트의 REST API([StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)와 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760))를 제공하여 클라우드 혼합 스트림, 클라우드 녹화, 릴레이 라이브 방송 세 가지 기능을 실행할 수 있습니다.

| 클라우드 기능 | 시작 방법  | 종료 방법 |
| :------- | :------- | :------- |
| 클라우드 녹화 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.RecordId` 매개변수를 지정하여 녹화 시작 | 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 종료 |
| 클라우드 혼합 스트림 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `LayoutParams` 매개변수를 지정하여 레이아웃 템플릿 및 레이아웃 매개변수 설정 | 모든 사용자 퇴장 후 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 수동 종료 |
| 릴레이 라이브 방송 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.StreamId` 매개변수를 지정하여 CDN 릴레이 라이브 방송 실행 | 자동 종료 또는 도중에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 종료 |

>? REST API 세트는 TRTC 클라우드 서비스에서 핵심 혼합 스트림 모듈인 MCU를 제어하고, MCU의 혼합 스트림 결과를 녹화 시스템과 라이브 방송 CDN에 전송하기 때문에 API는 `Start/StopMCUMixTranscode`라고 불립니다. 따라서 기능적 측면에서 보면 `Start/StopMCUMixTranscode`는 혼합 스트림 기능뿐 아니라 클라우드 녹화 및 릴레이 라이브 방송의 CDN 기능까지 구현합니다.

![](https://main.qcloudimg.com/raw/65ef546c0e424af77f7d20f23aa1d363.gif)

- **콘솔에서 설정**
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

>?클라우드 혼합 스트림에 대한 자세한 설명은 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618#restapi)을 참고하십시오.

- **녹화 파일 이름 생성**
  녹화 파일 이름은 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 지정한 `OutputParams.RecordId` 매개변수에 따라 생성되며, `OutputParams.RecordId_시작 시간_종료 시간` 포맷으로 생성됩니다.

- **현재 지원 플랫폼**
  사용자의 서버로 제어하며, 클라이언트 플랫폼의 제약을 받지 않습니다.

[](id:search)
## 녹화 파일 검색

녹화 기능을 활성화하면 TRTC 시스템에서 녹화한 파일은 Tencent Cloud VOD 플랫폼에서 확인할 수 있습니다. VOD 콘솔에서 직접 검색하거나 백그라운드 서버에서 REST API를 사용하여 시간대별로 필터링할 수 있습니다.

#### 방법1: VOD 콘솔에서 수동 검색
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/)에 로그인한 후 왼쪽 메뉴에서 [미디어 자원 관리]를 선택합니다.
2. 리스트 상단에 있는 [접두사 검색]을 클릭한 후, [접두사 검색]을 선택하고 검색창에 키워드(예: `1400000123_1001_rexchang_main`)를 입력한 다음 <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">를 클릭하면 비디오 이름의 접두사가 매칭되는 비디오 파일이 표시됩니다.
3. 생성 시간으로 타깃 파일을 필터링할 수도 있습니다.

#### 방법2: VOD의 REST API를 통해 검색
Tencent Cloud VOD 시스템은 멀티미디어 파일 관리를 위한 일련의 REST API를 제공합니다. [미디어 정보 검색](https://intl.cloud.tencent.com/document/product/266/34179)의 REST API를 통해 VOD 시스템 상의 파일을 검색할 수 있습니다. 요청 매개변수 표에 있는 `Text` 매개변수로 퍼지 매칭하거나 `StreamId` 매개변수로 정확한 검색을 진행할 수도 있습니다.
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



[](id:delete)
## 녹화 파일 삭제

Tencent Cloud VOD 시스템은 멀티미디어 파일 관리를 위한 REST API를 제공합니다. [미디어 삭제 API](https://intl.cloud.tencent.com/document/product/266/37571)를 통해 지정한 파일을 삭제할 수 있습니다.
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

>! [프로 버전](https://intl.cloud.tencent.com/document/product/647/34615) TRTC SDK의 사용을 권장합니다. 프로 버전은 [Player+](https://intl.cloud.tencent.com/document/product/266/7836)와 [Mobile Live Video Broadcasting](https://intl.cloud.tencent.com/product/mlvb) 등의 기능이 통합되어 있어 하위 레이어 모듈을 효율적으로 재사용해 증분 용량이 독립적인 SDK 2개를 통합한 용량보다 작고, 부호 충돌(symbol duplicate) 문제를 방지할 수 있습니다.


## 관련 요금

클라우드 녹화 및 재생과 관련한 요금 항목은 다음과 같습니다. 녹화 요금은 기본료이며, 기타 요금은 실제 사용 현황에 따라 과금합니다.

>?본 문서의 가격은 예시이며 참고용으로만 제공됩니다. 실제와 금액이 상이한 경우 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385), [Cloud Streaming Services](https://buy.intl.cloud.tencent.com/pricing/css), [Video on Demand](https://buy.intl.cloud.tencent.com/pricing/vod)의 가격을 기준으로 합니다.

#### 녹화 요금: 트랜스 코딩 또는 캡슐화로 발생하는 요금 계산

녹화는 멀티미디어 스트림 트랜스 코딩 또는 캡슐화 필요하며 서버의 컴퓨팅 리소스 소모가 발생합니다. 따라서 녹화 작업에 따른 컴퓨팅 리소스의 점유율에 대한 요금이 발생합니다.

>!
>- 2020년 7월 1일 이후 처음으로 TRTC 콘솔에서 애플리케이션을 생성한 Tencent Cloud 계정의 경우, 클라우드 녹화 기능 사용으로 발생하는 녹화 요금은 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)을 기준으로 합니다.
>- 2020년 7월 1일 이전에 TRTC 콘솔에서 애플리케이션을 생성한 Tencent Cloud 계정의 경우, 2020년 7월 1일 이전과 이후에 생성한 모든 애플리케이션에서 클라우드 녹화 기능 사용으로 발생하는 녹화 요금은 기본적으로 **라이브 방송 녹화** 계속 사용 과금 규정을 적용합니다.

**라이브 방송 녹화**는 동시 녹화 채널 수에 따라 요금이 계산되며, 동시 접속 수가 많을수록 요금도 증가합니다. 자세한 과금 설명은 [CSS>라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/39605)를 참고하십시오.

>예를 들어 현재 1000명의 호스트를 보유하고 있고 저녁 피크 시간에 최대 500개 채널의 호스트 멀티미디어 스트림을 동시 녹화해야 하는 경우, 녹화 단가가 5.2941USD/채널/월이라고 가정한다면 총 녹화 요금은 `500개 채널×5.2941USD/채널/월=2647.05USD/월`입니다.
>[녹화 포맷 설정](#fileFormat)에서 녹화 파일 포맷 2개를 선택한 경우 녹화 요금과 스토리지 요금은 두 배(×2)가 되며, 파일 포맷 3개를 선택한 경우 녹화 요금 및 스토리지 요금은 세 배(×3)가 됩니다. 반드시 필요한 경우가 아니라면 비용을 대폭 절약할 수 있도록 한 가지 파일 포맷만 선택할 것을 권장합니다.

**스토리지 요금: 파일을 Tencent Cloud에 저장하는 경우 해당 요금 발생**
녹화한 파일을 Tencent Cloud에 저장하는 경우, 저장으로 인해 디스크 리소스가 소모되므로 저장하는 리소스 용량에 따라 요금이 발생합니다. 저장 시간이 길수록 요금 또한 증가하므로 특별하게 필요한 경우가 아니라면 파일 저장 기간을 짧게 설정하여 비용을 절약할 수 있습니다. 또는 파일을 사용자 서버에 저장할 수도 있습니다. 스토리지 요금은 [비디오 스토리지(일 결산) 가격](https://intl.cloud.tencent.com/document/product/266/14666)에서 일 단위로 결산할 수 있습니다.

>예를 들어, [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)을 통해 호스트의 비트 레이트(videoBitrate)를 1000kbps로 설정하고 해당 호스트의 라이브 방송 비디오(파일 포맷 한 가지 선택)를 1시간 동안 녹화하는 경우, `(1000 / 8)KBps×3600초=450000KB=0.45GB` 크기의 비디오 파일이 생성되며 해당 파일로 인해 매일 발생하는 스토리지 요금은 약 `0.45GB×0.0009USD/GB/일=0.000405USD`입니다.

#### 시청 요금: 파일을 VOD 시청에 사용하는 경우 해당 요금 발생

녹화한 파일을 VOD 시청에 사용하는 경우, VOD 시청으로 인해 CDN 트래픽 소모가 발생합니다. 따라서 VOD 가격에 따라 요금이 발생하며 기본적으로 트래픽에 따라 과금됩니다. 시청하는 사람이 많을수록 요금이 증가하며, 시청 요금은 [비디오 가속(일 결산) 가격](https://intl.cloud.tencent.com/document/product/266/14666)에서 일 단위로 결산할 수 있습니다.

>예를 들어, 클라우드 녹화를 통해 1GB 크기의 파일을 생성하고 1000명의 시청자가 동영상을 처음부터 끝까지 모두 시청하였을 경우 약 1TB의 VOD 시청 트래픽이 발생합니다. 차등 가격표에 따라 계산하면 1000명의 시청자에게 `1000×1GB×0.0794USD/GB=79.4USD`의 요금이 발생합니다.
>Tencent Cloud에서 귀하의 서버로 파일을 다운로드할 때도 소량의 VOD 트래픽이 발생하며, 월 청구서에 기재됩니다.

#### 트랜스 코딩 요금: 혼합 스트림 녹화를 활성화하는 경우 해당 요금 발생

혼합 스트림 녹화를 활성화하면 스트림 혼합을 위해 디코딩과 인코딩이 진행되고, 이에 따른 별도의 혼합 스트림 트랜스 코딩 요금이 발생합니다. 혼합 스트림 트랜스 코딩은 해상도 크기와 트랜스 코딩 시간에 따라 과금되며, 호스트가 채택한 해상도가 높고, 마이크 연결 시간(보통 마이크 연결 시 혼합 스트림 트랜스 코딩 필요)이 길수록 요금이 증가합니다. 자세한 요금 계산법은 [라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/document/product/267/39604)을 참고하십시오.

>예를 들어, [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)을 통해 호스트의 비트 레이트(videoBitrate)를 1500kbps로, 해상도를 720P로 각각 설정한 상태에서 호스트가 시청자와 1시간 동안 마이크를 연결해 인터랙션했다면 마이크 연결 시간 동안 [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/647/34618)이 활성화되고, 이에 따라 `0.0057 USD/분×60분=0.342USD` 의 트랜스 코딩 요금이 발생합니다.

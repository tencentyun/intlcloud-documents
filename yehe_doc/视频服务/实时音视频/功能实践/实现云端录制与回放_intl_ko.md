## 적용 시나리오

원격 교육, 쇼 라이브 방송, 화상 회의, 원격 점검, 금융 녹음 및 녹화, 온라인 진료 등의 응용 시나리오에서는 증거 수집, 자격 인증, 심사, 저장, 재생 등의 수요로 인해 전체 영상 통화 또는 대화형 라이브 방송을 녹화 및 저장이 필요합니다.

TRTC의 클라우드 녹화는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장할 수 있습니다.
![](https://main.qcloudimg.com/raw/7820cdafe40fabc38653bc53795412d2.png)

방 안 여러 채널의 멀티미디어에 대해 먼저 [클라우드 혼합 스트리밍](https://intl.cloud.tencent.com/document/product/647/34618)을 진행한 후, 다시 혼합된 멀티미디어 스트림을 한 파일로 녹화하는 방법도 있습니다.
![](https://main.qcloudimg.com/raw/2f92f978c2ca76d001891e645905e8f9.png)

## 콘솔 가이드

<span id="open"></span>
### 녹화 서비스 활성화

1.TRTC 콘솔에 로그인한 후 왼쪽 메뉴에서 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)를 선택합니다.
2. 대상 애플리케이션이 있는 라인의 [기능 설정]을 클릭하여 기능 설정 페이지로 이동합니다. 애플리케이션을 생성하지 않은 상태인 경우 [애플리케이션 생성]을 클릭하여 애플리케이션 이름을 입력하고 [확인]을 클릭하면 새로운 애플리케이션이 생성됩니다.
3. [클라우드 녹화 활성화] 오른쪽에 있는 <img src="https://main.qcloudimg.com/raw/3fc81b259baa4edf112af2f570e6d97f.png"  style="margin:0;">을 클릭하면 클라우드 녹화 설정 페이지가 팝업됩니다.

<span id="recordType"></span>

### 녹화 방식 선택

TRTC의 클라우드 녹화 서비스는 "전체 자동 녹화"와 "특정 사용자 녹화" 두 가지 녹화 방식을 제공합니다.
![](https://main.qcloudimg.com/raw/d8084b7aa472b95ec21448703e4b6a49.png)

- **전체 자동 녹화**
  TRTC 방별로 각 사용자가 업스트리밍한 멀티미디어 스트리밍을 모두 자동 녹화합니다. 녹화 작업의 시작 및 중지 또한 모두 자동으로 진행되므로 별도로 신경 쓸 필요가 없어 조작이 간단하고 사용이 편리합니다. 자세한 사용 방법은 [방법1: 전체 자동 녹화](#autoRecord)를 참조하십시오.

- **특정 사용자 녹화**
  일부 사용자의 멀티미디어 스트리밍을 지정하여 녹화할 수 있습니다. 클라이언트의 SDK API 또는 서버의 REST API를 이용해 제어할 수 있으며, 추가적인 개발 작업이 필요합니다. 자세한 사용 방법은 [방법2: 특정 사용자 녹화(SDK API)](#recordSDKAPI) 또는 [방법3: 특정 사용자 녹화(REST API)](#recordRESTAPI)를 참조하십시오.

<span id="fileFormat"></span>

###  파일 포맷 선택
클라우드 녹화는 HLS, MP4, FLV, AAC의 네 가지 파일 포맷을 지원하며 비즈니스 수요에 따라 선택할 수 있습니다. 해당 포맷별 차이점 및 적용 시나리오는 아래 표를 참고하십시오.

<table>
<tr><th>매개변수</th><th>매개변수 설명</th></tr>
<tr>
<td>파일 유형</td>
<td>다음과 같은 파일 유형을 지원합니다.<ul style="margin:0"><li><b>HLS</b>: 대부분의 브라우저에서 온라인 재생을 지원하며, 비디오 재생 시나리오에 적합합니다. 또한 중단된 시점부터 계속 녹화가 가능하며 단일 파일 최장 시간 제한이 없습니다.</li><li><b>FLV</b>: 브라우저에서 온라인 재생을 지원하지 않으나 파일 크기가 작고 오류 발생률이 적습니다. 녹화 파일을 VOD 플랫폼에 저장할 필요가 없는 경우 해당 파일 유형을 선택할 수 있으며, 녹화 완료 후 바로 녹화 파일이 다운로드되고 원본 파일은 삭제됩니다.</li><li><b>MP4</b>: Web 브라우저에서 온라인 재생을 지원합니다. 그러나 해당 포맷은 오류 발생률이 높아 영상 통화 중 패킷 손실이 발생할 경우 최종 파일의 재생 품질에 영향을 줍니다.</li><li><b>AAC</b>: 오디오 녹음만 필요한 경우 해당 파일 유형을 선택할 수 있습니다.</li></td>
</tr>
<tr>
<td nowrap="nowrap">단일 파일 최장 시간(분)</td>
<td><ul style="margin:0"><li/>실제 비즈니스 수요에 따라 단일 비디오 파일의 최장 시간 제한을 설정할 수 있습니다. 최장 시간 제한을 초과하면 시스템에서 자동으로 비디오 파일을 분할합니다. 단위는 분이며 설정 가능한 범위는 5 - 120입니다.<li/>[문서 유형]을 [HLS]로 설정하는 경우 단일 파일의 최장 시간 제한이 없으며, 해당 매개변수는 적용되지 않습니다.</td>
</tr>
<tr>
<td>파일 저장 기간(일)</td>
<td>실제 비즈니스 수요에 따라 비디오 파일을 VOD 플랫폼에 저장하는 기간을 설정할 수 있습니다. 단위는 일이며 설정 가능한 범위는 0 - 1080입니다. 기간이 만료되면 파일은 VOD 플랫폼에서 자동으로 삭제되며 다시 복구할 수 없습니다. 0으로 설정하면 영구 저장됩니다.</td>
</tr>
<tr>
<td>지속 녹화 만료 시간(초)</td>
<td><li/>[파일 유형]을 [HLS]로 설정한 경우에만 해당 매개변수가 적용됩니다.<li/>기본적으로 통화(또는 라이브 방송) 중 네트워크 변동 또는 기타 이유로 스트리밍이 끊기는 경우 녹화 파일이 여러 개 파일로 분할됩니다. "통화(또는 라이브 방송)별로 1개의 재생 링크만 생성"하고 싶은 경우 실제 상황에 따라 지속 녹화 만료 시간을 설정할 수 있습니다. 스트리밍이 끊긴 시간 간격이 설정한 지속 녹화 만료 시간보다 작은 경우 통화(또는 라이브 방송)별로 파일이 1개만 생성됩니다. 단위는 초이며 설정 가능한 범위는 1 - 1800이고, 0으로 설정하는 경우 스트리밍이 끊긴 후 지속 녹화하지 않습니다.</td>
</tr>
</table>

>? HLS는 최대 30분까지 지속 녹화를 지원하여 "1교시당 1개의 재생 링크 생성"을 할 수 있습니다. 또한 대다수의 브라우저에서 온라인으로 시청할 수 있어 온라인 교육 시나리오의 비디오 재생 시나리오에 매우 적합합니다.

<span id="storageLocation"></span>

###  저장 위치 선택

TRTC 클라우드 녹화 파일은 Tencent Cloud의 VOD 플랫폼에 저장되도록 기본 설정되어 있습니다. 만약 프로젝트에서 여러 비즈니스가 하나의 Tencent Cloud VOD 계정을 공유해서 사용하고 있다면 녹화 파일을 분리해 저장해야 할 수 있습니다. Tencent Cloud VOD의 "서브 애플리케이션" 기능을 사용하면 TRTC 녹화 파일을 다른 비즈니스 파일과 분리하여 저장할 수 있습니다.

- **VOD 메인 애플리케이션과 서브 애플리케이션이란 무엇인가요?**
  메인 애플리케이션과 서브 애플리케이션은 일종의 VOD에서의 리소스 구분 방식입니다. 메인 애플리케이션은 VOD에서의 루트 계정이라고 볼 수 있으며, 서브 계정은 여러 개를 생성할 수 있고 루트 계정 하위에 있는 서브 계정이라고 볼 수 있습니다. 서브 계정은 독립적인 리소스 관리 권한을 가지며 스토리지 영역에서 다른 서브 계정과 상호 분리되어 있습니다.

- **VOD 서비스의 서브 애플리케이션은 어떻게 활성화하나요?**
  문서 ["VOD 서브 애플리케이션은 어떻게 활성화합니까"](https://intl.cloud.tencent.com/document/product/266/33987)에 따라 새로운 서브 계정을 추가할 수 있으며, 해당 방법은 VOD [콘솔](https://console.cloud.tencent.com/vod)로 이동하여 작업해야 합니다.

<span id="recordCallback"></span>

###  녹화 콜백 설정

신규 파일 [생성 알림](#callback)을 실시간으로 수신하고 싶은 경우 이 곳에 서버에서 녹화 파일 콜백에 사용한 주소를 입력하십시오. 해당 주소에는 HTTP(또는 HTTPS) 프로토콜에 부합해야 합니다. 신규 녹화 파일 생성 시 Tencent Cloud에서 해당 주소를 통해 사용자의 서버로 알림을 전송합니다.

![](https://main.qcloudimg.com/raw/9b9beab813d929a7a364eb2d8ab045ba.png)

녹화 콜백 수신 및 솔루션에 대한 자세한 내용은 [녹화 파일 수신](#callback) 문서 후반부를 참조하십시오.

<span id="startAndStop"></span>

## 녹화 제어 방법
TRTC는 [전체 자동 녹화](#autoRecord), [특정 사용자 녹화(SDK API 제어)](#recordSDKAPI), [특정 사용자 녹화(REST API 제어)](#recordRESTAPI)의 세 가지 클라우드 녹화 제어 방법을 제공합니다. 자세한 내용은 다음 설명을 참조하십시오.

- 해당 방법은 콘솔에서 어떻게 설정하나요?
- 녹화 작업은 어떻게 시작하나요?
- 녹화 작업은 어떻게 종료하나요?
- 방 안의 여러 채널의 화면을 어떻게 한 채널로 혼합하나요?
- 녹화한 파일은 어떤 형식으로 이름이 생성되나요?
- 해당 방법을 지원하는 플랫폼에는 어떤 것이 있나요?

<span id="autoRecord"></span>

### 방법1: 전체 자동 녹화
- **콘솔에서 설정**
  콘솔에서 [녹화 방식 선택](#recordType) 시 "전체 자동 녹화"로 설정하면 됩니다.
  
- **녹화 작업 시작**
  TRTC는 방 안 모든 사용자의 멀티미디어 스트림을 하나의 독립된 파일로 저장하며, 별도의 조작이 필요 없습니다.
  
- **녹화 작업 종료**
  자동으로 종료됩니다. 즉, 호스트가 멀티미디어 업스트리밍을 중단하면 해당 호스트의 클라우드 녹화가 자동으로 종료됩니다. [파일 포맷 선택]((#fileFormat) 시 "지속 녹화 시간"을 설정했다면 지속 녹화 설정 시간이 지난 후 녹화 파일을 확인할 수 있습니다.
  
- **다중 화면 혼합**
  전체 자동 녹화 모드에서 클라우드 혼합 스트리밍을 하는 방법은 "서버 REST API 방법"과 "클라이언트 SDK API 방법" 두 가지가 있습니다. 두 방법을 동시에 사용하지 마십시오.
  - [서버 REST API 혼합 스트리밍 방법](#recordRESTAPI): 사용자의 서버에서 API를 호출하며 클라이언트 플랫폼 버전에 제한을 받지 않습니다.
  - [클라이언트 SDK API 혼합 스트리밍 방법](#recordSDKAPI): 클라이언트에서 직접 혼합 스트리밍을 요청합니다. iOS, Android, Windows, Mac, Electron 등을 지원하며, 현재는 Web 브라우저는 지원하지 않습니다.

- **녹화 파일 이름 생성**
  - 호스트가 방 입장 시 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정한 경우 녹화 파일 이름이 `userDefineRecordId_시작 시간_종료 시간` 형식으로 생성됩니다.
  - 호스트가 방 입장 시 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개 변수를 지정하지 않았으나 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 지정한 경우 녹화 파일 이름이 `streamId_시작 시간_종료 시간` 형식으로 생성됩니다.
  - 호스트가 방 입장 시 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수와 [streamId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167) 매개변수를 모두 지정하지 않은 경우 녹화 파일 이름이`sdkappid_roomid_userid_시작 시간_종료 시간` 형식으로 생성됩니다.

- **지원되는 플랫폼**
사용자의 서버에서 제어되며 클라이언트 플랫폼의 제한을 받지 않습니다.

<span id="recordSDKAPI"></span>
### 방법2: 특정 사용자 녹화(SDK API)
TRTC SDK에서 제공하는 일부 API 인터페이스 및 매개변수를 호출하여 클라우드 혼합 스트리밍, 클라우드 녹화, 릴레이 라이브 방송의 세 가지 기능을 실현할 수 있습니다.

| 클라우드 기능 | 시작 방법                                                   | 종료 방법                                                   |
| :------- | :------- | :------- |
| 클라우드 녹화 | 방 입장 시 매개변수 `TRTCParams`의 `userDefineRecordId` 필드 설정   | 호스트 방 퇴장 시 자동 종료 |
| 클라우드 혼합 스트리밍 | SDK API [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)를 호출하여 클라우드 혼합 스트리밍 활성화 | 혼합 스트리밍을 요청한 호스트가 방 퇴장 후 혼합 스트리밍이 자동으로 종료되거나, 혼합 스트리밍 중 [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93)을 호출하여 매개변수를 `null/nil`로 수동 설정하는 경우 종료됨 |
| 릴레이 라이브 방송 | 방 입장 시 매개변수 `TRTCParams`의 `streamId` 필드 설정 | 호스트 방 퇴장 시 자동 종료 |

- **콘솔에서 설정**
  콘솔에서 [녹화 방식 선택](#recordType) 시 "특정 사용자 녹화"로 설정하면 됩니다.

- **녹화 작업 시작**
  호스트가 방 입장 시 입장 매개변수[TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams)의 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 필드를 지정하면 해당 호스트가 업스트리밍한 멀티미디어 데이터가 클라우드 녹화됩니다. 호스트가 해당 매개변수를 지정하지 않으면 녹화 작업이 트리거되지 않습니다.
```Objective-C
// 예시 코드: 사용자 rexchang의 멀티미디어 스트리밍 지정 녹화, 파일 id: 1001_rexchang
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC의 SDKAppID, 애플리케이션 생성 후 획득
param.roomId   = 1001;           // 방 번호
param.userId   = @"rexchang";    // 사용자 이름
param.userSig  = @"xxxxxxxx";    // 로그인 서명
param.role     = TRTCRoleAnchor; // 역할: 호스트
param.userDefineRecordId = @"1001_rexchang";  // 녹화 ID. 즉, 해당 사용자의 녹화 시작 지정
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVE 모드를 사용하십시오.
```

- **녹화 작업 종료**
  자동으로 종료됩니다. 방 퇴장 시 [userDefineRecordId](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce) 매개변수를 지정한 호스트가 멀티미디어 업스트리밍을 중단하면 해당 호스트의 클라우드 녹화가 자동으로 종료됩니다. [파일 포맷 선택]((#fileFormat) 시 "지속 녹화 시간"을 설정했다면 지속 녹화 설정 시간이 지난 후 녹화 파일을 확인할 수 있습니다.

- **다중 화면 혼합**
  SDK API [setMixTranscodingConfig()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) 호출을 통해 방 안에 있는 다른 사용자들의 화면과 음성을 현재 사용자의 멀티미디어 스트림 채널로 혼합할 수 있습니다. 해당 부분에 대한 자세한 설명은 [클라우드 혼합 스트리밍 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618#.E6.96.B9.E6.A1.88.E4.B8.80.EF.BC.9A.E6.9C.8D.E5.8A.A1.E7.AB.AF-rest-api-.E6.B7.B7.E6.B5.81.E6.96.B9.E6.A1.88) 문서를 참조하십시오.
>! TRTC 방에서 한 호스트(라이브 방송을 시작한 호스트 권장)가 `setMixTranscodingConfig`를 호출하면 됩니다. 여러 호스트가 호출할 경우 혼란 상태로 인해 오류가 발생할 수 있습니다.

- **녹화 파일 이름 생성**
  녹화 파일 이름은 `userDefineRecordId_시작 시간_종료 시간` 형식으로 생성됩니다.

- **지원되는 플랫폼**
  [iOS](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Android](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a154fa0570c3bb6a9f99fb108bda02520), [Windows](http://doc.qcloudtrtc.com/group__TRTCTypeDef__cplusplus.html#a3a7a5e6144aa337752d22269d25f7cfc), [Mac](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce), [Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) 등의 단말기에서 요청하는 녹화 제어를 지원하며, 현재는 Web 브라우저에서의 제어 요청은 지원하지 않습니다.

<span id="recordRESTAPI"></span>
### 방법3: 특정 사용자 녹화(REST API)

TRTC의 서버는 한 세트의 REST API( [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761)와 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760))를 제공하여 클라우드 혼합 스트리밍, 클라우드 녹화, 릴레이 라이브 방송 세 가지 기능을 제공합니다.

| 클라우드 기능 | 시작 방법                                                   | 종료 방법                                                   |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 클라우드 녹화 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.RecordId` 매개변수를 지정하면 녹화가 시작됩니다. | 자동으로 종료되거나, 중간에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하면 종료됩니다. |
| 클라우드 혼합 스트리밍 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `LayoutParams` 매변수를 지정하면 레이아웃 템플릿과 레이아웃 매개변수를 설정할 수 있습니다. | 모든 사용자가 퇴장한 후 자동으로 종료되거나, 중간에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하면 수동으로 종료할 수 있습니다. |
| 릴레이 라이브 방송 | [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `OutputParams.StreamId` 매개변수를 지정하면 CDN의 릴레이 라이브 방송을 활성화할 수 있습니다. | 자동으로 종료되거나, 중간에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하면 종료됩니다. |

>? 이는 TRTC 클라우드 서비스의 핵심 혼합 스트리밍 모듈인 MCU가 REST API를 제어하며, MCU의 혼합 스트리밍 결과를 녹화 시스템과 라이브 방송 CDN에 전송합니다. 따라서 API 이름이 `Start/StopMCUMixTranscode`이며, 기능적으로 봤을 때 `Start/StopMCUMixTranscode`로 혼합 스트리밍 기능 뿐만이 아니라 클라우드 녹화 및 릴레이 라이브 방송 CDN 기능도 실현할 수 있습니다.

- **콘솔에서 설정**
  콘솔에서 [녹화 방식 선택](#recordType) 시 "특정 사용자 녹화"로 설정하면 됩니다.

- **녹화 작업 시작**
서버에서 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 를 호출하여 `OutputParams.RecordId` 매개변수를 지정하면 혼합 스트리밍 및 녹화가 실행됩니다.
```
// 코드 예시: REST API를 통해 클라우드 혼합 스트리밍 및 클라우드 녹화 작업 실행
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
>- 해당 REST API는 방 안에 최소 1명 이상의 사용자가 입장(enterRoom)해야만 적용됩니다.
>- REST API는 단일 스트림 녹화는 지원하지 않으며, 단일 스트림 녹화가 필요한 경우 [방법1](#autoRecord) 또는 [방법2](#recordSDKAPI)를 선택하십시오.

- **녹화 작업 종료**
자동 종료됩니다. 또는 중간에 [StopMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37760)를 호출하여 혼합 스트리밍 및 녹화 작업을 종료할 수도 있습니다.

- **다중 화면 혼합**
[StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 `LayoutParams` 매개변수를 설정하면 클라우드 혼합 스트리밍이 실행됩니다. 해당 API는 전체 라이브 방송 시간 동안 여러 번 호출하여 필요에 따라 `LayoutParams` 매개변수를 수정하거나 혼합 화면 레이아웃을 변경할 수 있습니다. 단, 여러 번 호출 시 매개변수 `OutputParams.RecordId`와 `OutputParams.StreamId`는 항상 동일해야 하며, 동일하지 않을 경우 스트리밍이 중단되어 여러 개의 녹화 파일이 생성될 수 있습니다.
>?클라우드 혼합 스트리밍에 대한 자세한 설명은 [클라우드 혼합 스트리밍 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618#restapi)을 참조하십시오.

- **녹화 파일 이름 생성**
  녹화 파일 이름은 [StartMCUMixTranscode](https://intl.cloud.tencent.com/document/product/647/37761) 호출 시 지정한 `OutputParams.RecordId` 매개변수에 따라 생성되며, `OutputParams.RecordId_시작 시간_종료 시간` 형식으로 생성됩니다.

- **지원되는 플랫폼**
사용자의 서버에서 제어되며 클라이언트 플랫폼의 제한을 받지 않습니다.

<span id="search"></span>
## 녹화 파일 검색
녹화 기능을 활성화한 후, TRTC 시스템에서 녹화한 파일은 Tencent Cloud VOD 플랫폼에서 확인할 수 있습니다. VOD 콘솔에서 직접 검색하거나 백그라운드 서버에서 REST API를 사용하여 시간대별로 필터링할 수 있습니다.

#### 방법1: VOD 콘솔에서 수동으로 검색하기
1. [VOD 콘솔](https://console.cloud.tencent.com/vod/)에 로그인한 후 왼쪽 메뉴에서 [미디어 관리]를 선택합니다.
2. 리스트 상단에 있는 [접두사 검색]을 클릭한 후, [접두사 검색]을 선택하고 검색창에 키워드(예: `1400000123_1001_rexchang_main`)를 입력한 뒤 <img src="https://main.qcloudimg.com/raw/16b35c89b5efe4a7153e1cb5282006fd.png"  style="margin:0;">를 클릭하면 비디오 이름의 접두사가 매칭되는 비디오 파일이 표시됩니다.
3. 생성 시간으로 대상 파일을 필터링할 수도 있습니다.

#### 방법2: VOD REST API를 통해 검색하기
Tencent Cloud VOD 시스템은 REST API를 통한 멀티미디어 파일 관리를 제공합니다. [미디어 정보 검색](https://intl.cloud.tencent.com/document/product/266/34179)의 REST API를 통해 VOD 시스템 상의 파일을 검색할 수 있습니다. 요청 매개변수 표에 있는 `Text` 매개변수로 퍼지 매칭할 수 있으며, `StreamId` 매개변수로 정확한 검색을 진행할 수도 있습니다.
REST 요청 예시:
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&StreamId=stream1001
&Sort.Field=CreateTime
&Sort.Order=Desc
&<공통 요청 매개변수>
```

<span id="callback"></span>
## 녹화 파일 수신
[녹화 파일 검색](#search) 이외에도, 콜백 주소 설정을 통해 Tencent Cloud에서 신규 녹화 파일 정보를 사용자 서버로 전송하도록 설정할 수 있습니다.
방 안의 마지막 멀티미디어 스트리밍 중인 사용자가 퇴장하면 Tencent Cloud에서 녹화를 종료하고 파일을 VOD 플랫폼에 저장하며, 이 과정은 약 30초~2분 정도 소요됩니다. 참고로, 지속 녹화 시간을 300초로 설정한 경우 기본 시간에 300초를 더한 시간이 소요됩니다. 저장 완료 후 Tencent Cloud는 [녹화 콜백 설정](#recordCallback)에서 설정한 콜백 주소(HTTP/HTTPS)를 통해 사용자 서버로 알림을 발송합니다.

Tencent Cloud는 모든 녹화 및 녹화와 관련된 이벤트를 설정한 콜백 주소를 통해 사용자 서버로 발송하며, 콜백 정보는 다음 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/483dba536acd022f93af3ca5ff6cd74a.png)
다음 표의 필드를 통해 해당 콜백이 어떤 통화(또는 라이브 방송)과 매칭되는지 확인할 수 있습니다.

<table>
<tr>
<th>번호</th>
<th>필드 이름</th>
<th>설명</th>
</tr><tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/b75fdd3c8a2c0b1562ee4cb5a4ef65d1.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>event_type</td>
<td>정보 유형. event_type이 100인 경우, 해당 콜백 정보는 녹화 파일 생성 정보임을 표시합니다.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/2a495b157f03a8905e372a2516ea3a8f.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_id</td>
<td>방 입장 시 TRTCParams의 <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#a207ce719c22c89014a61d34af3e1e167">streamId</a> 필드를 설정하여 지정할 수 있습니다.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/1cf7ec54371a5e95e2ea00bdda4d1a64.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userid</td>
<td>사용자 이름의 Base64 인코딩</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/66d50d985be81cae9698fae3ffa40f40.png" style="box-shadow: 0 0 0px #ccc;"></td>
<td>stream_param.userdefinerecordid</td>
<td>사용자 정의 필드이며, TRTCParams의 <a href="http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#adacd59ca3b1e9e5e6205a0a131a808ce">userDefineRecordId</a> 필드를 통해 지정할 수 있습니다.</td>
</tr>
<tr>
<td style="text-align:center"><img src="https://main.qcloudimg.com/raw/d1cb894a93a1d69cd4215c54064eca5d.png"  style="box-shadow: 0 0 0px #ccc;"></td>
<td>video_url</td>
<td>녹화 파일의 시청 주소이며, <a href="#play">VOD 재생</a>에 사용할 수 있습니다.</td>
</tr></table>


<span id="delete"></span>
## 녹화 파일 삭제

Tencent Cloud VOD 시스템은 REST API를 통한 멀티미디어 파일 관리를 제공합니다. [미디어 삭제 API](https://intl.cloud.tencent.com/document/product/266/37571)를 통해 지정한 파일을 삭제할 수 있습니다.
REST 요청 예시:

```
https://vod.tencentcloudapi.com/?Action=DeleteMedia
&FileId=52858907988664150587
&<공통 요청 매개변수>
```

<span id="play"></span>

## 녹화 파일 재생

온라인 교육 등과 같은 시나리오에서는 일반적으로 라이브 방송 종료 후 녹화 파일을 여러 번 재생하여 학습 리소스를 충분히 활용할 수 있습니다.

#### 파일 포맷 선택(HLS)
[녹화 포맷 설정](#fileFormat)에서 파일 포맷을 HLS로 선택합니다.
HLS는 최대 5분의 중단 시간 지속 녹화를 지원하여 "라이브 방송 1회(또는 1교시)당 1개의 재생 링크 생성"을 할 수 있습니다. 또한 대다수의 브라우저에서의 온라인 재생을 지원해 비디오 재생 시나리오에 매우 적합합니다.

#### VOD 주소 획득(video_url)
[녹화 파일 수신](#callback) 시 콜백 정보의 **video_url** 필드를 가져올 수 있으며, 해당 필드는 해당 녹화 파일의 Tencent Cloud VOD 주소입니다.

#### VOD 플레이어 연결
사용 플랫폼에 따라 VOD 플레이어를 연결할 수 있으며, 자세한 방법은 다음을 참고하십시오.
- [iOS 플랫폼](http://doc.qcloudtrtc.com/group__TXVodPlayer__ios.html)
- [Android 플랫폼](http://doc.qcloudtrtc.com/group__TXVodPlayer__android.html)
- [Web 브라우저](https://intl.cloud.tencent.com/document/product/266/33977)

>! [프로 버전](https://intl.cloud.tencent.com/document/product/647/34615) TRTC SDK 사용을 권장합니다. 프로 버전은 [MLVB](https://intl.cloud.tencent.com/zh/product/mlvb) 등의 기능이 통합되어 있어 하위 레이어 모듈을 효율적으로 재사용해 증분 용량이 독립적인 SDK 2개를 통합한 용량보다 작고, 부호 충돌(symbol duplicate) 문제를 방지할 수 있습니다.


## 관련 비용

클라우드 녹화 및 재생 관련 비용에는 다음 몇 가지 항목이 포함되어 있습니다. 이 중 녹화 비용은 기본 비용이며, 기타 비용은 사용 상황에 따라 과금됩니다.

>?본 가격은 예시로 참고용으로만 제공됩니다. 실제와 금액이 상이한 경우 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385), [LVB](https://buy.cloud.tencent.com/price/lvb), [VOD](https://buy.cloud.tencent.com/price/vod)의 가격을 기준으로 합니다.

#### 녹화 비용: 트랜스 코딩 또는 캡슐화로 발생하는 비용 계산
녹화는 멀티미디어 스트리밍 트랜스 코딩 또는 캡슐화가 필요하며 서버에서 리소스를 계산하는 소모가 발생합니다. 따라서 녹화 작업에 따라 리소스 계산으로 인한 서버 점유율에 따라 비용이 발생합니다.
>!
>- 2020년 7월 1일 이후 처음으로 TRTC 콘솔에서 애플리케이션을 생성한 Tencent Cloud 계정에서 클라우드 녹화 기능을 사용한 후 발생하는 녹화 비용은 [클라우드 녹화 과금 설명](https://intl.cloud.tencent.com/document/product/647/38385)을 기준으로 합니다.
>- 2020년 7월 1일 이전에 TRTC 콘솔에서 애플리케이션을 생성한 Tencent Cloud 계정의 경우, 2020년 7월 1일 이전과 이후에 생성한 모든 애플리케이션에서 클라우드 녹화 기능을 사용하여 발생하는 녹화 비용은 기본적으로 **라이브 방송 녹화** 계속 사용 과금 규정을 적용합니다.

**라이브 방송 녹화**는 동시 녹화 채널 수에 따라 요금이 계산되며, 동시 접속 수가 많을수록 녹화 비용이 높아집니다. 자세한 과금 설명은 [LVB>라이브 방송 녹화](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6)를 참조하십시오.

>예를 들어, 현재 1000명의 호스트를 보유하고 있고 저녁 피크 시간에 동시에 최대 500개의 호스트 멀티미디어 스트리밍을 녹화해야 하는 경우, 녹화 단가가 5.2941USD/채널/월이라고 가정한다면 총 녹화 비용은 `500개 채널 X 5.2941USD/채널/월 = 2647.05USD/월`입니다.
>[녹화 포맷 설정](#fileFormat) 시 2개 녹화 파일 포맷을 선택한 경우, 녹화 비용과 스토리지 비용은 두 배(x2)가 되며, 3개 파일 포맷을 선택한 경우 녹화 비용 및 스토리지 비용은 세 배(x3)가 됩니다. 반드시 필요한 경우가 아니라면 한 가지 파일 포맷만 선택하는 것을 권장하며, 비용을 대폭 절약할 수 있습니다.

**스토리지 비용: 파일을 Tencent Cloud에 저장하는 경우 해당 비용 발생**
녹화한 파일을 Tencent Cloud에 저장하는 경우, 저장으로 인해 디스크 리소스가 소모되므로 저장하는 리소스 용량에 따라 비용이 발생합니다. 저장 시간이 길수록 비용 또한 높아지므로 특별하게 필요한 경우가 아니라면 파일 저장 기간을 짧게 설정하면 비용을 절약할 수 있습니다. 또는 파일을 사용자 서버에 저장할 수도 있습니다. 스토리지 비용은 [비디오 스토리지(일 결산) 가격](https://intl.cloud.tencent.com/document/product/266/14666)을 선택하여 일 단위로 결산할 수 있습니다.

>예를 들어, [setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam)을 통해 호스트의 비트레이트(videoBitrate)를 1000kbps로 설정하고 해당 호스트의 라이브 방송 비디오(파일 포맷 한 가지 선택) 1시간 동안 녹화하는 경우, `(1000 / 8)KBps × 3600초 = 450000KB = 0.45GB` 크기의 비디오 파일이 생성되며 해당 파일로 인해 매일 발생하는 스토리지 비용은 약 `0.45GB × 0.0009USD/GB/일 = 0.000405USD`입니다.

#### 시청 비용: 파일을 VOD 시청에 사용하는 경우 해당 비용 발생
녹화한 파일을 VOD 시청에 사용하는 경우, VOD 시청으로 인해 CDN 트래픽 소모가 발생합니다. 따라서 VOD 가격에 따라 비용이 발생하며 기본적으로 트래픽에 따라 과금됩니다. 시청하는 사람이 많을수록 비용이 높아지며, 시청 비용은 [비디오 가속(일 결산) 가격](https://intl.cloud.tencent.com/document/product/266/14666)을 선택하여 일 단위로 결산할 수 있습니다.

>예를 들어, 클라우드 녹화를 통해 1GB의 파일이 생성되었고 1000명의 시청자가 처음부터 끝까지 모두 시청하였을 경우 약 1TB의 VOD 시청 트래픽이 발생합니다. 차등 가격표에 따라 계산하면 `1000 × 1GB × 0.0794USD/GB = 79.4USD`의 비용이 발생합니다.
>Tencent Cloud에서 사용자 서버로 파일을 다운로드할 경우 단발성으로 약간의 VOD 트래픽 소모가 발생하며 월별 청구서에 표시됩니다.

#### 트랜스 코딩 비용: 혼합 스트리밍 녹화를 활성화하는 경우 해당 비용 발생
혼합 스트리밍 녹화를 활성화하는 경우, 혼합 스트리밍으로 인한 디코딩 및 인코딩 작업이 발생해 별도의 혼합 스트리밍 트랜스 코딩 비용이 발생합니다. 혼합 스트리밍 트랜스 코딩은 해상도 및 트랜스 코딩 시간에 따라 과금되며, 호스트용 해상도가 높고 마이크 연결 시간(일반적으로 마이크를 연결하는 시나리오에서 혼합 스트리밍 트랜스 코딩이 필요함)이 길수록 비용이 높아집니다. 자세한 비용 계산은 [라이브 방송 트랜스 코딩](https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.A0.87.E5.87.86.E8.BD.AC.E7.A0.81)을 참조하십시오.

>예를 들어, [setVideoEncodrParam()](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam)을 통해 호스트의 비트레이트(videoBitrate)를 1500kbps, 해상도를 720P로 설정하였고, 호스트 1명과 시청자의 마이크 연결 시간이 1시간이고 해당 마이크 연결 시간 동안 [클라우드 혼합 스트리밍 ](https://intl.cloud.tencent.com/document/product/647/34618)을 활성화한 경우, `0.0057USD/분 × 60분 = 0.342USD`의 트랜스 코딩 비용이 발생합니다.

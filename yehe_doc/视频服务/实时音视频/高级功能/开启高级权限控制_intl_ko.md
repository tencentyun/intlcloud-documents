## 개요

방 입장을 제한하거나 마이크 켜기를 제한하고 싶거나, 지정한 사용자만 방에 입장할 수 있거나 마이크를 켤 수 있도록 허용하고 싶은 경우, 또는 클라이언트에서 권한을 판단할 경우 쉽게 크래킹 공격을 받을 수 있어 걱정되는 경우 **고급 권한 제어 활성화**를 고려해볼 수 있습니다.

다음과 같은 시나리오에서는 고급 권한 제어 활성화가 필요하지 않습니다.

- 시나리오 1: 많은 사람이 들어올수록 좋기 때문에 방 입장 제한이 필요 없는 경우
- 시나리오 2: 해커의 크래킹에 대한 클라이언트 방어가 급하게 필요하지 않은 경우

다음과 같은 시나리오에서는 더 최적화된 보안을 위해 고급 권한 제어 활성화를 권장합니다.

- 시나리오 1: 보안성 요구가 비교적 높은 비디오 통화 또는 음성 통화가 필요한 경우
- 시나리오 2: 방별로 각각의 입장 권한을 설정해야 하는 경우
- 시나리오 3: 관중의 마이크 켜기 권한을 제어해야 하는 경우


## 지원 플랫폼

|   iOS    | Android  |  Mac OS  | Windows  | Electron |  Web |
| :------: | :------: | :------: | :------: | :------: | :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |     &#10003;    |

## 고급 권한 제어의 원리

고급 권한 제어를 활성화한 후에는 TRTC 백그라운드 서비스 시스템이 UserSig ‘방 입장 티켓’만을 인증하는 것이 아니라 **PrivateMapKey**라고 하는 ‘권한 티켓’까지 인증합니다. 권한 티켓에는 암호화된 roomid와 “비트 권한 리스트”가 포함되어 있습니다.

PrivateMapKey에는 roomid가 포함되어 있어 사용자가 UserSig만 제공하고 PrivateMapKey를 제공하지 않는 경우 지정된 방에 입장할 수 없습니다.

PrivateMapKey 상의 ‘비트 권한 리스트’는 byte의 8개 비트를 사용하며, 각각 해당 티켓을 가지고 있는 사용자를 대표합니다. 해당 티켓이 지정하고 있는 방에서 가지는 8가지 기능 권한은 다음과 같습니다.

| 비트 위치    | 이진법 표시 | 10진법 숫자 | 권한 의미                             |
| ------- | ---------- | :--------: | ------------------------------------ |
| 1번째 비트 | 0000 0001  |     1      | 방 생성 권한                       |
| 2번째 비트 | 0000 0010  |     2      | 방 입장 권한                       |
| 3번째 비트 | 0000 0100  |     4      | 오디오 발신 권한                       |
| 4번째 비트 | 0000 1000  |     8      | 오디오 수신 권한                       |
| 5번째 비트 | 0001 0000  |     16      | 비디오 발신 권한                       |
| 6번째 비트 | 0010 0000  |     32     | 비디오 수신 권한                       |
| 7번째 비트 | 0100 0000  |     64     | 비디오 서브 채널(즉, 화면 공유) 발신 권한 |
| 8번째 비트 | 1000 0000  |     128     | 비디오 서브 채널(즉, 화면 공유) 수신 권한 |


## 고급 권한 제어 활성화
[](id:step1)
### 1단계: TRTC 콘솔에서 고급 권한 제어를 활성화합니다.

1. Tencent Cloud TRTC 콘솔에서 왼쪽에 있는 [Application Management](https://console.cloud.tencent.com/trtc/app)를 클릭합니다.
2. 오른쪽 애플리케이션 리스트에서 고급 권한 제어를 활성화할 애플리케이션을 선택하고 [기능 설정]을 클릭합니다.
3. ‘기능 설정’ 페이지에서 [고급 권한 제어 활성화] 버튼을 활성화하고 [확인]을 누르면 고급 권한 제어가 활성화됩니다.
![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)


>!SDKAppid의 고급 권한 제어를 활성화한 후에는 해당 SDKAppid를 사용하는 모든 사용자는 TRTCParams에 `privateMapKey` 매개변수를 전달해야만 방에 입장([2단계](#step2)와 같이)할 수 있습니다. 만약 온라인으로 해당 SDKAppid를 사용하는 사용자가 있는 경우 해당 기능을 활성화하지 마십시오.

[](id:step2)

### 2단계: 귀하의 서버에서 PrivateMapKey를 계산합니다.

PrivateMapKey는 클라이언트에서의 리버스 크래킹을 방지하기 위한 것으로 ‘비회원도 고급 레벨 방 입장 가능’한 크래킹 버전이 나타날 수 있어, 서버에서 계산 후 다시 App에 반환하는 방식만 가능하며 App에서 직접 계산할 수 없습니다.

Tencent Cloud는 Java, PHP, Node.js 세가지 버전의 PrivateMapKey 계산 코드를 제공하며, 직접 다운로드하여 서버에 통합할 수 있습니다.

| 언어 버전 |                         주요 함수                         |                           다운로드 링크                           |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
|   Java   | `genPrivateMapKey` 및 `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
|    GO    | `GenPrivateMapKey` 및 `GenPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
|   PHP    | `genPrivateMapKey` 및 `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
|  Node.js  | `genPrivateMapKey` 및 `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
|  Python  | `genPrivateMapKey` 및 `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
|    C#    | `genPrivateMapKey` 및 `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |

[](id:step3)

### 3단계: 귀하의 서버에서 PrivateMapKey를 App으로 전달합니다.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)
상기 이미지와 같이 귀하의 서버에서 PrivateMapKey를 계산한 후 App으로 전달할 수 있으며, App은 두 가지 방법을 통해 PrivateMapKey를 SDK로 전달할 수 있습니다.

#### 방법1: enterRoom 시 SDK 전달
사용자 방 입장 권한을 제어하려면, `TRTCCloud`의 `enterRoom` 인터페이스 호출 시 [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)의 **privateMapKey** 매개변수를 설정하여 구현할 수 있습니다.

해당 경우의 방 입장 시 PrivateMapKey 검증 방법은 비교적 간단하며, 방 입장 전 사용자 권한을 정확하게 확인할 수 있는 시나리오에 매우 적합합니다.

#### 방법2: 테스트용 인터페이스를 통해 SDK에 업데이트
라이브 방송 시나리오에서 관중이 마이크를 켜 호스트가 되는 마이크 연결 시나리오가 종종 존재합니다. 관중이 호스트가 되는 경우 TRTC가 다시 방 입장 시 입장 매개변수인 `TRTCParams`에 존재하는 PrivateMapKey를 인증하며, PrivateMapKey의 유효기간을 ‘5분’ 등으로 비교적 짧게 설정하면 인증에 실패되어 사용자가 방에서 퇴장될 수 있습니다.

해당 문제를 해결하기 위해서는 유효기간을 연장(예: ‘5분’을 ‘6시간’으로 변경)하는 방법 이외에도, 관중이 자신의 신분을 호스트로 변경하기 전 `switchRole`을 통해 다시 귀하의 서버에 privateMapKey를 신청하고 SDK의 테스트용 인터페이스인 `updatePrivateMapKey`를 호출하여 SDK에 업데이트하는 방법이 있습니다. 코드 예시는 다음과 같습니다:
[](id:example_code)
<dx-codeblock>
::: Android java
JSONObject jsonObject = new JSONObject();
try {
    jsonObject.put("api", "updatePrivateMapKey");
    JSONObject params = new JSONObject();
    params.put("privateMapKey", "xxxxx"); // 신규 privateMapKey 입력
    jsonObject.put("params", params);
    mTRTCCloud.callExperimentalAPI(jsonObject.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
:::
::: iOS OC
NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
[params setObject:@"xxxxx" forKey:@"privateMapKey"]; // 신규 privateMapKey 입력
NSDictionary *dic = @{@"api": @"updatePrivateMapKey", @"params": params};
NSData *jsonData = [NSJSONSerialization dataWithJSONObject:dic options:0 error:NULL];
NSString *jsonStr = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[WXTRTCCloud sharedInstance] callExperimentalAPI:jsonStr];
:::
::: C++ C++
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";
TRTCCloudCore::GetInstance()->getTRTCCloud()->callExperimentalAPI(api.c_str());
:::
::: C# C#
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";       
mTRTCCloud.callExperimentalAPI(api);
:::
</dx-codeblock>

## FAQ
[](id:q1)
#### 1. 온라인 상의 모든 방에 들어갈 수 없습니다.

방 권한 제어가 활성화되면 현재 SDKAppid의 모든 방은 `TRTCParams`에 privateMapKey가 설정되어 있어야만 입장할 수 있습니다. 따라서 현재 온라인 서비스를 운영 중인 상태에서 온라인 버전에 privateMapKey 관련 로직이 없다면 해당 기능을 활성화하지 마십시오.

[](id:q2)
#### 2. PrivateMapKey와 UserSig의 차이점은 무엇입니까?

UserSig은 TRTCParams의 필수 항목으로, 현재 사용자에게 TRTC 클라우드 서비스를 사용 권한이 있는지 여부를 검사하여 해커가 귀하의 SDKAppid 계정 내 트래픽을 도용하지 못하도록 방지합니다.

PrivateMapKey는 TRTCParams의 필수 항목이 아니며, 현재 사용자가 지정된 roomid 방에 입장할 수 있는 권한이 있는지 여부와 해당 방에서 가지는 권한을 검사합니다. 귀하의 비즈니스에 사용자의 신분 구분이 필요한 경우에만 활성화해야 합니다.

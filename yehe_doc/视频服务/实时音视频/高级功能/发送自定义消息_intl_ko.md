## 콘텐츠 소개

TRTC SDK는 사용자 정보 메시지를 발송하는 기능을 제공하며, 해당 기능을 통해 모든 호스트 역할을 하는 사용자가 동일한 라이브 룸의 다른 사용자에게 자신의 사용자 정의 메시지를 발송할 수 있습니다.

## 지원 플랫폼

| iOS | Android | Mac OS | Windows | Electron| web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|   &#10003;  |   &#10003;   |   &#10003;  |   &#10003;   | &#10003;  |   ×  |

## 발신/수신 원리
사용자의 사용자 정의 메시지가 멀티미디어 데이터 스트림에 삽입되어 멀티미디어 데이터와 함께 방 안에 있는 다른 사용자들에게 전송됩니다. 멀티미디어 채널은 본래 100% 신뢰할 수 있지 않으므로 신뢰성을 높이기 위해 TRTC SDK 내부에서 일부 신뢰도가 높은 메커니즘을 구현합니다.

![](https://main.qcloudimg.com/raw/cc11b0e81970929ef28d2074c8297753.jpg)

## 메시지 발송

TRTCCloud의 `sendCustomCmdMsg` 인터페이스 호출을 통해 발송하며, 발송 시 다음 4개의 매개변수를 지정해야 합니다.


| 매개변수 이름 | 매개변수 설명 |
|:--------:|:--------------|
| cmdID | 메시지 ID. 1 ~ 10으로 설정할 수 있으며, 각 서비스 유형 메시지별로 서로 다른 cmdID를 사용해야 합니다. |
| data | 발송 대기 중인 메시지. 최대 1KB(1000바이트)까지 지원합니다. |
| reliable | 신뢰도 높은 발송 여부. 신뢰도 높은 발송은 일정의 딜레이가 발생하며, 이는 수신측에서 재전송 대기를 위해 일정 시간 동안 데이터를 일시 저장하기 때문입니다.  |
| ordered | 순차 요구 여부. 즉, 수신측이 수신하는 데이터 순서와 발신측이 발송하는 순서의 일치 여부를 요구하는지 나타내며, 이는 수신측에서 해당 메시지를 일시 저장하고 정렬하기 때문에 일정한 수신 딜레이가 발생합니다.  |

>reliable과 ordered를 동시에 YES 또는 NO로 설정하십시오. 현재는 서로 다른 값으로 설정할 수 없습니다.

- **Objective-C**

``` Objective-C
//사용자 정의 메시지 발송 예시 코드
- (void)sendHello {
    // 사용자 정의 메시지 명령어로, 해당 부분은 서비스에서 사용자 정의한 규칙에 따라야 하며, 0X1을 발신 문자로 하는 메시지 전송 예시입니다.
    NSInteger cmdID = 0x1;
    NSData *data = [@"Hello" dataUsingEncoding:NSUTF8StringEncoding];
    // reliable과 ordered는 동일한 값으로 설정해야 합니다. 본 예시는 신뢰성이 보장되는 메시지가 발송 순서에 따라 도달하는 설정입니다.
    [trtcCloud sendCustomCmdMsg:cmdID data:data reliable:YES ordered:YES];
}
```

- **Java**

``` java
//사용자 정의 메시지 발송 예시 코드
public void sendHello() {
    try {
        // 사용자 정의 메시지 명령어로, 해당 부분은 서비스에서 사용자 정의한 규칙에 따라야 하며, 0X1을 발신 문자로 하는 메시지 전송 예시입니다.
        int cmdID = 0x1;
        String hello = "Hello";
        byte[] data = hello.getBytes("UTF-8");
        // reliable과 ordered는 동일한 값으로 설정해야 합니다. 본 예시는 신뢰성이 보장되는 메시지가 발송 순서에 따라 도달하는 설정입니다.
        trtcCloud.sendCustomCmdMsg(cmdID, data, true, true);
				
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
    }
}
```

- **C++**

``` C++
// 사용자 정의 메시지 발송 예시 코드
void sendHello()
{
    // 사용자 정의 메시지 명령어로, 해당 부분은 서비스에서 사용자 정의한 규칙에 따라야 하며, 0X1을 발신 문자로 하는 메시지 전송 예시입니다.

    uint32_t cmdID = 0x1;
    uint8_t* data = { '1', '2', '3' };
    uint32_t dataSize = 3;  // data 길이

    // reliable과 ordered는 동일한 값으로 설정해야 합니다. 본 예시는 신뢰성이 보장되는 메시지가 발송 순서에 따라 도달하는 설정입니다.
    trtcCloud->sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```
- **C#**

```c#
// 사용자 정의 메시지 발송 예시 코드
private void sendHello()
{
    // 사용자 정의 메시지 명령어로, 해당 부분은 서비스에서 사용자 정의한 규칙에 따라야 하며, 0X1을 발신 문자로 하는 메시지 전송 예시입니다.

    uint cmdID = 0x1;
    byte[] data = { '1', '2', '3' };
    uint dataSize = 3;  // data 길이

    // reliable과 ordered는 동일한 값으로 설정해야 합니다. 본 예시는 신뢰성이 보장되는 메시지가 발송 순서에 따라 도달하는 설정입니다.
    mTRTCCloud.sendCustomCmdMsg(cmdID, data, dataSize, true, true);
}
```


## 메시지 수신

방 안에 있는 한 사용자가`sendCustomCmdMsg`를 통해 사용자 정의 메시지를 발송하면, 방 안에 있는 다른 사용자는 SDK 콜백의 `onRecvCustomCmdMsg` 인터페이스를 통해 해당 메시지를 수신합니다.

- **Objective-C**

``` Objective-C
//방 안의 다른 사용자가 발송한 메시지 수신 및 처리
- (void)onRecvCustomCmdMsgUserId:(NSString *)userId cmdID:(NSInteger)cmdId seq:(UInt32)seq message:(NSData *)message
{
	// userId가 발송한 메시지 수신
    switch (cmdId)  // 발신측과 수신측이 협의한 cmdId
    {
    case 0:
        // cmdId = 0 메시지 처리
        break;
    case 1:
        // cmdId = 1 메시지 처리
        break;
    case 2:
        // cmdId = 2 메시지 처리
        break;
    default:
        break;
    }
}

```

- **Java**

``` java
//TRTCCloudListener를 상속하여 onRecvCustomCmdMsg 구현 방법으로 방 안에 있는 다른 사용자의 발송 메시지 수신 및 처리
public void onRecvCustomCmdMsg(String userId, int cmdId, int seq, byte[] message) {
	// userId가 발송한 메시지 수신
    switch (cmdId)  // 발신측과 수신측이 협의한 cmdId
    {
    case 0:
        // cmdId = 0 메시지 처리
        break;
    case 1:
        // cmdId = 1 메시지 처리
        break;
    case 2:
        // cmdId = 2 메시지 처리
        break;
    default:
        break;
    
}
```

- **C++**

``` C++
// 방 안의 다른 사용자가 발송한 메시지 수신 및 처리
void TRTCCloudCallbackImpl::onRecvCustomCmdMsg(
                            const char* userId, int32_t cmdId, uint32_t seq, const uint8_t* msg, uint32_t msgSize)
{
    // userId가 발송한 메시지 수신
    switch (cmdId)  // 발신측과 수신측이 협의한 cmdId
    {
    case 0:
        // cmdId = 0 메시지 처리
        break;
    case 1:
        // cmdId = 1 메시지 처리
        break;
    case 2:
        // cmdId = 2 메시지 처리
        break;
    default:
        break;
    }
}
```

* **C#**

```c#
// 방 안의 다른 사용자가 발송한 메시지 수신 및 처리
public void onRecvCustomCmdMsg(string userId, int cmdId, uint seq, byte[] msg, uint msgSize)
{
    // userId가 발송한 메시지 수신
    switch (cmdId)  // 발신측과 수신측이 협의한 cmdId
    {
    case 0:
        // cmdId = 0 메시지 처리
        break;
    case 1:
        // cmdId = 1 메시지 처리
        break;
    case 2:
        // cmdId = 2 메시지 처리
        break;
    default:
        break;
    }
}
```

## 사용 제한

사용자 정의 메시지는 멀티미디어 데이터보다 높은 전송 우선순위를 가집니다. 따라서 사용자 정의 데이터 발송이 너무 많은 경우 멀티미디어 데이터가 간섭을 받을 수 있으며, 이로 인해 화면 랙 또는 흐릿해지는 현상이 발생할 수 있습니다. 이에 따라 사용자 정의 메시지 발송에 대해 다음과 같이 빈도수를 제한합니다.

- 사용자 정의 메시지는 클라우드 방송에서 방 안에 있는 사용자들에게 발송합니다. 따라서 초당 최대 30개까지 발송할 수 있습니다.
- 모든 메시지 패킷(즉, data 크기)은 최대 1KB로 제한되며, 이를 초과할 경우 중간 라우터 또는 서버에서 손실될 확률이 높습니다.
- 모든 클라이언트는 초당 최대 총 8KB의 데이터를 전송할 수 있습니다. 즉, 모든 데이터 패킷이 1KB인 경우 초당 최대 8개의 데이터 패킷만 발송할 수 있습니다.









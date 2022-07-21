본 문서는 TRTC 방 퇴장 방법과 어떤 경우에 사용자가 강제 퇴장 당할 수 있는지 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2de2f23672af65132b09d78d031d6c2d.png)

## 호출 가이드

[](id:step1)
### 1단계: 필수 단계 수행

1. [빠른 통합(Electron)](https://intl.cloud.tencent.com/document/product/647/35097)에 설명된 대로 SDK를 가져오고 App 권한을 구성합니다.
2. [방 입장](https://cloud.tencent.com/document/product/647/74635)의 안내에 따라 방 입장 프로세스를 진행합니다.

[](id:step2)
### 2단계: 현재 방에서 퇴장
[exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#exitRoom) API를 호출하여 현재 방을 나가면 SDK는 onExitRoom(int reason) 콜백 이벤트를 통해 방을 나가는 이유를 알려줍니다.
```javascript
import TRTCCloud from 'trtc-electron-sdk';
const trtcCloud = new TRTCCloud();

// 현재 방 퇴장
trtcCloud.exitRoom();
```

exitRoom API가 호출된 후 SDK는 두 가지 주요 작업을 완료해야 하는 방 퇴장 프로세스에 들어갑니다.
- **주요 작업1: 현재 사용자의 퇴장 알림**
방의 다른 사용자에게 다가오는 방 퇴장을 알리면 현재 사용자로부터 **onRemoteUserLeaveRoom** 콜백을 받게 됩니다. 그렇지 않으면 다른 사용자가 현재 사용자의 비디오 이미지가 ‘정지’된 것으로 간주할 수 있습니다.
- **주요 작업2: 디바이스 권한 철회**
현재 사용자가 방을 나가기 전에 오디오/비디오 스트림을 게시하는 경우 사용자는 방을 나가는 동안 카메라와 마이크를 끄고 장치 권한을 해제해야 합니다.

따라서 onExitRoom 콜백을 수신한 후 TRTCCloud 인스턴스를 해제하는 것이 좋습니다.

[](id:step3)
### 3단계: 현재 방에서 강제 퇴장
[onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) 콜백은 방 퇴장 외에 다른 두 가지 경우에도 수신됩니다:
- **사례1: 사용자가 방에서 퇴장 당한 경우**
[RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630) API를 호출하여 사용자를 TRTC 방에서 퇴장시킬 수 있습니다. 퇴장 당한 사용자는 onExitRoom(1) 콜백을 받게 됩니다.

- **사례2: 현재 방이 해산됨**
[DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631) API를 호출하여 TRTC 방을 해산할 수 있습니다. 방이 해산되면 방에 있는 모든 사용자가 onExitRoom(2) 콜백을 받습니다.

```javascript
// 방 퇴장 이유를 얻기 위해 onExitRoom 콜백 수신
function onExitRoom(reason) {
  console.log(`onExitRoom reason: ${reason}`);
}
trtcCloud.on('onExitRoom', onExitRoom);
```

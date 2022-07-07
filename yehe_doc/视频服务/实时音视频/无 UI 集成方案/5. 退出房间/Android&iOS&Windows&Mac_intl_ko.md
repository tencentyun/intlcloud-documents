본 문서는 TRTC 방 퇴장 방법과 어떤 경우에 사용자가 강제 퇴장 당할 수 있는지 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/2de2f23672af65132b09d78d031d6c2d.png)

## 호출 가이드


[](id:step1)
### 1단계: 필수 단계 수행
[빠른 통합(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)에 설명된 대로 SDK를 가져오고 애플리케이션 권한을 구성합니다.
[방 입장](https://intl.cloud.tencent.com/document/product/647/47645)의 안내에 따라 방 입장 절차를 진행합니다.

[](id:step2)
### 2단계: 현재 방에서 퇴장
exitRoom API를 호출하여 현재 방을 나가면 SDK는 onExitRoom(int reason) 콜백 이벤트를 통해 방 퇴장 이유를 알려줍니다.
<dx-codeblock>
::: Android  java
// 현재 방 퇴장
mCloud.exitRoom();
:::
::: iOS&Mac  swift
self.trtcCloud = [TRTCCloud sharedInstance];
// 현재 방 퇴장
[self.trtcCloud exitRoom];
:::
::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();
// 현재 방 퇴장
trtc_cloud_->exitRoom();
:::
</dx-codeblock>

exitRoom API가 호출된 후 SDK는 두 가지 주요 작업을 완료해야 하는 방 퇴장 프로세스에 들어갑니다.
- **핵심 과제1: 현재 사용자 퇴장 알림**
방의 다른 사용자에게 다가오는 방 퇴장을 알리면 현재 사용자로부터 **onRemoteUserLeaveRoom** 콜백을 받게 됩니다. 그렇지 않으면 다른 사용자가 현재 사용자의 비디오 이미지가 ‘정지’된 것으로 간주할 수 있습니다.
- **핵심 과제2: 디바이스 권한 철회**
현재 사용자가 방을 나가기 전에 오디오/비디오 스트림을 게시하는 경우 사용자는 방을 나가는 동안 카메라와 마이크를 끄고 장치 권한을 해제해야 합니다.

따라서 onExitRoom 콜백을 수신한 후 TRTCCloud 인스턴스를 해제하는 것이 좋습니다.


[](id:step3)
### 3단계: 강제로 현재 방 퇴장
onExitRoom(int reason) 콜백은 활성 방 퇴장 외에 다른 두 가지 경우에도 수신됩니다.
- **사례1: 사용자가 방에서 퇴장 당한 경우**
[RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630)를 사용할 수 있습니다.  사용자를 TRTC 방에서 퇴장시키는 API입니다. 퇴장 당한 사용자는 onExitRoom(1) 콜백을 받게 됩니다.

- **사례2: 현재 방이 해산됨**
[DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631) API를 호출하여 TRTC 방을 해산할 수 있습니다. 방이 해산되면 방에 있는 모든 사용자가 onExitRoom(2) 콜백을 받습니다.


<dx-codeblock>
::: Android  java
// 방 퇴장 이유를 얻기 위해 onExitRoom 콜백 수신
@Override
public void onExitRoom(int reason) {
    if (reason == 0) {
        Log.d(TAG, "Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        Log.d(TAG, "Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        Log.d(TAG, "Current room is dissolved by server through the restful api...");
    }
}
:::
::: iOS&Mac  ObjC
// 방 퇴장 이유를 얻기 위해 onExitRoom 콜백 수신
- (void)onExitRoom:(NSInteger)reason {
    if (reason == 0) {
        NSLog(@"Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        NSLog(@"Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        NSLog(@"Current room is dissolved by server through the restful api...");
    }
}
:::
::: Windows  C++
// 방 퇴장 이유를 얻기 위해 onExitRoom 콜백 수신
void onExitRoom(int reason) {
    if (reason == 0) {
        printf("Exit current room by calling the 'exitRoom' api of sdk ...");
    } else if (reason == 1) {
        printf("Kicked out of the current room by server through the restful api...");
    } else if (reason == 2) {
        printf("Current room is dissolved by server through the restful api...");
    }
}
:::
</dx-codeblock>

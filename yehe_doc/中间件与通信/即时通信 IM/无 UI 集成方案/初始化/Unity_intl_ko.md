## 기능 설명
해당 기능을 사용하기 전에 IM SDK를 **반드시** 초기화해야 합니다.
대부분의 시나리오에서 IM SDK는 애플리케이션 라이프사이클 동안 한 번만 초기화하면 됩니다.


## 초기화
다음 단계에 따라 SDK를 초기화할 수 있습니다.
1. SDKAppID를 준비합니다.
2. SdkConfig를 설정합니다.
3. SDK 이벤트 리스너를 설정합니다.
4. [`Init`](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html) SDK를 호출하여 SDK를 초기화합니다.

자세한 단계는 다음과 같습니다.

[](id:SDKAppID)
### SDKAppID 준비
초기화를 수행하려면 올바른 SDKAppID가 있어야 합니다.
SDKAppID는 Tencent Cloud IM 계정을 고유하게 식별합니다. 각 App에 대해 새 SDKAppID를 신청하는 것이 좋습니다. 메시지는 자연스럽게 격리되며 서로 다른 SDKAppID 값 간에 통신할 수 없습니다.
[IM 콘솔](https://console.cloud.tencent.com/im)에서 모든 SDKAppID 값을 볼 수 있으며 **애플리케이션 생성**을 클릭하여 SDKAppID를 생성할 수 있습니다.


[](id:SDKConfig)
### SdkConfig 설정

SDK를 초기화하기 전에 로컬 SDK 캐시 및 로그 위치를 설정하는 데 사용되는 [SdkConfig](https://comm.qq.com/im/doc/unity/zh/types/SDKSetConfigAttributes/SdkConfig.html) 객체를 초기화해야 합니다.

IM 실행 로그 및 데이터의 스토리지 경로를 구성해야 합니다.

### sdk_config_config_file_path

로컬 IM 데이터의 저장 경로입니다.
>!애플리케이션은 이 경로에 대한 읽기-쓰기 액세스 권한이 필요합니다.

### sdk_config_log_file_path

IM 로그의 저장 경로입니다.
>!애플리케이션은 이 경로에 대한 읽기-쓰기 액세스 권한이 필요합니다.

### 초기화 API 호출
상기 단계를 수행한 후 `Init` SDK([상세 보기](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html))를 호출하여 SDK를 초기화할 수 있습니다.

예시 코드는 다음과 같습니다.

```c#
public static void Init() {
        int sdkappid = 0; // IM 콘솔에서 SDKAppID 가져오기.
        SdkConfig sdkConfig = new SdkConfig();

        sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";

        sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";

        TIMResult res = TencentIMSDK.Init(long.Parse(sdkappid), sdkConfig);
}
```

### SDK 글로벌 이벤트 리스너 등록
초기화 후 SDK는 [`NetworkStatusListenerCallback`](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html), [`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) 및 기타 콜백을 통해 연결 상태 및 로그인 티켓 만료와 같은 이벤트를 발생시킵니다.
initSDK를 호출한 직후 글로벌 이벤트 리스너를 등록하고 이러한 콜백에서 로직 프로세싱을 수행하는 것이 좋습니다.

콜백은 다음과 같습니다.

| 이벤트 콜백                                                  | 설명                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| [RecvNewMsgCallback](https://comm.qq.com/im/doc/unity/zh/callback/RecvNewMsgCallback.html) | 새 메시지 수신 콜백                               |
| [MsgReadedReceiptCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgReadedReceiptCallback.html) | 메시지 수신 확인 콜백                             |
| [MsgRevokeCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgRevokeCallback.html) | 메시지 회수 콜백                                  |
| [MsgElemUploadProgressCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgElemUploadProgressCallback.html) | 메시지 요소의 업로드 진행 콜백                    |
| [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupTipsEventCallback.html) | 그룹 시스템 메시지 콜백                           |
| [GroupAttributeChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupAttributeChangedCallback.html) | 그룹 속성 변경 콜백                               |
| [ConvTotalUnreadMessageCountChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/ConvTotalUnreadMessageCountChangedCallback.html) | 대화의 읽지 않은 메시지 수 변경 콜백              |
| [NetworkStatusListenerCallback](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html) | 네트워크 연결 상태 수신 콜백                      |
| [KickedOfflineCallback](https://comm.qq.com/im/doc/unity/zh/callback/KickedOfflineCallback.html) | 강제 오프라인 콜백                                |
| [UserSigExpiredCallback](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) | 티켓 만료 콜백                                    |
| [OnAddFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnAddFriendCallback.html) | 친구 추가 콜백                                    |
| [OnDeleteFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnDeleteFriendCallback.html) | 친구 삭제 콜백                                    |
| [UpdateFriendProfileCallback](https://comm.qq.com/im/doc/unity/zh/callback/UpdateFriendProfileCallback.html) | 친구 프로필 업데이트 콜백                         |
| [FriendAddRequestCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendAddRequestCallback.html) | 친구 요청 콜백                                    |
| [FriendApplicationListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListDeletedCallback.html) | 친구요청 삭제 콜백                                |
| [FriendApplicationListReadCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListReadCallback.html) | 친구 요청 읽기 콜백                               |
| [FriendBlackListAddedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListAddedCallback.html) | 블록리스트 친구 추가 콜백                         |
| [FriendBlackListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListDeletedCallback.html) | 블록리스트 친구 제거 콜백                         |
| [LogCallback](https://comm.qq.com/im/doc/unity/zh/callback/LogCallback.html) | 로그 콜백                                         |
| [MsgUpdateCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgUpdateCallback.html) | 메시지 업데이트 콜백                              |
| [MsgGroupMessageReadMemberListCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgGroupMessageReadMemberListCallback.html) | 그룹 메시지를 읽은 그룹 구성원 목록 가져오기 콜백 |

>! [`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) 콜백을 수신하면 로그인에 사용하는 UserSig가 만료된 것입니다. 이 경우 새 UserSig를 사용하여 다시 로그인해야 합니다. 만료된 UserSig를 계속 사용하면 IM SDK가 무한 로그인 루프에 빠집니다.

### 초기화 취소
일반적으로 애플리케이션의 라이프사이클이 IM SDK의 라이프사이클과 동일한 경우 애플리케이션을 종료하기 전에 IM SDK를 초기화 취소할 필요가 없습니다.
그러나 특수한 경우(예: 특정 UI에 들어간 후에만 IM SDK를 초기화하고 UI를 종료한 후에는 더 이상 사용하지 않음)에서 IM SDK를 초기화 취소할 수 있습니다.

초기화 취소 API `unInit` SDK([상세 보기](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Uninit.html))를 호출하여 초기화 취소를 수행할 수 있습니다.

예시 코드는 다음과 같습니다.

```c#
// SDK 초기화 취소
TencentIMSDK.Uninit();
```
## 기타
res는 SDK가 호출될 때 반환되는 결과입니다. TIMResult.TIM_SUCC = 0이면 API가 성공적으로 호출됩니다.

SDK가 성공적으로 초기화된 후 메시지 누락을 방지하려면 필요한 이벤트 리스너를 추가해야 합니다.

[](id:qa)

## FAQ

[](id:qa1)

### 1. 로그인, 메시지, 그룹, 대화, 관계 체인 및 프로필, 신호 기능을 사용하기 전에 IM SDK를 초기화해야 합니다.

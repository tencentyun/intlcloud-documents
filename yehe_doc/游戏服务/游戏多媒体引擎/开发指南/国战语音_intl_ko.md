개발자가 편리하게 GME(Game Multimedia Engine) API에 액세스하고 디버깅할 수 있도록, 본문에서는 GME 클랜전 음성 채팅 모드를 구현하는 방법을 설명합니다.

## 시나리오

클랜전 게임 시나리오에서 GME는 호스트 및 청취자 역할을 제공합니다. 사용자가 방에 입장하기 전에 호스트 역할이 설정되면 마이크를 켜고 말할 수 있으며, 스피커를 켜고 방에서 다른 사람이 말하는 것을 들을 수 있습니다. 사용자가 청취자 역할로 방에 입장하면 마이크를 켜도 방에서 말할 수 없습니다.

## 전제 조건

- GME 애플리케이션을 생성하고 SDK의 AppID와 Key를 얻었습니다. 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME의 실시간 음성 채팅 서비스**를 활성화했습니다. 자세한 내용은 [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.
- **GME SDK 통합을** 완료했습니다. 자세한 내용은 [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858)를 참고하십시오.

## 액세스 단계

다음은 클랜전 음성 채팅 모드를 구현하는 과정입니다.

<dx-steps>
-<dx-tag-link link="#enable" tag="콘솔">GME 서비스 사용</dx-tag-link>
-<dx-tag-link link="#config" tag="콘솔">역할 설정</dx-tag-link>
-<dx-tag-link link="#access" tag="비즈니스">실시간 음성 채팅 사용</dx-tag-link>
-<dx-tag-link link="#callback" tag="비즈니스">마이크 활성화</dx-tag-link> 
-<dx-tag-link link="#result" tag="콘솔">역할 변경 </dx-tag-link>
-<dx-tag-link link="#usage" tag="콘솔">방 퇴장</dx-tag-link>
</dx-steps>

 [](id:enable)
### 1단계: GME 서비스 사용

GME SDK를 호출하고 통합하는 방법에 대한 자세한 내용은 [Native SDK Quick Access](https://intl.cloud.tencent.com/document/product/607/40858), [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544) 및 [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.

[](id:config)
### 2단계: 역할 설정

EnterRoom API를 호출하기 전에 SetAudioRole API를 호출하여 클랜전 음성 채팅 모드에서 현재 사용자의 역할을 설정해야 합니다.

#### 함수 프로토타입
```
public abstract int SetAudioRole(ITMG_AUDIO_MEMBER_ROLE role); 
```

| 매개변수 | 유형                   | 의미                                                         |
| ---- | ---------------------- | ------------------------------------------------------------ |
| role | ITMG_AUDIO_MEMBER_ROLE | <li>ITMG_AUDIO_MEMBER_ROLE_ANCHOR 방에서 마이크와 스피커를 활성화할 수 있는 호스트 </li><li>ITMG_AUDIO_MEMBER_ROLE_AUDIENCE 방에서 스피커만 활성화할 수 있는 청취자</li> |

#### 예시 코드
```
ITMGContext.GetInstance().SetAudioRole(ITMG_AUDIO_MEMBER_ROLE.ITMG_AUDIO_MEMBER_ROLE_AUDIENCE);
```

[](id:access)
### 3단계: 실시간 음성 채팅 서비스 사용 

EnterRoom API를 호출하여 음성 채팅방에 입장합니다.

[](id:callback)
### 4단계: 마이크 활성화 

- 역할이 호스트인 경우 EnableMic 및 EnableSpeaker API를 호출하여 마이크와 스피커를 각각 활성화할 수 있습니다.
- 역할이 청취자인 경우 EnableSpeaker API를 사용하여 스피커를 활성화할 수 있지만, EnableMic API 호출 시 AV_ERR_INVALID_ARGUMENT 오류 코드(1004)가 반환되어 사용자가 청취자 모드에 있으며 마이크를 활성화할 수 없음을 상기시킵니다.

[](id:result)
### 5단계: 역할 변경

방에서 SetAudioRole을 호출하여 역할을 변경할 수 있습니다.
- 역할이 설정되지 않은 경우 새 역할이 적용됩니다.
- 역할이 설정된 경우 새 역할이 적용됩니다.
- 역할이 설정되지 않았거나 역할이 호스트이고 마이크가 활성화된 상태에서 말하는 경우 역할이 청취자로 변경되면 마이크가 활성화되어 있어도 방에서 말할 수 없습니다. 이 경우 비즈니스 레이어에서 EnableMic API를 호출하여 마이크 UI 상태를 변경하는 것이 좋습니다.

[](id:usage)
### 6단계: 방 퇴장 

ExitRoom API를 호출하여 실시간 음성 채팅방을 나가면 역할 상태가 무효가 되며 역할을 다시 설정해야 합니다.

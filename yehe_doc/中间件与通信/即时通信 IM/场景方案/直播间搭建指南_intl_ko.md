라이브 스트리밍이 보편화되면서 점점 더 많은 기업과 개발자들이 자체 라이브 스트리밍 플랫폼을 구축하고 있습니다. 이 과정에서 라이브 스트림 푸시 및 풀, 라이브 트랜스코딩, 라이브 화면 캡처, 라이브 스트림 믹싱, 라이브 채팅방, 라이브 룸 인터랙션(예: 좋아요, 선물 및 공동 앵커) 및 라이브 룸 상태 관리와 같은 복잡한 요구 사항을 처리해야 합니다. 이 문서에서는 Tencent Cloud 제품([Instant Messaging](https://console.cloud.tencent.com/im), [Cloud Streaming Services](https://console.cloud.tencent.com/live/livestat))를 예로 들어 라이브 룸을 구현하는 방법과 가능한 문제 및 고려 사항을 설명하고, 라이브 스트리밍 비즈니스 및 요구 사항을 간략히 안내합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/bd431307af0643d731a59b6211be54a8.png)



## 1. 준비 작업

### 애플리케이션 생성

Tencent Cloud에서 라이브 룸을 설정하려면 아래와 같이 [콘솔](https://console.cloud.tencent.com/im)에서 IM 애플리케이션을 생성해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cf88237a876833c58d50bf4c50f90a97.png)

### 라이브 스트림 푸시 및 재생 도메인 추가

라이브 룸을 구축하려면 라이브 기능이 필수적이며 [CSS](https://console.cloud.tencent.com/live/livestat)를 통해 라이브 기능을 실현할 수 있습니다. 아래 그림과 같이 스트림 푸시 및 재생 도메인을 추가해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c3d16ab2edd963d9e2da6c5e0eb9ea62.png)
자세한 작업 방법은 [외부 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참고하십시오.


### 기본 구성 완료

준비 작업에서 생성된 애플리케이션은 개발에만 적용되는 무료 버전입니다. 프로덕션 환경에서는 필요에 따라 프로 또는 플래그십 에디션을 활성화해야 합니다. 버전별 차이점에 대한 자세한 내용은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

라이브 스트리밍 시나리오에서는 애플리케이션을 생성한 후 몇 가지 추가 구성이 필요합니다.

#### 키로 UserSig 계산하기
IM 계정 시스템에서 사용자 로그인에 필요한 암호는 IM에서 제공한 키를 사용하여 서버에서 계산합니다. 자세한 내용은 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오. 개발 단계에서 클라이언트의 개발 지연을 방지하기 위해 아래와 같이 [콘솔에서 UserSig 계산](https://console.cloud.tencent.com/im/tool-usersig)할 수도 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5075d8e78f6c31da25d8fa2bf2e940f7.png)

#### 관리자 계정 구성

라이브 스트리밍 중에 관리자는 라이브 룸에 메시지를 보내거나 정책을 준수하지 않는 사용자를 음소거(강제 퇴장)해야 할 수 있습니다. 이 작업은 [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621)를 통해 수행할 수 있습니다. 이러한 API를 호출하려면 [IM 관리자 계정 생성](https://console.cloud.tencent.com/im/account-management)을 해야 합니다. 기본적으로 IM은 UserID가 administrator인 계정을 제공합니다. 필요에 따라 여러 관리자 계정을 만들 수도 있으며, 최대 5개의 관리자 계정을 만들 수 있습니다.

#### 콜백 주소 구성 및 콜백 활성화

라이브 룸에서 화면 댓글을 기반으로한 경품 추첨, 메시지 통계 수집, 민감한 콘텐츠 감지 등 요구 사항을 구현하려면 IM 백엔드가 특정 시나리오에서 비즈니스 백엔드를 다시 호출하는 IM 콜백 모듈을 사용해야 합니다. HTTP API를 제공하고 아래와 같이 [콘솔 > 콜백 구성](https://console.cloud.tencent.com/im/callback-setting) 모듈에서 구성하기만 하면 됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/4c9580f801581b5ac4a7a90dcebac706.png)


### 클라이언트 SDK 통합

준비가 끝나면 IM 및CSS 클라이언트 SDK를 프로젝트에 통합해야 합니다. 필요에 따라 다른 통합 옵션을 선택할 수 있습니다.
IM은 [Instant Messaging 시작하기](https://www.tencentcloud.com/document/product/1047/34552)를 참고하십시오.
CSS는 [MLVB SDK 시작하기](https://intl.cloud.tencent.com/document/product/1071/41929)를 참고하십시오.

다음은 라이브 룸의 일반적인 기능을 설명하고 구현 코드와 함께 모범 사례를 제공합니다.

## 2. 라이브 룸 기능 개발 가이드

### 라이브 룸 상태

라이브 룸의 상태는 다음과 같습니다.
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">No.</td>
<th>라이브 룸 상태</td>
</tr>
<tr  ><td>1</td>
<td>시작 예정</td>
</tr><tr  ><td>2</td>
<td>라이브 중</td>
</tr><tr  ><td>3</td>
<td>일시 중지</td>
</tr><tr><td>4</td>
<td>종료</td>
</tr><tr  ><td>5</td>
<td>재생됨</td>
</tr></tbody>
</table>
라이브 룸 상태에는 다음과 같은 특징이 있습니다.
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">No.</td>
<th>특징</td>
</tr><tr  ><td>1</td>
<td>라이브 룸에 있는 사용자에게 라이브 룸 상태 변경을 실시간으로 알려야 합니다.</td>
</tr><tr  ><td>2</td>
<td>라이브 룸을 처음 사용하는 사용자는 라이브 룸의 현재 상태를 확인해야 합니다.</td>
</tr></tbody>
</table>
 

두 가지 구현 스키마가 제공되며 각각의 장단점을 분석하면 다음과 같습니다.

<table selecttype="cells" ><colgroup><col  ><col  ><col  ></colgroup>
<tbody>
<tr  ><th>구현 스키마</td>
<th>장점</td>
<th>단점</td>
</tr><tr  ><td>비즈니스 백엔드는 라이브 룸 상태를 유지하고 IM 서버 API를 사용하여 사용자에게 상태를 알리기 위해 <a href="https://intl.cloud.tencent.com/document/product/1047/34959">Sending Ordinary Messages in a Group</a> 합니다.</td>
<td>라이브 룸 상태를 자주 가져와야 하는 경우 비즈니스 백엔드에 상태를 저장하면 IM 그룹 프로필에 상태를 저장하는 것보다 IM SDK를 호출하는 빈도가 줄어듭니다. <br>이 구현 스키마를 사용하면 IM SDK가 통합되지 않은 경우 라이브 룸 상태를 얻을 수 있습니다.</td>
<td>비즈니스 백엔드는 라이브 룸 상태를 읽고 쓰기 위한 추가 모듈을 제공해야 합니다. <br>데이터는 비즈니스 백엔드와 IM 그룹 프로필 모두에서 가져오기 때문에 라이브 룸 데이터를 가져올 때 예외가 발생할 가능성이 더 큽니다. <br>사용자 정의 메시지를 보낼 때 손실될 수 있습니다. 많은 수의 메시지가 있는 경우 우선순위가 낮은 메시지가 먼저 삭제되어 라이브 룸 상태 표시에 영향을 줍니다. 따라서 우선순위가 높은 사용자 정의 메시지를 사용하는 것이 좋습니다.</td>
</tr><tr  ><td>사용자 정의 그룹 필드 또는 그룹 속성을 통해 라이브 룸 상태를 저장하고 클라이언트 SDK의 <a href="https://intl.cloud.tencent.com/document/product/1047/48175">그룹 속성 변경 콜백</a>을 통해 그룹 사용자에게 알릴 수 있습니다.</td>
<td>라이브 룸 상태를 읽고 쓰기 위한 추가 모듈을 제공할 필요가 없습니다. <br>이론적으로 그룹 속성 변경에 대한 콜백은 손실되지 않습니다. <br>라이브 룸 데이터는 예외를 줄이는 통합 데이터 소스 역할을 하는 그룹 프로필에서 가져옵니다.</td>
<td>고노출 모듈에서 그룹 프로필을 자주 가져와야 하므로 IM에 대한 부담이 커집니다. <br>IM SDK 모듈이 통합되지 않은 경우 비즈니스 백엔드에서 IM 서버 SDK를 호출하여 그룹 프로필을 가져와야 하며 호출 수가 제한됩니다.</td>
</tr></tbody>
</table>


상기 분석을 바탕으로 라이브 룸 상태를 유지하기 위해 다음 두 가지 스키마를 결합할 것을 권장합니다.

1. 라이브 룸에서 스키마1을 사용하여 라이브 룸 상태를 가져옵니다.
2. 라이브 룸 외부에서 스키마2를 사용하여 라이브 룸 상태를 가져옵니다.
3. 비즈니스 백엔드에서 라이브 룸 상태가 변경된 후 [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34621)를 사용하여 데이터를 IM 그룹 프로필([그룹 속성](https://intl.cloud.tencent.com/document/product/1047/44188) 및 [사용자 정의 그룹 필드](https://intl.cloud.tencent.com/document/product/1047/34962))에 즉시 동기화합니다.

### 그룹 유형 선택

라이브 스트리밍 시나리오의 사용자 채팅 섹션에는 다음과 같은 특징이 있습니다.

1. 사용자가 자주 그룹에 가입하고 탈퇴하며 그룹 대화 정보(읽지 않은 횟수 및 lastMessage)를 관리할 필요가 없습니다.
2. 사용자는 승인 없이 그룹에 가입할 수 있습니다.
3. 사용자는 채팅 기록에 신경 쓰지 않고 메시지를 보냅니다.
4. 일반적으로 많은 수의 그룹 구성원이 있습니다.
5. 그룹 구성원 정보를 저장할 필요가 없습니다.

따라서 IM의 [그룹 특성](https://intl.cloud.tencent.com/document/product/1047/33529)에 따라 라이브 룸의 그룹 유형으로 오디오/비디오 그룹(AVChatRoom)을 선택할 수 있습니다.

IM 오디오 비디오 그룹(AVChatRoom)은 다음과 같은 특징이 있습니다.
- **인원 제한이 없으며, 천만 규모의 인터랙티브 라이브 방송 시나리오를 구현할 수 있습니다**.
- 모든 온라인 사용자 대상 푸시 메시지(그룹 시스템 알림)를 지원합니다.
- 그룹 참여 신청 후 관리자의 승인 없이 바로 참여할 수 있습니다.

>? Web용 IM SDK를 사용하면 사용자가 한 번에 하나의 오디오/비디오 그룹(AVChatRoom)에만 참여할 수 있습니다. 사용자가 클라이언트에 로그인하여 라이브 룸 A에 입장하면 [콘솔](https://console.cloud.tencent.com/im/login-message)에서 멀티 클라이언트 로그인이 활성화되고 사용자가 다른 클라이언트에 로그인하여 라이브 룸 B에 입장하면 해당 사용자는 라이브 룸 A에서 제거됩니다.

### 라이브 룸 공지

라이브 룸 공지(토픽)는 각 라이브 룸마다 필요하며, 방에 입장한 후 사용자가 볼 수 있습니다. 또한, 오디오/비디오 그룹 구성원에게 실시간으로 공지 변경 사항을 알려야 합니다. 라이브 룸 상태와 마찬가지로 비즈니스 백엔드 또는 IM 그룹 프로필에 라이브 룸 알림을 저장할 수 있습니다. 그러나 주의가 필요한 몇 가지 추가 사항이 있습니다.

1. 그룹 프로필의 그룹 notification 및 그룹 introduction 필드는 각각 최대 **240**바이트와 **300**바이트를 포함할 수 있습니다.
2. 그룹 프로필의 그룹 notification 및 그룹 introduction 필드는 string 유형만 지원합니다. 이미지와 텍스트로 알림을 생성하려면 json string 유형을 사용할 수 있으며 이미지는 온라인 url에 액세스할 수 있어야 합니다.
3. Web에서 editor를 통해 알림을 설정하는 경우, 보다 구체적으로 html 태그를 포함하는 경우 native에서 구문 분석되지 않을 수 있습니다.

라이브룸 알림은 [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34620) 또는 클라이언트 SDK의 그룹 속성을 통해 설정할 수 있습니다. 클라이언트는 그룹 속성을 통해 현재 그룹 정보를 얻고 GroupListener에서 OnGroupInfoChange를 수신하여 변경된 그룹 속성을 가져옵니다.

예시 코드:

<dx-tabs>
 ::: Android
```java
// 클라이언트에서 그룹 프로필 가져오기
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
      // 그룹 프로필 가져오기 완료
  }

  @Override
  public void onError(int code, String desc) {
      // 그룹 프로필 가져오기 실패
  }
});
// 클라이언트 그룹 프로필 수정
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("수정할 그룹 ID");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // 그룹 프로필 수정 완료
  }

  @Override
  public void onError(int code, String desc) {
      // 그룹 프로필 수정 실패
  }
});
```

::: 

::: iOS & Mac

```swift
[[V2TIMManager sharedInstance] getGroupsInfo:@[@"groupA"] succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // 그룹 프로필 가져오기 완료
} fail:^(int code, NSString *desc) {
    // 그룹 프로필 가져오기 실패
}];
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"수정할 그룹 ID";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // 그룹 프로필 수정 완료
} fail:^(int code, NSString *desc) {
    // 그룹 프로필 수정 실패
}];
```

:::

::: Flutter

```dart
// 그룹 프로필 가져오기
V2TimValueCallback<List<V2TimGroupInfoResult>> groupinfos = await groupManager.getGroupsInfo(groupIDList: ['groupid1']);
// 그룹 프로필 수정
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
    // ... 기타 프로필
  }));
// 콜백
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, changeInfos) {
    // 그룹 정보 변경 콜백
  })));
```

:::

::: Web 

```js
// 그룹 프로필 가져오기
let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['key1','key2'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError) {
  console.warn('getGroupProfile error:', imError); // 세부 그룹 프로필 가져오기 실패 정보
});
// 그룹 프로필 수정
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // 그룹 이름 수정
  introduction: 'this is introduction.', // 그룹 소개 수정
  // v2.6.0부터 그룹 구성원은 그룹 사용자 정의 필드 변경에 대한 그룹 팁 수신과 콘텐츠 획득, 자세한 내용은 Message.payload.newGroupProfile.groupCustomField 참고
  groupCustomField: [{ key: 'group_level', value: 'high'}] // 그룹 사용자 정의 필드 수정
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 수정 완료 후 세부 그룹 프로필
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // 그룹 프로필 수정 실패 정보
});
// v2.6.2부터 SDK는 모두 음소거 및 음소거 해제를 지원합니다. 현재 그룹 내 모든 구성원이 음소거 상태인 경우 그룹 팁을 전달할 수 없습니다.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // true: 전원 음소거, false: 전원 음소거 해제
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 수정 완료 후 세부 그룹 프로필
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // 그룹 프로필 수정 실패 정보
});
```

:::
</dx-tabs>

[다른 SDK의 그룹 프로필 처리 모듈 예시 코드](https://intl.cloud.tencent.com/document/product/1047/48185)

### 메시지 우선순위

라이브 룸에는 많은 수의 사용자 메시지가 있습니다. 각 사용자는 자주 메시지를 보낼 수 있습니다. 전송된 메시지 수가 IM 빈도 제어 임계값에 도달하면 IM 백엔드는 시스템 실행 안정성을 보장하기 위해 일부 메시지를 삭제합니다. 클라이언트의 메시지 수신 빈도가 너무 높으면 메시지의 가독성이 떨어질 수 있으므로 이러한 임계값을 적용해야 합니다.

그룹 메시지에는 세 가지 우선순위가 있으며 백엔드는 우선순위가 높은 메시지를 먼저 전달합니다. 따라서 중요도에 따라 메시지에 대해 다른 우선순위를 설정하십시오.
다음은 3가지 우선순위를 높음에서 낮음 순으로 나열한 것입니다.

| 우선순위 | 설명          |
| -------- | ------------- |
| High     | 높은 우선순위 |
| Normal   | 중간 우선순위 |
| Low      | 낮은 우선순위 |

메시지는 다음 정책에 따라 삭제됩니다.

총 메시지 수에 대한 빈도 제어는 그룹에서 초당 보낼 수 있는 메시지 수를 제한합니다. 기본적으로 값은 40건/초입니다. 값을 초과하면 백엔드에서 우선순위가 높은 메시지를 먼저 전달하고 우선순위가 같은 메시지를 랜덤으로 전달합니다.

빈도 제어에 의해 제한된 메시지는 메시지 기록에 저장되지 않지만, 발신자에게 발송 성공이 반환될 수 있습니다. 이 때, [Callback Before Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34374)가 트리거되지만 [Callback After Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34375)는 트리거되지 않습니다.

따라서 라이브 룸에 대한 메시지 우선순위를 설정해야 합니다.

라이브 룸 메시지는 다음과 같이 중요도에 따라 우선순위가 지정됩니다.

1. 모든 사용자에게 표시되어야 하는 보상 및 선물 메시지
2. 텍스트, 오디오 및 이미지 메시지
3. 좋아요 메시지

>? 일반적으로 C 사용자가 보낸 메시지는 우선순위에 관계없이 화면에 표시됩니다. 많은 수의 메시지가 있는 경우 사용자가 다른 사용자의 메시지 일부가 손실되는 것이 허용됩니다.

메시지 우선순위 설정 예시 코드:
<dx-tabs>
::: Android

```java
// 사용자 정의 메시지 생성
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage("사용자 정의 일대일 메시지".getBytes());
// 메시지 우선순위를 높은 우선순위 메시지로 설정
v2TIMMessage.setPriority(V2TIMMessage.V2TIM_PRIORITY_HIGH)
// 메시지 발송
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onProgress(int progress) {
        // 사용자 정의 메시지에 대한 진행률은 다시 호출되지 않음
    }

    @Override
    public void onSuccess(V2TIMMessage message) {
        // 사용자 정의 그룹 메시지 전송 완료
    }

    @Override
    public void onError(int code, String desc) {
        // 사용자 정의 그룹 메시지 전송 실패
    }
});
```

:::

:::  iOS&Mac

```swift
/ 텍스트 메시지 생성
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"content"];
// 메시지 발송
[V2TIMManager.sharedInstance sendMessage:message
                                receiver:@"userID"
                                 groupID:nil
                                priority:V2TIM_PRIORITY_NORMAL
                          onlineUserOnly:NO
                         offlinePushInfo:nil
                                progress:nil
                                succ:^{
    // 텍스트 메시지 전송 완료
}
                                fail:^(int code, NSString *desc) {
    // 텍스트 메시지 전송 실패
}];
```

:::

::: Flutter

```dart
/ 텍스트 메시지 생성
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;

       // 텍스트 메시지 발송
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // 전송 완료
    }
  }
```

:::

::: Web

```js
// 텍스트 메시지 발송
// 1. 메시지 인스턴스 생성, 반환된 인스턴스 화면에 표시 가능
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // 그룹 채팅에 적용되는 메시지 우선순위(v2.4.2 이상에서 지원). 그룹의 메시지가 빈도 제한을 초과하면 백엔드가 우선순위가 높은 메시지를 먼저 전달합니다. 자세한 내용 참고: https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6)
  // 지원되는 열거 값: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL(기본값), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  },
  // v2.20.0 부터 일대일 메시지에 대해 수신 확인 기능이 지원됩니다. 사용하려면 플래그십 에디션 패키지를 구입하고 메시지 작성 시 needReadReceipt를 true로 설정합니다.
  needReadReceipt: true
  // 클라우드에 저장된 사용자 정의 메시지 데이터 (수신자에게 전송되며 애플리케이션을 제거하고 다시 설치한 후에도 계속 가져올 수 있음, 이 속성은 v2.10.2 이상에서 지원)
  // cloudCustomData: 'your cloud custom data'
});
// 2. 메시지 전송
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // 전송 완료
  console.log(imResponse);
}).catch(function(imError) {
  // 전송 실패
  console.warn('sendMessage error:', imError);
});
```

:::
</dx-tabs>

[다른 SDK의 메시지 우선순위 설정 예시 코드](https://intl.cloud.tencent.com/document/product/213/4855)

### 선물 및 좋아요 메시지 모범 사례

![](https://qcloudimg.tencent-cloud.cn/raw/bf0d1df7fcbf05819643f27091c64e98.png)

#### 선물 메시지

1. 클라이언트의 비영구적 연결 요청은 과금 로직과 관련된 비즈니스 서버로 전송됩니다.
2. 요금이 발생한 후 발신자는 XXX가 XXX 선물을 보낸 것을 볼 수 있습니다. (보내는 사람이 자신이 보낸 선물을 볼 수 있도록, 메시지가 많은 경우 메시지 폐기 정책이 트리거될 수 있음)
3. 요금 정산 후 서버 API를 호출하여 사용자 정의 메시지(선물)를 보낼 수 있습니다.
4. 여러 개의 선물을 연속으로 보낼 경우 메시지를 병합해야 합니다.
   1. 99와 같이 미리 선물 개수를 선택하면 매개변수에 99가 포함된 메시지를 보낼 수 있습니다.
   2. 선물을 여러 번 보내고 총 개수가 불확실한 경우 선물 20개마다 메시지를 보내거나(값 조정 가능) 1초 이내에 클릭할 수 있습니다. 예를 들어 99개의 선물을 연속으로 클릭하면 최적화 후 5개의 메시지만 보내면 됩니다.

#### 좋아요 메시지

1. 선물 메시지와 달리 좋아요 메시지는 청구되지 않으며 고객에게 직접 전송됩니다.
2. 서버에서 집계해야 하는 좋아요 메시지의 경우 클라이언트에서 트래픽 스로틀링이 수행된 후 클라이언트에서 좋아요가 집계되고 짧은 시간 동안의 좋아요 메시지가 하나로 병합됩니다. 비즈니스 서버는 메시지를 보내기 전에 콜백에서 좋아요 수를 얻습니다.
3. 계산할 필요가 없는 유사 메시지의 경우 2단계의 로직이 사용됩니다. 여기서 비즈니스 서버는 클라이언트에서 트래픽 스로틀링이 수행된 후 메시지를 보내고 메시지를 보내기 전에 콜백에서 카운트를 가져올 필요가 없습니다.

### 라이브 룸 사용자의 신분 및 레벨

사용자 레벨의 개념은 대부분의 라이브 룸에 적용됩니다. 다음을 기반으로 가중 사용자 레벨을 결정할 수 있습니다.

1. 라이브 룸 사용자의 온라인 지속 시간
2. 라이브 룸 사용자가 전송 완료한 일반 메시지 수
3. 라이브룸 사용자가 보낸 좋아요 및 선물 수
4. 사용자의 라이브 룸의 회원 권한 보유 여부
5. ...

온라인 지속 시간 및 메시지 수의 경우 준비 지침에 따라 구성할 수 있는 IM 콜백을 사용해야 합니다. [콘솔](https://console.cloud.tencent.com/im/callback-setting)의 콜백은 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6d6fdc21dd0b75dc0f8d8f38e95d5bf0.jpg)

정보 수집을 위한 순서도는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5f1779379a08a66b0647cc368404a439.jpg)


메시지 전송 후 콜백의 예시 데이터:

```json
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // 콜백 명령
    "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
    "Type": "Public", // 그룹 유형
    "From_Account": "jared", // 발신자
    "Operator_Account":"admin", // 요청 개시자
    "Random": 123456, // 랜덤 숫자
    "MsgSeq": 123, // 메시지의 시퀀스 번호
    "MsgTime": 1490686222, // 메시지 시간
    "OnlineOnlyFlag": 1, // 값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다.
    "MsgBody": [ // 메시지 본문, 자세한 내용은 TIMMessage 메시지 객체 참고
        {
            "MsgType": "TIMTextElem", // 텍스트
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

MsgBody의 메시지 유형에 따라 일반, 좋아요, 선물 메시지를 식별할 수 있습니다. 모든 필드에 대한 자세한 내용은 [Callback After Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34375)를 참고하십시오.

사용자 온라인 상태 변경에 대한 콜백 데이터 예시:

```json
{
    "CallbackCommand": "State.StateChange",
    "EventTime": 1629883332497,
    "Info": {
        "Action": "Login",
        "To_Account": "testuser316",
        "Reason": "Register"
    },
    "KickedDevice": [
        {
            "Platform": "Windows"
        },
        {
            "Platform": "Android"
        }
    ]
}
```

온라인 지속 시간을 계산하기 위해 Info의 필드를 기반으로 사용자 온라인 상태를 식별할 수 있습니다. 모든 필드에 대한 자세한 내용은 [State Change Callbacks](https://intl.cloud.tencent.com/document/product/1047/34357)를 참고하십시오.

>?또한, 라이브 룸 인기도를 표시하여 라이브 룸 추천의 기준으로 활용하는 경우가 많습니다. 사용자 수준과 유사하게 결정되며 IM의 콜백 시스템을 통해 구현할 수 있습니다.

### 라이브 룸의 메시지 기록

오디오/비디오 그룹(AVChatRoom)에 대한 메시지 기록은 기본적으로 저장되지 않습니다. 새로운 사용자가 라이브 룸에 입장하면 해당 사용자는 입장 후 보낸 메시지만 볼 수 있습니다. 사용자 경험을 최적화하기 위해 아래와 같이 가져올 수 있는 메시지 기록 수를 구성할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/648238f2a9ebddf3d946494a1fd0cd76.jpg)



>? 이 기능은 플래그십 에디션에서만 사용할 수 있으며 지난 24시간 동안 최대 20개의 메시지 기록을 가져올 수 있습니다.

오디오/비디오 그룹의 메시지 기록은 다른 그룹과 동일한 방식으로 가져옵니다. 샘플 코드:
<dx-tabs>
::: Android

```java
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // 더 오래된 클라우드 메시지 풀링
option.setGetTimeBegin(1640966400);         // 2022-01-01 00:00:00부터 시작
option.setGetTimePeriod(1 * 24 * 60 * 60);  // 하루 전체의 메시지 풀링
option.setCount(Integer.MAX_VALUE);         // 시간 범위 내의 모든 메시지 반환
option.setGroupID(#you group id#);          // 그룹 메시지 풀링
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```

::: 

::: iOS&Mac

```swift
// 일대일 메시지 기록 풀링
// 첫 번째 풀링에 대해 lastMsg를 nil로 설정
// lastMsg는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지일 수 있음
[V2TIMManager.sharedInstance getC2CHistoryMessageList:#your user id# count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // 다음 풀링을 위해 lastMsg 기록
    V2TIMMessage *lastMsg = msgs.lastObject;
    NSLog(@"success, %@", msgs);
} fail:^(int code, NSString *desc) {
    NSLog(@"fail, %d, %@", code, desc);
}];
```

::: 

::: Flutter

```dart
// 일대일 메시지 기록 풀링
// 첫 번째 풀링에 대해 lastMsgID를 null로 설정
// lastMsgID는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지 id일 수 있음
TencentImSDKPlugin.v2TIMManager.getMessageManager().getC2CHistoryMessageList(
        userID: "userId",
        count: 10,
        lastMsgID: null,
);
```

::: 

::: Web

```js
// 대화가 열릴 때 처음 메시지 목록 풀링
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // 메시지 리스트.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // 이 매개변수는 다음 페이지 풀에 전달되어야 합니다.
  const isCompleted = imResponse.data.isCompleted; // 모든 메시지가 풀링되었는지 여부를 나타냅니다.
});
// 메시지 리스트를 풀 다운하여 더 많은 메시지 보기
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // 메시지 리스트.
  const nextReqMessageID = imResponse.data.nextReqMessageID; // 이 매개변수는 다음 페이지 풀에 전달되어야 합니다.
  const isCompleted = imResponse.data.isCompleted; // 모든 메시지가 풀링되었는지 여부를 나타냅니다.
});
```

::: 
</dx-tabs>

[다른 SDK의 메시지 기록 가져오기 예시 코드](https://intl.cloud.tencent.com/document/product/1047/47998)

### 라이브 룸의 온라인 사용자 수

라이브 룸의 온라인 사용자 수를 표시하는 것은 일반적인 기능입니다. 각각 장단점이 있는 두 가지 구현 스키마가 있습니다.

1. 클라이언트 SDK에서 제공하는 [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce) API를 통해 스케쥴된 풀링 방식으로 그룹의 온라인 사용자 수를 가져옵니다.
2. 백엔드에서 그룹에 가입하거나 탈퇴하는 콜백을 기반으로 [Sending System Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34958) 또는 [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)과 같은 서버 API를 통해 모든 그룹 구성원에게 데이터를 전달합니다.

라이브 룸이 하나뿐이라면 클라이언트 SDK의 API를 통해 온라인 사용자 수를 풀링하기에 충분합니다. 온라인 사용자 수를 표시하기 위해 많은 노출 위치가 필요한 라이브 룸이 여러 개 있는 경우 두 번째 스키마를 권장합니다.

>? 서버는 예를 들어 5초마다 한 번씩 스케쥴된 방식으로 온라인 사용자 수 통계 메시지를 클라이언트에 보낼 수 있습니다. 그러나 라이브 룸의 온라인 사용자 수가 급격히 변경되지 않으면 추가 네트워크 오버헤드가 발생합니다. 변경률을 모니터링하여 숫자를 업데이트하는 것이 좋습니다.
>
>필요에 따라 라이브 룸의 온라인 사용자 수의 정확성과 실시간성의 우선순위를 결정할 수 있습니다.

라이브 룸의 온라인 사용자 수를 가져오는 코드는 다음과 같습니다.

<dx-tabs>
::: Android

```java
2TIMManager.getGroupManager().getGroupOnlineMemberCount("group_avchatroom", new V2TIMValueCallback<Integer>() {
  @Override
  public void onSuccess(Integer integer) {
      // 오디오/비디오 그룹(AVChatRoom)의 온라인 구성원 수 가져오기 성공
  }

  @Override
  public void onError(int code, String desc) {
      // 오디오/비디오 그룹(AVChatRoom)의 온라인 구성원 수 가져오기 실패
  }
});
```

::: 

::: iOS&Mac

```swift
[[V2TIMManager sharedInstance] getGroupOnlineMemberCount:@"group_avchatroom" succ:^(NSInteger count) {
    // 오디오/비디오 그룹(AVChatRoom)의 온라인 구성원 수 가져오기 성공
} fail:^(int code, NSString *desc) {
    // 오디오/비디오 그룹(AVChatRoom)의 온라인 구성원 수 가져오기 실패
}];
```

::: 

::: Flutter

```dart
groupManager.getGroupOnlineMemberCount(groupID: '');
```

::: 

::: Web

```js
// 오디오/비디오 그룹의 온라인 사용자 수 가져오기(v2.8.0부터 지원)
let promise = tim.getGroupOnlineMemberCount('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.memberCount);
}).catch(function(imError) {
  console.warn('getGroupOnlineMemberCount error:', imError); // 오디오/비디오 그룹(AVChatRoom)의 온라인 구성원 수 가져오기 실패 관련 오류 정보
});
```

::: 

</dx-tabs>

### 라이브 룸에서 사용자 음소거

라이브 룸에서는 다양한 시나리오에서 모든 사용자 또는 지정된 사용자를 음소거할 수 있습니다.

일반적으로 서버 SDK는 음소거에 사용됩니다. 전체 음소거하려면 [Modifying the Profile of a Group](https://intl.cloud.tencent.com/document/product/1047/34962)에 설명된 대로 그룹 속성의 MuteAllMember 필드를 설정합니다. 지정된 사용자를 음소거하려면 [Bulk Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951)의 지침에 따라 그룹 구성원 속성을 설정하십시오.

라이브 룸 관리자가 백엔드에서 그룹 음소거를 설정할 때 클라이언트는 콜백 이벤트를 수신한 후 타깃 사용자의 입력 상자를 disable 상태로 설정해야 합니다. 그렇지 않으면 사용자는 메시지를 보낼 때 메시지 전송 실패 프롬프트를 받게 됩니다. 사용자의 음소거가 해제되면 클라이언트도 입력 상자를 enable 상태로 설정해야 합니다.

클라이언트의 콜백 코드:

<dx-tabs>
::: Android

```java
// 1분 동안 그룹 구성원 userB 음소거
V2TIMManager.getGroupManager().muteGroupMember("groupA", "userB", 60, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // 그룹 구성원 음소거 성공
  }

  @Override
  public void onError(int code, String desc) {
      // 그룹 구성원 음소거 실패
  }
});

// 모든 구성원 음소거
V2TIMGroupInfo info = new V2TIMGroupInfo();
info.setGroupID("groupA");
info.setAllMuted(true);
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // 모든 구성원 음소거 성공
  }

  @Override
  public void onError(int code, String desc) {
      // 모든 구성원 음소거 실패
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberInfoChanged(String groupID, List<V2TIMGroupMemberChangeInfo> v2TIMGroupMemberChangeInfoList) {
    // 그룹 구성원의 음소거 수신
    for (V2TIMGroupMemberChangeInfo memberChangeInfo : v2TIMGroupMemberChangeInfoList) {
      // 음소거된 사용자의 ID
      String userID = memberChangeInfo.getUserID();
      // 음소거 지속 시간
      long muteTime = memberChangeInfo.getMuteTime();
    }
  }

  @Override
  public void onGroupInfoChanged(String groupID, List<V2TIMGroupChangeInfo> changeInfos) {
    // 모든 구성원 음소거 수신
    for (V2TIMGroupChangeInfo groupChangeInfo : changeInfos) {
      if (groupChangeInfo.getType() == V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // 모든 구성원 음소거 여부
        boolean isMuteAll = groupChangeInfo.getBoolValue();
      }
    }
  }
});
```

::: 

::: iOS&Mac

```swift
// 1분 동안 그룹 구성원 user1 음소거
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // 그룹 구성원 음소거 성공
} fail:^(int code, NSString *desc) {
    // 그룹 구성원 음소거 실패
}];

// 모든 구성원 음소거
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"groupA";
info.allMuted = YES;
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // 모든 구성원 음소거 성공
} fail:^(int code, NSString *desc) {
    // 모든 구성원 음소거 실패
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupMemberChangeInfo *> *)changeInfoList {
    // 그룹 구성원의 음소거 수신
    for (V2TIMGroupMemberChangeInfo *memberChangeInfo in changeInfoList) {
      // 음소거된 사용자의 ID
      NSString *userID = memberChangeInfo.userID;
      // 음소거 지속 시간
        uint32_t muteTime = memberChangeInfo.muteTime;
    }
}

- (void)onGroupInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupChangeInfo *> *)changeInfoList {
    // 모든 구성원 음소거 수신
    for (V2TIMGroupChangeInfo groupChangeInfo in changeInfoList) {
      if (groupChangeInfo.type == V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // 모든 구성원 음소거 여부
        BOOL isMuteAll = groupChangeInfo.boolValue;
      }
    }
}
```

::: 

::: Flutter

```dart
// 10분 동안 그룹 구성원 userB 음소거
groupManager.muteGroupMember(groupID: '',userID: 'userB',seconds: 10);

// 모든 구성원 음소거
groupManager.setGroupInfo(info: V2TimGroupInfo(isAllMuted: true,groupID: '',groupType: 'Public'));

TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {
    //그룹 구성원 정보 변경
  },
  onGroupInfoChanged: (groupID,info){
    // 그룹 프로필 수정
  }
  ));
```

::: 

::: Web 

```js
tim.setGroupMemberMuteTime(options);
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // 10분 동안 사용자 음소거; 0으로 설정되면 사용자 음소거 해제
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 새 그룹 프로필
  console.log(imResponse.data.member); // 새 그룹 구성원 프로필
}).catch(function(imError) {
  console.warn('setGroupMemberMuteTime error:', imError); // 음소거 실패 관련 오류 정보
});
// 주제 내 그룹 구성원 음소거 지속 시간 설정
let promise = tim.setGroupMemberMuteTime({
  groupID: 'topicID',
  userID: 'user1',
  muteTime: 600 // 10분 동안 사용자 음소거; 0으로 설정되면 사용자 음소거 해제
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 새 그룹 프로필
  console.log(imResponse.data.member); // 새 그룹 구성원 프로필
}).catch(function(imError) {
  console.warn('setGroupMemberMuteTime error:', imError); // 음소거 실패 관련 오류 정보
});
// v2.6.2부터 SDK는 모두 음소거 및 음소거 해제를 지원합니다. 현재 그룹 내 모든 구성원이 음소거 상태인 경우 그룹 팁을 전달할 수 없습니다.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // true: 전원 음소거, false: 전원 음소거 해제
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 수정 완료 후 세부 그룹 프로필
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // 그룹 프로필 수정 실패 정보
});
```

::: 
</dx-tabs>

[다른 SDK의 그룹 수신 예시 코드](https://intl.cloud.tencent.com/document/product/1047/48466)

그룹 구성원 음소거 상태의 변경 사항은 기본적으로 클라이언트에 전달되지 않으며 [콘솔](https://console.cloud.tencent.com/im/qun-setting)에서 구성해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/734a516e0507894e087cbbe21d955b17.png)

>?Client SDK는 현재 라이브 룸에서 사용자 음소거를 지원하지 않습니다. 해당 서버 API를 사용하여 [Banning Group Members](https://intl.cloud.tencent.com/document/product/1047/50296) 및 [Unbanning Group Members](https://intl.cloud.tencent.com/document/product/1047/50297)할 수 있습니다.

### 라이브 룸 차단

개발자는 서버의 [Banning Group Members](https://intl.cloud.tencent.com/document/product/1047/50296) API를 통해 라이브 룸의 구성원을 강제 퇴장할 수 있으며, 강제 퇴장된 구성원이 그룹에 다시 들어올 수 없도록 일정 기간 동안 차단할 수 있습니다.


[콘솔 구성 항목](https://console.cloud.tencent.com/im/callback-setting)은 다음과 같습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/120263819a43d755069750ae853623d0.png)


>!** 클라이언트 SDK 6.6.X 이상 버전, Flutter SDK 4.1.1 이상 버전에서는 라이브 룸 구성원 내보내기 API를 사용하여 차단 기능을 구현할 수 있습니다.**

샘플 코드:

<dx-tabs>
::: Android

```java
List<String> userIDList = new ArrayList<>();
userIDList.add("userB");
V2TIMManager.getGroupManager().kickGroupMember("groupA", userIDList, "", new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
      // 구성원 제거 성공
  }

  @Override
  public void onError(int code, String desc) {
      // 구성원 제거 실패
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberKicked(String groupID, V2TIMGroupMemberInfo opUser,
  List<V2TIMGroupMemberInfo> memberList) {
      // 그룹 구성원 제거됨
  }
});
```

::: 

::: iOS&Mac

```swift
[[V2TIMManager sharedInstance] kickGroupMember:@"groupA" memberList:@[@"user1"] reason:@"" succ:^(NSArray<V2TIMGroupMemberOperationResult *> *resultList) {
    // 구성원 제거 성공
} fail:^(int code, NSString *desc) {
    // 구성원 제거 실패
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberKicked:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // 그룹 구성원 제거됨
}
```

::: 

::: Flutter

```dart
groupManager.kickGroupMember(groupID: '',memberList: []);
```

::: 

::: Web

```js
tim.deleteGroupMember(options);
```

::: 

</dx-tabs>

#### 라이브 룸에서 민감한 콘텐츠 필터링

라이브 룸에서 민감한 콘텐츠를 필터링하는 것은 다음과 같이 구현할 수 있는 또 다른 중요한 기능입니다.

1. 그룹 메시지를 보내기 전에 콜백을 바인딩합니다.
2. 콜백 데이터를 기반으로 메시지 유형을 식별하고 메시지 데이터를 Tianyu 또는 다른 타사 점검 서비스에 전달합니다.
3. 메시지가 일반 문자 메시지인 경우 Tianyu의 점검 결과를 기다렸다가 메시지를 IM 백엔드로 전달할지 여부를 나타내는 데이터 패킷을 반환합니다.
4. 메시지가 리치 미디어 메시지인 경우 메시지를 IM 백엔드로 전달하기 위한 데이터 패킷을 반환합니다. Tianyu가 비동기 결과를 반환한 후 메시지가 규정 위반으로 식별되면 메시지 편집 API 또는 사용자 정의 그룹 메시지 API를 통해 메시지 변경 알림을 전달합니다. 알림을 받은 후 클라이언트는 규정 위반 메시지를 차단합니다.

메시지 전송 전 콜백의 예시 데이터:

```json
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // 콜백 명령
    "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
    "Type": "Public", // 그룹 유형
    "From_Account": "jared", // 발신자
    "Operator_Account":"admin", // 요청 개시자
    "Random": 123456, // 랜덤 숫자
    "OnlineOnlyFlag": 1, // 값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다.
    "MsgBody": [ // 메시지 본문, 자세한 내용은 TIMMessage 메시지 객체 참고
        {
            "MsgType": "TIMTextElem", // 텍스트
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

MsgBody의 MsgType 필드를 기반으로 메시지 유형을 식별할 수 있습니다. 필드에 대한 자세한 내용은 [Callback Before Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34374)를 참고하십시오.

규정 위반 메시지를 특정 방식으로 처리하도록 선택할 수 있으며, 이는 IM 백엔드로 반환되는 콜백의 데이터 패킷을 통해 구현할 수 있습니다.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 다른 ErrorCode 값은 다른 의미를 갖습니다.
}
```



| ErrorCode | 설명                                                         |
| --------- | ------------------------------------------------------------ |
| 0         | 발언 허용, 메시지 전달 가능                                  |
| 1         | 발언 거부, 클라이언트 10016 반환                             |
| 2         | 자동 폐기가 활성화되고 클라이언트가 메시지를 정상적으로 반환 |

필요에 따라 사용할 수 있습니다.

민감한 콘텐츠 감지 순서도는 다음과 같습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/fe9f27edee7601b0e6153321887c5eec.png)


### 라이브 룸의 그룹 구성원 목록

`getGroupMemberList` API를 호출하여 표시할 라이브 룸의 온라인 그룹 구성원 목록을 가져올 수 있습니다. 오디오/비디오 그룹(AVChatRoom)은 구성원이 많기 때문에 전체 구성원 목록 풀링 기능은 사용할 수 없습니다. 플래그십 에디션과 그 외의 에디션은 설정이 다릅니다.

1. 플래그십 에디션이 아닌 사용자는 `getGroupMemberList`를 호출하여 최근 30명의 그룹 구성원을 풀링할 수 있습니다.
2. 플래그십 에디션 사용자는 `getGroupMemberList`를 호출하여 최근 1,000명의 그룹 구성원을 풀링할 수 있습니다. 이 기능은 IM 콘솔에서 활성화해야 합니다. 활성화되지 않은 경우 플래그십 이외 기타 에디션에서와 같이 최근 30명의 그룹 구성원만 풀링합니다.

콘솔의 구성은 다음 이미지 2.6과 같습니다.

![img](https://qcloudimg.tencent-cloud.cn/raw/d8b552ecd47be3e749a91ef002bec855.jpg)

플래그십 에디션 사용자가 아닌 경우 `getGroupMemberList`와 그룹 수신의 onGroupMemberEnter 및 onGroupMemberQuit 콜백을 통해 클라이언트의 온라인 그룹 구성원 목록을 유지할 수 있습니다. 단, 사용자가 라이브룸을 나간 후 다시 입장한 후에는 최근 30명의 그룹 구성원만 풀링할 수 있습니다.

<dx-tabs>
::: Android

```java
// filter 매개변수를 통해 그룹 소유자의 프로필을 풀링하도록 지정
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
    @Override
    public void onError(int code, String desc) {
        // 메시지 가져오기 실패
    }

    @Override
    public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
        // 대화 가져오기 성공
    }
});
```

::: 

::: iOS&Mac

```swift
[[V2TIMManager sharedInstance] getGroupMemberList:@"groupA" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberFullInfo *> *memberList) {
    // 대화 가져오기 성공
} fail:^(int code, NSString *desc) {
    // 메시지 가져오기 실패
}];
```

::: 

::: Flutter

```dart
// filter 매개변수를 사용하여 그룹 소유자의 프로필만 가져오도록 지정합니다. filter를 All로 설정하여 모든 그룹 구성원의 프로필을 가져올 수도 있습니다.
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```

::: 

::: Web

```js
tim.getGroupMemberList(options);

```

::: 

</dx-tabs>

### 라이브 룸의 화면 댓글을 기반으로 한 경품 추첨

메시지 통계와 마찬가지로 라이브 스트리밍의 경품 추첨도 메시지를 보낸 후 콜백이 필요합니다. 구체적으로, 메시지 내용이 감지되고 경품 추첨의 키워드에 도달한 사용자가 풀에 추가됩니다.

### 실시간 화면 댓글
 AVChatRoom(오디오/비디오 그룹)은 친근한 인터랙션 경험을 구축하기 위해 화면 댓글, 선물하기 및 좋아요 등 다양한 메시지를 지원합니다.
![](https://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/product/im-new/css/img/scenes/function2.gif)

### 라이브 룸에서 방송

방송 기능은 라이브 룸의 시스템 알림 기능과 유사하지만 메시징에 속한다는 점에서 후자와 다릅니다. 시스템 관리자가 방송 메시지를 전달하면 SDKAppID 아래의 모든 라이브 룸이 이를 수신합니다.

방송 기능은 현재 플래그십 에디션에서만 사용할 수 있으며 콘솔에서 활성화해야 합니다.

비즈니스 백엔드에서 방송 메시지를 보내는 방법에 대한 자세한 지침은 [오디오/비디오 그룹 방송 메시지](https://intl.cloud.tencent.com/document/product/1047/49440)를 참고하십시오.

>?플래그십 에디션 사용자가 아닌 경우 서버에서 사용자 정의 그룹 메시지를 보내 기능을 구현할 수 있습니다.
>

## 3. 라이브 오디오/비디오 스트림

- ### 앵커(스트림 푸시)

  현재 CSS는 스트림을 푸시하는 다음과 같은 방법을 제공합니다.

  1. 클라이언트에서 [OBS 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31569)
  2. Web에서 [Web 푸시](https://console.cloud.tencent.com/live/tools/webpush)
  3. App에서 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38158)

  >? 앵커가 스트림을 푸시할 푸시 주소를 구성해야 하며, 이는 [푸시 스트림 설정](https://intl.cloud.tencent.com/document/product/267/31059)에 따라 생성하거나 [주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 통해 생성할 수 있습니다.

- ### 클라이언트(풀 스트림)

  클라이언트는 다양한 방법으로 라이브 스트림을 얻을 수 있습니다.

  1. PC에서 [VCL 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/32483)
  2. App용 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38160)

  >? 스트림을 가져오려면 재생 주소를 구성해야 하며, 이는 [재생 설정](https://intl.cloud.tencent.com/document/product/267/31058)을 따라 생성하거나 [주소 생성기](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 통해 생성할 수 있습니다. SDK 액세스 과정에 대한 자세한 내용은 [재생](https://www.tencentcloud.com/document/product/267/51155)을 참고하십시오.

- ### 라이브 디렉터

  라이브 스트리밍에 대한 더 많은 요구 사항을 충족하기 위해 [라이브 디렉터](https://console.cloud.tencent.com/live/caster)를 사용하여 라이브 스트림을 처리할 수 있습니다. 현재 라이브 디렉터는 다음 기능을 지원합니다.

  1. 워터마크, 텍스트 및 전환
  2. 라이브 스트리밍을 위한 VOD
  3. 라이브 스트리밍을 위한 정의, 비트레이트 및 해상도 설정
  4. 라이브 스트리밍을 위한 레이아웃 조정
  5. 라이브 녹화
  6. 실시간 화면 댓글 추가
  7. 라이브 스트림 모니터링


- ### 고급 기능 더보기
  
  CSS는 푸시/풀 스트림 서비스 외에도 다음과 같은 고급 기능이 있습니다.
  1. [라이브 리먹싱 및 트랜스코딩](https://intl.cloud.tencent.com/document/product/267/31561), 독점적인 초고속 고화질 트랜스코딩 기술로, 시나리오 동적 인코딩을 지능적으로 인식하고 라이브 고화질 저코드 및 화질 향상을 실현합니다.
  2. [타임 시프트](https://intl.cloud.tencent.com/document/product/267/31565), 라이브 방송 중 하이라이트 영상을 일시 중지 및 다시 볼 수 있도록 지원합니다.
  3. [라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/31563), 라이브 방송 중 동기화 녹화 및 저장이 가능하여 녹화된 비디오의 후속 편집 및 재전파에 편리합니다.
  4. [라이브 방송 워터마크](https://intl.cloud.tencent.com/document/product/267/31073), 생방송 화면에 선명한 워터마크 또는 디지털 워터마크를 겹쳐 영상 도난 방지 효과를 실현합니다.
  5. [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/37665), 설정한 혼합 스트림 레이아웃에 따라 다양한 경로의 입력 소스를 새로운 스트림으로 동기식으로 혼합하여 라이브 인터랙션 효과를 실현할 수 있습니다.
  6. [릴레이](https://intl.cloud.tencent.com/document/product/267/42524), 다른 플랫폼의 라이브 또는 VOD 비디오를 라이브 방송 형태로 배포할 수 있으며, 컨텐츠 풀링 및 푸시 기능을 제공하고,기존 라이브 방송이나 영상을 대상 주소로 푸시합니다.
  
## 4. FAQ
### 1. CSS를 테스트할 수 있나요?
CSS 서비스를 활성화한 신규 사용자에게는 1년간 유효한 20GB의 트래픽이 무료로 제공됩니다. 이때 테스트에 의해 발생하는 트래픽은 이를 이용하여 차감할 수 있으며, 패키지를 초과하는 부분은 후불 일 결산 방식으로 과금됩니다. 동시에 라이브 방송 워터마크, 트랜스코딩, 녹화, 화면 캡처, 음란물 감지 등과 같은 라이브 방송 부가 기능을 사용할 수도 있습니다. 부가 기능은 기본적으로 비활성화되어 있으며, 필요에 따라 사용 및 과금됩니다. 기능에 대한 자세한 내용은 [제품 개요](https://intl.cloud.tencent.com/document/product/267/2822)를 참고하십시오.

### 2. 라이브 방송은 접속 인원 수 제한이 있습니까?
기본적으로 CSS는 네트워크 및 기타 조건이 허용하는 한 라이브 스트림의 온라인 시청자 수를 제한하지 않습니다. 그러나 대역폭 제한을 설정한 경우 기존 시청자가 너무 많아 대역폭 제한을 초과하면 새로운 시청자가 라이브 스트림을 시청할 수 없습니다. 이 경우 온라인 시청자 수에 제한이 있습니다.

### 3. 메시지 전송 중 메시지 전송 상태, `Message.nick`, `Message.avatar` 필드가 비어 있는 경우 UI에 닉네임과 프로필 사진을 표시하려면 어떻게 해야 하나요?
getUserInfo API를 호출하여 사용자 정보에서 nick 및 avatar 필드를 가져와 메시지 전송 필드로 사용합니다.

### 4. 메시지가 손실되는 원인은 무엇입니까?

메시지가 손실되는 가능 원인은 다음과 같습니다.

- 오디오-비디오 그룹에는 초당 40개 메시지의 빈도 제한이 적용됩니다. 메시지 전송 전 콜백과 메시지 전송 후 콜백 수신 여부를 확인할 수 있습니다. 전자는 수신되었지만 후자는 수신되지 않은 경우 빈도 제한으로 인해 메시지가 차단된 것입니다.
- 자세한 내용은 [메시지](https://intl.cloud.tencent.com/document/product/1047/34458)를 참고하십시오. Web 클라이언트 퇴장으로 인해 Android/iOS/PC 클라이언트가 퇴장되는지 확인합니다.
- Web 클라이언트에서 문제가 발생하면 SDK 버전이 v2.7.6 이전인지 확인하십시오. 그렇다면 최신 버전으로 업그레이드하십시오.

상기 원인에 해당되지 않는 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의주시기 바랍니다.



## 5. 고객센터

그룹 번호 검색: 853084820, 더 자세한 답변을 드리겠습니다.

## 기능 설명
* 메시지 기록을 가져오기 위한 API는 `TencentImSDKPlugin.v2TIMManager.getMessageManager()` 클래스에 있습니다.
* 기록 일대일 및 그룹 메시지 풀링 지원 외에도 시퀀스, 시작 지점 또는 시간 범위별로 메시지를 가져오기 위한 고급 API가 제공됩니다.
* 로컬 및 클라우드 메시지 기록을 모두 가져올 수 있습니다.

> ? 클라우드에서 메시지 기록을 가져오고 네트워크 예외가 발견되면 SDK는 로컬에 저장된 메시지 기록을 반환합니다.

로컬에 저장된 메시지 기록에는 시간 제한이 적용되지 않지만 클라우드에 저장된 메시지에는 다음과 같은 시간 제한이 적용됩니다.
* 평가판: 무료 저장 기간은 7일이며 연장할 수 없습니다
* 프로 버전: 무료 저장 기간은 7일이며 연장할 수 있습니다
* 플래그십 버전: 무료 저장 기간은 30일이며 연장할 수 있습니다

> ?
> * 메시지 기록의 저장 기간을 연장하는 것은 부가 가치 서비스입니다. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 관련 구성을 수정할 수 있습니다. 결제에 대한 자세한 내용은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.
> * 리치 미디어 메시지(예: 이미지, 파일 및 오디오 등)는 메시지 기록과 동일한 저장 기간을 갖습니다.

[](id:c2c)

## 일대일 메시지 기록 풀링

`getC2CHistoryMessageList` API ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getC2CHistoryMessageList.html))를 호출하여 일대일 메시지 기록을 가져옵니다.
네트워크가 정상이면 최신 클라우드 데이터를 가져옵니다. 비정상적인 경우 SDK는 로컬에 저장된 메시지 기록을 반환합니다.
로컬 메시지 기록만 가져오려면 [고급 API](#advance)를 참고하십시오.

이 API는 페이지별 풀링을 지원합니다. 자세한 내용은 [페이지별 풀링](#advance_page)을 참고하십시오.

예시 코드는 다음과 같습니다.


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



[](id:group)
## 그룹 메시지 기록 풀링

`getGroupHistoryMessageList` API ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getGroupHistoryMessageList.html))를 호출하여 그룹 메시지 기록을 가져옵니다.
네트워크가 정상이면 최신 클라우드 데이터를 가져옵니다. 비정상적인 경우 SDK는 로컬에 저장된 메시지 기록을 반환합니다.
로컬 메시지 기록만 가져오려면 [고급 API](#advance)를 참고하십시오.

이 API는 페이지별 풀링을 지원합니다. 자세한 내용은 [페이지별 풀링](#advance_page)을 참고하십시오.

> !
> * 회의 그룹(Meeting)의 메시지 기록만 가져올 수 있습니다. 그룹 메시지 제한에 대한 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오.
> * 이 API는 라이브 방송 그룹(AVChatRoom)에 적용되지 않습니다. 메시지가 클라우드 로밍 서버 또는 로컬 데이터베이스에 저장되지 않기 때문입니다.

예시 코드는 다음과 같습니다.


```dart
// 그룹 메시지 기록 풀링
// 첫 번째 풀링에 대해 lastMsgID를 null로 설정
// lastMsgID는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지 id일 수 있음
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .getGroupHistoryMessageList(
        groupID: "groupID",
        count: 10,
        lastMsgID: null,
      );
```


## 고급 기능

[](id:advance)
### 고급 API

위의 일반 API가 메시지 기록을 가져오는 요구 사항을 충족할 수 없는 경우 고급 API `getHistoryMessageList` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getHistoryMessageList.html))를 사용할 수 있습니다.

일대일 및 그룹 메시지 기록을 가져오는 것 외에도 이 API는 다음과 같은 고급 기능을 지원합니다.
* 메시지 풀링의 소스 설정: 로컬 데이터베이스 또는 클라우드에서 풀링.
* 메시지 풀링의 순서 지정: 시간 역순 또는 시간순으로 풀링.
* 로컬 풀링의 메시지 유형 지정: 텍스트, 이미지, 오디오, 비디오, 파일, 이모티콘, 그룹 tips, 병합 또는 사용자 정의 메시지 등.

API 프로토타입:


```dart
    // 일대일 메시지 기록 풀링
    // 첫 번째 풀링에 대해 lastMsgID를 null로 설정
    // lastMsgID는 두 번째 풀링에 대해 반환된 메시지 목록의 마지막 메시지 id일 수 있음
    V2TimValueCallback<List<V2TimMessage>> getHistoryMessageListRes =
        await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .getHistoryMessageList(
      getType: HistoryMsgGetTypeEnum.V2TIM_GET_LOCAL_OLDER_MSG, // 메시지 풀링의 소스 및 시퀀스
      userID: "userID", // 사용자id는 특정 사용자와 일대일 메시지를 풀링하려면 userID만 지정하면 됩니다.
      groupID: "groupID", // 그룹 id는 특정 그룹에서 그룹 메시지를 풀링하려면 groupID만 지정하면 됩니다.
      count: 10, // 데이터 수 풀링
      lastMsgID: null, // 시작 메시지 id 풀링
      // 그룹 채팅만 가능합니다.
      // lastMsgSeq를 메시지 풀링의 시작점으로 설정하면 반환된 메시지 목록에 해당 메시지가 포함됩니다.
      // lastMsg와 lastMsgSeq가 모두 지정된 경우 SDK는 lastMsg를 사용합니다.
      // lastMsg와 lastMsgSeq가 모두 지정되지 않은 경우 getTimeBegin 설정 여부에 따라 풀링 시작 지점이 결정됩니다. 그렇다면 설정된 범위가 시작점으로 사용됩니다. 아니오인 경우 최신 메시지가 시작점으로 사용됩니다.
      lastMsgSeq: -1,
      messageTypeList: [], // 기록 정보 속성을 필터링하는 데 사용되며 비어 있으면 모든 속성 정보를 풀링합니다.
    );
    if (getHistoryMessageListRes.code == 0) {
      //가져오기 성공
    }
```


매개변수 설명:

| 매개변수   | 설명                                                         | 일대일 채팅에 유효 | 그룹 채팅에 유효 | 필수 입력 여부 | 비고                                                         |
| ---------- | ------------------------------------------------------------ | ------------------ | ---------------- | -------------- | ------------------------------------------------------------ |
| getType    | **로컬/클라우드** 및 **역순/시간순**으로 각각 설정할 수 있는 메시지 풀링의 소스 및 시퀀스 | YES                | YES              | YES            | 풀링 소스를 클라우드로 설정하면 로컬 메시지 목록과 클라우드 메시지 목록이 병합되어 반환됩니다. 네트워크 연결이 없으면 로컬 메시지 목록이 반환됩니다. |
| userID     | 일대일 메시지 기록을 가져올 지정된 사용자 ID                 | YES                | <b>NO</font>     | NO             | 특정 사용자와 일대일 메시지를 풀링하려면 userID만 지정하면 됩니다. |
| groupID    | 그룹 메시지 기록을 가져올 지정된 그룹 ID                     | <b>NO</font>       | YES              | NO             | 특정 그룹에서 그룹 메시지를 풀링하려면 groupID만 지정하면 됩니다. |
| count      | 풀링당 메시지 수                                             | YES                | YES              | YES            | iOS/Android는 20으로 설정하는 것이 좋습니다. 그렇지 않으면 풀링 속도에 영향을 줄 수 있습니다. Web의 최댓값은 15입니다. |
| lastMsgID  | 메시지 기록을 풀링할 시작 메시지를 나타내는 마지막 메시지의 ID | YES                | YES              | NO             | 1. 일대일 채팅과 그룹 채팅 모두에 사용할 수 있습니다. <br/>2. lastMsg를 메시지 풀링의 시작점으로 설정하면 이 메시지는 반환된 메시지 목록에 **포함되지 않습니다**. <br/>3. 비워두면 대화의 가장 최근 메시지가 끌어오기 시작점으로 사용됩니다. |
| lastMsgSeq | 메시지 기록을 풀링할 시작 메시지를 나타내는 마지막 메시지의 seq | <b>NO</font>       | YES              | NO             | 1. 그룹 채팅만 가능합니다. <br/>2. lastMsgSeq를 메시지 풀링의 시작점으로 설정하면 반환된 메시지 목록에 해당 메시지가 **포함됩니다**.<br/>3. lastMsg와 lastMsgSeq가 모두 지정된 경우 SDK는 lastMsg를 사용합니다. <br/>4. lastMsg와 lastMsgSeq가 모두 지정되지 않은 경우 getTimeBegin 설정 여부에 따라 풀링 시작 지점이 결정됩니다. 그렇다면 설정된 범위가 시작점으로 사용됩니다. 아니오인 경우 최신 메시지가 시작점으로 사용됩니다. |


[](id:advance_page)
### 페이지별 풀링

[일대일 메시지 기록 풀링](#c2c), [그룹 메시지 기록 풀링](#group) 및 [고급 API를 통한 풀링](#advance)은 모두 `lastMsg` 및 `count` 를 사용하여 페이징할 수 있습니다.

* 페이지별 풀링은 `lastMsg` 및 `count`를 사용하여 구현할 수 있습니다. 첫 번째 풀링의 경우 `lastMsg`를 비워둘 수 있습니다. 이는 반환된 메시지 목록의 마지막 메시지가 다음 페이지의 데이터를 풀링하기 위한 `lastMsg`로 사용됨을 나타냅니다.
* `lastMsg`가 비어 있으면 SDK는 기본적으로 최신 메시지부터 메시지 기록을 반환합니다.
* `lastMsg`가 설정되면 반환된 메시지 목록에는 설정된 `lastMsg`가 포함되지 않습니다.
* 반환된 메시지 목록에는 역순으로 메시지가 표시됩니다.

>?
>1. 메시지 기록 풀링 속도에 영향을 주지 않으려면 페이징에 대해 `count`를 20으로 설정하는 것이 좋습니다.
>2. 해당 메시지가 반환된 메시지 목록에 포함되므로 후속 가져오기에는 `lastMsgSeq`를 사용하지 않는 것이 좋습니다.

### 로컬 메시지만 풀링

로컬 메시지만 풀링하도록 `getType`을 설정합니다.

* `getType`이 `V2TIM_GET_LOCAL_OLDER_MSG`로 설정되면 로컬에 저장된 메시지가 역순으로 풀링됩니다.
* `getType`이 `V2TIM_GET_LOCAL_NEWER_MSG`로 설정되면 로컬에 저장된 메시지를 시간순으로 가져옵니다.

다음 예시 코드는 최신 메시지부터 역순으로 로컬 데이터베이스에서 20개의 일대일 메시지를 가져오는 프로세스를 보여줍니다.


```dart
TencentImSDKPlugin.v2TIMManager.getMessageManager().getHistoryMessageList(
        count: 10,
        getType: HistoryMsgGetTypeEnum.V2TIM_GET_LOCAL_OLDER_MSG,
        userID: "userID",
);
```


[](id:advance_group_at)

### 그룹 @ 메시지로 리디렉션한 후 메시지 풀링

사용자가 그룹 대화에서 그룹 @ 메시지를 받은 후 사용자는 일반적으로 @ 표시줄을 클릭하여 메시지로 이동하고 표시할 인접 메시지를 풀링해야 합니다.
그룹 @ 메시지도 표시해야 하므로 `sequence`를 lastMsgSeq로 설정하고 [고급 API](#advance)를 사용하여 메시지를 풀링할 수 있습니다.

다음 예시 코드는 @ 표시줄을 클릭하고 그룹 @ 메시지로 리디렉션하고 해당 메시지보다 앞과 뒤의 처음 20개 메시지를 표시용으로 풀링하는 프로세스를 보여줍니다.



```dart
// 그룹 @ 메시지의 sequence 가져오기
int atSequence = 1081;

// 그룹 @ 메시지와 이전 메시지 풀링

  TencentImSDKPlugin.v2TIMManager.getMessageManager().getHistoryMessageList(
        count: 20, // 20개의 메시지 풀링
        getType: HistoryMsgGetTypeEnum.V2TIM_GET_CLOUD_OLDER_MSG, // 그룹 @ 메시지보다 먼저 메시지 풀링
        lastMsgSeq: atSequence,// 풀 목록에 포함된 그룹 @ 메시지에서 풀링 시작
        groupID: "groupID" // 그룹 메시지 풀링
      );



// 그룹 @ 메시지 이후에 메시지 풀링
TencentImSDKPlugin.v2TIMManager.getMessageManager().getHistoryMessageList(
        count: 20, // 20개의 메시지 풀링
        getType: HistoryMsgGetTypeEnum.V2TIM_GET_CLOUD_NEWER_MSG, // 그룹 @ 메시지 이후에 메시지 풀링
        lastMsgSeq: atSequence,// 풀 목록에 포함된 그룹 @ 메시지에서 풀링 시작
        groupID: "groupID" // 그룹 메시지 풀링
      );
```



[](id:qa)
## FAQ

[](id:qa1)
### 1. 메시지 기록을 가져올 때 로그에 "total count of request cloud message exceed max limit"이 표시되면 어떻게 해야 합니까?

현재 SDK 정책은 다음과 같습니다.
1. getType이 클라우드 메시지 기록을 풀링하도록 설정되고 풀링할 메시지 수가 x로 설정된 경우 SDK는 클라우드에서 x개의 메시지를 풀링합니다.
2. SDK는 삭제된 메시지 및 현재 사용자와 관련 없는 메시지와 같은 유효하지 않은 메시지를 필터링합니다.
3. 클라우드에 유효하지 않은 메시지 기록이 너무 많으면 SDK가 여러 페이징 풀링을 수행합니다.
시스템 안정성과 견고성을 보장하기 위해 SDK는 최대 3개의 자동 페이징 가져오기를 수행합니다. 이 한도를 초과하면 “total count of request cloud message exceed max limit”라는 메시지가 로그에 표시됩니다.

이러한 제한 메커니즘이 비즈니스 레이어에 미치는 영향을 최소화하려면 다음 조치를 취하여 유효하지 않은 메시지를 줄이십시오.
* 온라인 메시지를 사용할 수 있습니다. 즉, 메시지를 보낼 때 `onlineUserOnly `를 `YES/true`로 설정하십시오.
* 그룹 메시지의 경우 대상 그룹 메시지를 사용하여 수신자를 지정합니다.

[](id:qa2)
### 2. 클라우드 메시지 기록 가져오기 중에 메시지가 ‘손실’된 경우 어떻게 해야 합니까?
getType이 클라우드 메시지 기록을 가져오도록 설정되고 메시지 수가 count인 경우 SDK는 다음 작업을 수행합니다.
1. 로컬 데이터베이스에서 count 메시지를 가져옵니다.
2. 클라우드에서 count 메시지를 가져오고 삭제된 메시지와 같은 유효하지 않은 메시지를 필터링합니다. 숫자가 count보다 작으면 페이징 풀링이 트리거됩니다.
3. 로컬 및 클라우드 메시지를 병합하고 메시지 상태와 같은 정보를 업데이트합니다.
4. 병합된 메시지 목록에서 count 메시지를 반환합니다.

일반적으로, 메시지 ‘손실’은 2단계에서 너무 많은 유효하지 않은 메시지 풀링을 나타내며, 이는 [질문 1의 제한 메커니즘](#qa1)을 트리거하고 실제로 클라우드에서 풀링한 메시지 수가 충분하지 않게 됩니다.
[질문 1의 해결 방법](#qa1)에 설명된 대로 이 문제를 해결하는 것이 좋습니다.

[](id:qa3)
### 3. 메시지 기록 풀링 시 그룹 명함 등 그룹 구성원 정보가 실시간으로 업데이트 되지 않는 경우 어떻게 해야 하나요?
* 메시지가 생성되면 SDK는 그룹 이름 카드 및 role과 같은 현재 그룹 구성원 정보를 업데이트하고 로컬 데이터베이스에 저장합니다.
* 그룹 메시지 기록을 풀링하면 SDK는 메시지가 생성되었을 때 그룹 구성원 정보를 직접 반환하고 실시간으로 업데이트하지 않습니다.

최신 그룹 구성원 정보를 얻으려면 `getGroupMembersInfo`([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMGroupManager/getGroupMembersInfo.html)) API를 사용할 수 있습니다.


[](id:qa4)
### 4. 메시지 기록 풀링 시 랙이 발생하면 어떻게 해야 합니까?
SDK는 메시지 풀링에 최적화되었습니다. 랙이 발생하면 풀링한 메시지 수(`count`)를 줄일 수 있습니다. 

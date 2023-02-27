## 기능 설명

대화 상단 고정은 친구나 그룹 대화를 사용자가 찾기 편리하게 대화 목록 상단에 고정하는 것을 의미합니다. 상단 고정 상태는 서버에 저장되며 단말 장치 전환 후 상단 고정 상태는 새 장치에 동기화됩니다.

>!최대 50개의 대화를 상단 고정할 수 있으며, 이 상한은 늘릴 수 없습니다.

## 대화 상단 고정

`pinConversation`([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/pinConversation.html)) API를 호출하여 대화 상단 고정 여부를 설정할 수 있습니다.

'V2TimConversation' 객체의 'orderKey' 필드로 정렬된 대화 순서입니다. 'orderKey' 필드는 정수이며, 새 메시지를 발송, 수신, 초안 설정 또는 대화 상단에 고정하면 대화가 활성화되고 'orderKey' 필드가 증가합니다.

상단 고정된 대화는 항상 상단에 고정되지 않은 대화의 앞에 있으며 동시에 여러 대화가 상단 고정된 경우 이들 대화 간의 상대적인 순서는 유지된다는 점에 유의해야 합니다. 예를 들어, 1, 2, 3, 4, 5 순으로 정렬된 5개의 대화가 있고 동시에 대화 2, 3이 상단에 고정됩니다. 상단 고정 후 순서는 2, 3, 1, 4, 5입니다. 대화 2와 3이 상위에 있으며 대화 2는 여전히 3보다 앞에 있습니다.

대화 목록을 가져오기 위해 'getConversationList'를 호출할 때 이 API는 먼저 상단 고정 대화를 반환한 다음 상단 고정이 아닌 대화를 반환합니다. 'V2TIMConversation' 객체의 `isPinned` 필드를 사용하여 대화가 상단에 고정되었는지 여부를 확인할 수 있습니다.

예시 코드는 다음과 같습니다.

```javascript
// isPinned 매개변수가 true이면 대화 상단 고정을 의미하고, 그렇지 않으면 상단 고정 취소를 의미합니다.
const isPinned = true;
conversationManager.pinConversation("conversationID", isPinned);
```

## 대화 상단 고정 변경 알림

사전에 대화 리스너를 추가하기 위해 `addConversationListener`([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/addConversationListener.html)) 를 호출하면 `onConversationChanged`에서 `V2TimConversation` 객체의 `isPinned` 필드 값을 가져올 수 있습니다. 이 필드에 따라 대화의 상단 고정 상태 변경 여부를 판단할 수 있습니다.
예시 코드는 다음과 같습니다.

```javascript
conversationManager.addConversationListener({
  onConversationChanged: (conversationList) => {
    // 변경 후 마지막 대화
  },
});
```

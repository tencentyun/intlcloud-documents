## 기능 설명

- `addAdvancedMsgListener`의 프로토콜에 콜백이 정의되어 있는 `V2TimAdvancedMsgListener` API를 사용하여 모든 유형의 메시지(텍스트, 사용자 지정 및 리치 미디어 메시지)를 수신합니다.

## 메시지 리스너 설정

### 고급 메시지 리스너

#### 리스너 추가

수신자는 `addAdvancedMsgListener` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/addAdvancedMsgListener.html)) API를 호출하여 고급 메시지 리스너를 추가합니다. App에서 적시에 메시지를 수신할 수 있도록 (예: 채팅 페이지가 초기화된 후) API를 일찍 호출하는 것이 좋습니다.

예시 코드는 다음과 같습니다.

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

TencentImSDKPlugin.v2TIMManager.getMessageManager().addAdvancedMsgListener(
        {
          onRecvC2CReadReceipt: ( receiptList) {},// C2C 메시지 읽기 알림(수신자가 markC2CMessageAsRead를 호출하면 알림이 수신됨)
          onRecvMessageModified: ( message) {},// 메시지 내용이 수정됨
          onRecvMessageReadReceipts: ( receiptList) {},// 메시지 수신 확인 알림(수신 확인이 지원되는 경우 수신자가 sendMessageReadReceipts를 호출할 때 알림 수신)
          onRecvMessageRevoked: ( messageid) {},// 메시지 회수 알림 수신
          onRecvNewMessage: ( message) {},// 새 메시지 수신
          onSendMessageProgress: ( message,  progress) {},// 메시지 업로드 진행 이벤트
        }
);
```

#### 리스너 제거

메시지 수신을 중지하기 위해 수신자는 `removeAdvancedMsgListener` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/removeAdvancedMsgListener.html))를 호출하여 고급 메시지 리스너를 제거합니다.

예시 코드는 다음과 같습니다.

```javascript
import { TencentImSDKPlugin } from 'react-native-tim-js';

// listener 생성
const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {},
    onSendMessageProgress: (message, progress) {},
  };
// listener 등록
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
// listener 제거
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener);
```

## 문자 메시지 수신

수신자는 다음 단계에서 고급 메시지 리스너를 사용하여 일대일 또는 그룹 문자 메시지를 받을 수 있습니다.

1. 이벤트 리스너를 설정하려면 `addAdvancedMsgListener`를 호출하십시오.
2. 텍스트 메시지가 포함된 `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html)) 콜백을 수신합니다.
3. 메시지 수신을 중지하려면 `removeAdvancedMsgListener`를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.

예시 코드는 다음과 같습니다.

```javascript

import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        const text = message.textElem.text;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## 사용자 정의 메시지 수신

수신자는 다음 단계에서 고급 메시지 리스너를 사용하여 사용자 지정 일대일 또는 그룹 메시지를 받을 수 있습니다.

1. 이벤트 리스너를 설정하려면 `addAdvancedMsgListener`를 호출하십시오.
2. `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html)) 콜백을 수신합니다.
3. 메시지 수신을 중지하려면 `removeAdvancedMsgListener`를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.

예시 코드는 다음과 같습니다.

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        const text = message.textElem.text;
        const data = message.customElem.data;
        const desc = message.customElem.desc;
        const ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (message, progress) {},
  };
TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener);
```

## 리치 미디어 메시지 수신

수신자는 다음 단계에서 고급 메시지 리스너를 **통해서만** 리치 미디어 메시지를 수신할 수 있습니다.

1. `addAdvancedMsgListener` API를 호출하여 고급 메시지 리스너를 설정합니다.
2. `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Callback/OnRecvNewMessage.html)) 콜백을 수신하여 V2TimMessage 메시지를 가져옵니다.
3. V2TIMMessage 메시지에서 elemType 속성을 구문 분석한 다음 유형에 따라 메시지를 다시 구문 분석하여 메시지 Elem의 특정 콘텐츠를 가져옵니다.
4. 메시지 수신을 중지하려면 `removeAdvancedMsgListener`를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.

### 이미지 메시지

이미지 메시지의 이미지는 원본, 대형 및 썸네일의 세 가지 형식이 될 수 있습니다. 후자의 두 개는 메시지 전송 중에 SDK에 의해 자동으로 생성되며 무시할 수 있습니다.
대형 이미지: 원본 이미지를 비례 압축하여 얻은 이미지입니다. 압축 후 높이와 너비 중 짧은 쪽이 720픽셀이 됩니다.
썸네일: 원본 이미지를 비례 압축하여 얻은 이미지입니다. 압축 후 높이와 너비 중 짧은 쪽이 198픽셀이 됩니다.

리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

다음 예시 코드는 V2TimMessage에서 이미지 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
import { TencentImSDKPlugin, MessageElemType} from 'react-native-tim-js';

const listener = {
    onRecvC2CReadReceipt: (receiptList) {},
    onRecvMessageModified: (message) {},
    onRecvMessageReadReceipts: (receiptList) {},
    onRecvMessageRevoked: (messageid) {},
    onRecvNewMessage: (message) {
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE){
        const path = message
            .imageElem.path; // 이미지 업로드 경로. 이 필드는 경험을 최적화하기 위해 미리 화면에 이미지를 표시하는 데 사용할 수 있는 메시지 발신자에게만 적용됩니다.
        message.imageElem.imageList.map(item => { // 대형 이미지, 원본 이미지 및 썸네일 트래버스
          // 이미지 속성 구문 분석
          const height = item.height;
          const localUrl = item.localUrl;
          const size = item.size;
          const type = item.type; // 대형 이미지, 썸네일, 원본 이미지
          const url = item.url;
          const uuid = item.uuid;
          const width = item.width;
        })
      }
    TencentImSDKPlugin.v2TIMManager
       .getMessageManager()
       .getMessageOnlineUrl(message.msgID);

    TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(message, 3, 0, false);
    },
    onSendMessageProgress: (message, progress) {},
  };
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);


```

### 비디오 메시지

비디오 메시지를 받은 후 채팅 페이지에 비디오 미리보기가 표시되고 사용자가 메시지를 클릭하면 비디오가 재생됩니다.
두 단계가 필요합니다.

리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

다음 예시 코드는 V2TimMessage에서 비디오 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO) {
  // 썸네일, 재생 주소, 너비 및 높이, 크기와 같은 비디오 메시지 속성을 구문 분석합니다.
  message.videoElem.UUID;
  message.videoElem.duration;
  message.videoElem.localSnapshotUrl;
  message.videoElem.localVideoUrl;
  message.videoElem.snapshotHeight;
  message.videoElem.snapshotPath;
  // ...
  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 5, 0, true);
}
```

### 음성 메시지

리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

다음 예시 코드는 V2TimMessage에서 오디오 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND) {
  // 음성 메시지의 재생 주소, 로컬 주소, 크기 및 기간을 구문 분석합니다.
  message.soundElem.UUID;
  message.soundElem.dataSize;
  message.soundElem.duration;
  message.soundElem.localUrl;
  message.soundElem.url;
  // ...
  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 4, 0, true);
}
```

### 파일 메시지

React Native SDK는 무료일 때 파일 메시지를 다운로드하여 직접 사용할 수 있으며 App이 제거되면 지워집니다.

다음 예시 코드는 V2TimMessage에서 파일 내용을 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE) {
  // 파일 메시지의 파일 이름, 크기, url 및 기타 정보를 구문 분석합니다
  message.fileElem.UUID;
  message.fileElem.fileName;
  message.fileElem.fileSize;
  message.fileElem.localUrl;
  message.fileElem.path;
  message.fileElem.url;

  TencentImSDKPlugin.v2TIMManager
     .getMessageManager()
     .getMessageOnlineUrl(message.msgID);

  TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(message, 6, 0, true);
}
```

### 지리적 위치 메시지

지리적 위치 메시지를 수신한 후 수신자는 `locationElem`에서 직접 위도 및 경도 정보를 구문 분석할 수 있습니다.
다음 예시 코드는 V2TimMessage에서 지리적 위치 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION) {
  // 위도, 경도, 설명과 같은 지리적 위치 정보를 구문 분석합니다
  message.locationElem.desc;
  message.locationElem.latitude;
  message.locationElem.longitude;
}
```

### 이모티콘 메시지

SDK는 이모티콘 메시지에 대한 메시지 패스스루 채널만 제공합니다. 메시지 콘텐츠 필드의 경우 `index` 및 `data`의 콘텐츠가 사용자에 의해 사용자 지정되는 `faceElem` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Interface/Message/V2TimFaceElem.html))을 참고하십시오.

예를 들어 발신자는 index = 1, data = "x12345"로 설정하여 ‘스마일’ 이모티콘을 나타낼 수 있습니다.
수신자는 수신한 이모티콘 메시지를 1과 "x12345"로 구문 분석하여 미리 설정된 규칙에 따라 ‘스마일’ 이모티콘으로 표시합니다.

다음 예시 코드는 V2TIMMessage에서 이모티콘 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
  message.faceElem.data;
  message.faceElem.index;
}
```

### 그룹 tips 메시지

그룹 tips 메시지는 ‘관리자가 그룹 채팅에서 alice를 제거했습니다’, ‘bob이 그룹 이름을 xxxx로 변경했습니다’와 같이 그룹 채팅에서 일반 메시지 이외의 사용자가 받는 팁 메시지 입니다.

> ? 그룹 tips 메시지는 그룹 구성원에게만 적용됩니다.

`V2TIMGroupTipsElem` ([상세 보기](https://comm.qq.com/im/doc/RN/zh/Interface/Message/V2TimGroupTipsElem.html))에 설명된 대로 여러 유형의 그룹 tips 메시지가 있습니다.

그룹 tips 메시지를 받은 후 수신자는 일반적으로 다음을 수행해야 합니다.

1. `V2TIMGroupTipsElem`의 모든 필드를 구문 분석합니다.
2. type에 따라 tips 메시지 유형을 식별합니다.
3. 유형에 따라 표시할 콘텐츠에 다른 필드를 병합합니다.

예를 들어:
type = `V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE`는 유형에서 구문 분석되어 그룹 프로필 변경 알림임을 나타냅니다.
수신자는 `opMember`에서 운영자 정보를 얻을 수 있고 `groupChangeInfoList`에서 새 그룹 이름을 얻을 수 있습니다.
이 시점에서 수신자는 ‘운영자’와 ‘새 그룹 이름’을 병합하여 ‘alice가 그룹 이름을 group123으로 이름을 바꿨습니다’와 같은 그룹 팁을 만들 수 있습니다.

다음 예시 코드는 V2TIMMessage에서 tips 콘텐츠를 구문 분석하는 방법을 보여줍니다.

```javascript
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS) {
  message.groupTipsElem.groupID; // 그룹
  message.groupTipsElem.type; // 그룹 Tips 유형
  message.groupTipsElem.opMember; // 운영자 프로필
  message.groupTipsElem.memberList; // 운영 중인 사용자 프로필
  message.groupTipsElem.groupChangeInfoList; // 그룹 정보 변경 내역
  message.groupTipsElem.memberChangeInfoList; // 그룹 구성원 변경 정보
  message.groupTipsElem.memberCount; // 현재 온라인 그룹 구성원 수
}
```

## 여러 Elem 객체가 포함된 메시지 수신

1. Message 객체에서 첫 번째 Elem 객체를 구문 분석합니다.
2. 첫 번째 Elem 객체의 nextElem 메소드를 통해 다음 Elem 객체를 가져옵니다. 다음 객체가 있으면 Elem 객체 인스턴스가 반환됩니다. 그렇지 않으면 null이 반환됩니다.

예시 코드는 다음과 같습니다.

```javascript
if (message.textElem.nextElem != null) {
  // 다음 요소가 있습니다.
}
```

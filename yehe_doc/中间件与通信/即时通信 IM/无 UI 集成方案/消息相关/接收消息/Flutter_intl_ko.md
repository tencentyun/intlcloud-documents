## 기능 설명
`addAdvancedMsgListener` API는 `V2TimAdvancedMsgListener` 프로토콜에 정의된 콜백과 함께 모든 유형의 메시지(텍스트, 사용자 지정 및 리치 미디어 메시지)를 수신하는 데 사용됩니다.


## 메시지 리스너 설정

### 고급 메시지 리스너

#### 리스너 추가
수신자는 `addAdvancedMsgListener` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/addAdvancedMsgListener.html))를 호출하여 고급 메시지 리스너를 추가합니다. 채팅 페이지가 초기화된 후와 같이 초기에 호출하여 App에서 적시에 메시지를 수신할 수 있도록 하는 것이 좋습니다.

예시 코드는 다음과 같습니다.


```dart
    // 메시지 리스너 생성
    V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
      onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {
        //일대일 메시지 읽기 콜백
      },
      onRecvMessageModified: (V2TimMessage message) {
        // msg는 수정된 메시지 객체
      },
      onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {
        //그룹 메시지 읽기 콜백
        receiptList.forEach((element) {
          element.groupID; // 그룹 id
          element.msgID; // 수신 확인 메시지 ID
          element.readCount; // 최신 그룹 메시지 읽음 수
          element.unreadCount; // 최신 그룹 메시지 읽지 않음 수
          element.userID; //  C2C 메시지 상대방 ID
        });
      },
      onRecvMessageRevoked: (String messageid) {
        // 로컬 점검 메시지에서 상대방이 철회한 메시지 처리
      },
      onRecvNewMessage: (V2TimMessage message) async {
        // 텍스트 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT) {
          message.textElem?.text;
        }
        // 사용자 정의 메시지 사용
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM) {
          message.customElem?.data;
          message.customElem?.desc;
          message.customElem?.extension;
        }
        // 이미지 메시지 사용
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
          message.imageElem
              ?.path; // 이미지 업로드 경로. 이 필드는 경험을 최적화하기 위해 미리 화면에 이미지를 표시하는 데 사용할 수 있는 메시지 발신자에게만 적용됩니다.
          message.imageElem?.imageList?.forEach((element) {
            // 대형 이미지, 원본 이미지 및 썸네일 트래버스
            // 이미지 속성 구문 분석
            element?.height;
            element?.localUrl;
            element?.size;
            element?.type; // // 대형 이미지, 썸네일 또는 원본 이미지
            element?.url;
            element?.uuid;
            element?.width;
          });
        }
        // 영상 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO) {
          // 썸네일, 재생 주소, 너비와 높이, 크기와 같은 비디오 메시지 속성을 구문 분석합니다.
          message.videoElem?.UUID;
          message.videoElem?.duration;
          message.videoElem?.localSnapshotUrl;
          message.videoElem?.localVideoUrl;
          message.videoElem?.snapshotHeight;
          message.videoElem?.snapshotPath;
          // ...
        }
        // 오디오 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND) {
          // 오디오 메시지의 재생 주소, 로컬 주소, 크기 및 지속 시간을 구문 분석합니다.
          message.soundElem?.UUID;
          message.soundElem?.dataSize;
          message.soundElem?.duration;
          message.soundElem?.localUrl;
          message.soundElem?.url;
          // ...
        }
        // 파일 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE) {
          // 파일 메시지의 파일 이름, 크기, URL 및 기타 정보를 구문 분석합니다
          message.fileElem?.UUID;
          message.fileElem?.fileName;
          message.fileElem?.fileSize;
          message.fileElem?.localUrl;
          message.fileElem?.path;
          message.fileElem?.url;
        }
        // 위치 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION) {
          // 위도, 경도, 설명과 같은 지리적 위치 정보를 구문 분석합니다
          message.locationElem?.desc;
          message.locationElem?.latitude;
          message.locationElem?.longitude;
        }
        // 이모티콘 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
          message.faceElem?.data;
          message.faceElem?.index;
        }
        // 그룹 tips 문자 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS) {
          message.groupTipsElem?.groupID; // 그룹
          message.groupTipsElem?.type; // 그룹 Tips 유형
          message.groupTipsElem?.opMember; // 운영자 프로필
          message.groupTipsElem?.memberList; // 운용 중인 사용자 프로필
          message.groupTipsElem?.groupChangeInfoList; // 그룹 정보 변경 내역
          message.groupTipsElem?.memberChangeInfoList; // 그룹 구성원 변경 정보
          message.groupTipsElem?.memberCount; // 현재 온라인 그룹 구성원 수
        }
        // 병합된 메시지 처리
        if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_MERGER) {
          message.mergerElem?.abstractList;
          message.mergerElem?.isLayersOverLimit;
          message.mergerElem?.title;
          V2TimValueCallback<List<V2TimMessage>> download =
              await TencentImSDKPlugin.v2TIMManager
                  .getMessageManager()
                  .downloadMergerMessage(
                    msgID: message.msgID!,
                  );
          if (download.code == 0) {
            List<V2TimMessage>? messageList = download.data;
          }
        }
        if (message.textElem?.nextElem != null) {
          //첫 번째 Elem 객체의 nextElem 메소드를 통해 다음 Elem 객체를 가져옵니다. 다음 Elem 객체가 있으면 Elem 객체 인스턴스가 반환됩니다. 그렇지 않으면 null이 반환됩니다.
        }
      },
      onSendMessageProgress: (V2TimMessage message, int progress) {
        //파일 업로드 진행률 콜백
      },
    );
    // 고급 메시지 이벤트 리스너 추가
    TencentImSDKPlugin.v2TIMManager
        .getMessageManager()
        .addAdvancedMsgListener(listener: listener);
```


#### 리스너 제거
메시지 수신을 중지하기 위해 수신자는 `removeAdvancedMsgListener` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/removeAdvancedMsgListener.html))를 호출하여 고급 메시지 리스너를 제거합니다.

예시 코드는 다음과 같습니다.


```dart
// listener 생성
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {},
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
// listener 등록
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
// listener 제거
TencentImSDKPlugin.v2TIMManager.getMessageManager().removeAdvancedMsgListener(listener: listener);
```



## 문자 메시지 수신

수신자는 다음 단계에서 고급 메시지 리스너를 사용하여 일대일 또는 그룹 문자 메시지를 받을 수 있습니다.
1. 이벤트 리스너를 설정하려면 `addAdvancedMsgListener`를 호출하십시오.
2. 사용자 정의 메시지가 포함된 `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) 콜백을 수신합니다.
3. 메시지 수신을 중지하려면 `removeAdvancedMsgListener` 를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.

예시 코드는 다음과 같습니다.


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // 텍스트 메시지 처리
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_TEXT){
        String text = message.textElem.text;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## 사용자 정의 메시지 수신

수신자는 다음 단계에서 고급 메시지 리스너를 사용하여 사용자 지정 일대일 또는 그룹 메시지를 받을 수 있습니다.
1. 이벤트 리스너를 설정하려면 `addAdvancedMsgListener`를 호출하십시오.
2. 사용자 정의 메시지가 포함된 `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) 콜백을 수신합니다.
3. 메시지 수신을 중지하려면 `removeAdvancedMsgListener` 를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.

예시 코드는 다음과 같습니다.


```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) {
      // 사용자 정의 메시지 사용
      if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_CUSTOM){
        String data = message.customElem.data;
        String desc = message.customElem.desc;
        String ext = message.customElem.extension;
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



## 리치 미디어 메시지 수신
수신자는 다음 단계에서 고급 메시지 리스너를 **통해서만** 리치 미디어 메시지를 수신할 수 있습니다.
1. `addAdvancedMsgListener` API를 호출하여 고급 메시지 리스너를 설정합니다.
2. `onRecvNewMessage` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Callback/OnRecvNewMessageCallback.html)) 콜백을 수신하여 V2TimMessage 메시지를 가져옵니다.
3. V2TIMMessage 메시지에서 elemType 속성을 구문 분석한 다음 유형에 따라 메시지를 다시 구문 분석하여 메시지 Elem의 특정 콘텐츠를 가져옵니다.
4. 메시지 수신을 중지하려면 `removeAdvancedMsgListener`를 호출하여 리스너를 제거하십시오. 이 단계는 선택 사항이며 필요에 따라 수행할 수 있습니다.




### 이미지 메시지

이미지 메시지의 이미지는 원본, 대형 및 썸네일의 세 가지 형식이 될 수 있습니다. 후자의 두 개는 메시지 전송 중에 SDK에 의해 자동으로 생성되며 무시할 수 있습니다.
대형 이미지: 원본 이미지를 비례 압축하여 얻은 이미지입니다. 압축 후 높이와 너비 중 짧은 쪽이 720픽셀이 됩니다.
썸네일: 원본 이미지를 비례 압축하여 얻은 이미지입니다. 압축 후 높이와 너비 중 짧은 쪽이 198픽셀이 됩니다.

Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

다음 예시 코드는 V2TimMessage에서 이미지 콘텐츠를 구문 분석하는 방법을 보여줍니다.



```dart
V2TimAdvancedMsgListener listener = V2TimAdvancedMsgListener(
    onRecvC2CReadReceipt: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageModified: (V2TimMessage message) {},
    onRecvMessageReadReceipts: (List<V2TimMessageReceipt> receiptList) {},
    onRecvMessageRevoked: (String messageid) {},
    onRecvNewMessage: (V2TimMessage message) async {
      // 이미지 메시지 사용
      if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_IMAGE) {
        String path = message
            .imageElem.path; // 이미지 업로드 경로. 이 필드는 경험을 최적화하기 위해 미리 화면에 이미지를 표시하는 데 사용할 수 있는 메시지 발신자에게만 적용됩니다.
        for (var item in message.imageElem.imageList) { // 대형 이미지, 원본 이미지 및 썸네일 트래버스
          // 이미지 속성 구문 분석
          int height = item.height;
          String localUrl = item.localUrl;
          int size = item.size;
          int type = item.type; // 대형 이미지, 썸네일, 원본 이미지
          String url = item.url;
          String uuid = item.uuid;
          int width = item.width;
        }
      }
      // 멀티미디어 메시지 URL 가져오기
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // 메시지 id
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // 가져오기 성공
      }

      // 멀티미디어 메시지 다운로드
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // 메시지 id
              messageType: 3, // 메시지 유형
              imageType: 0, // 이미지 유형, messageType이 이미지 메시지인 경우에만 유효
              isSnapshot: false // 썸네일 여부, messageType이 비디오 메시지인 경우에만 유효
              );
      if (downloadMessageRes.code == 0) {
        // 다운로드 성공
      }
    },
    onSendMessageProgress: (V2TimMessage message, int progress) {},
  );
  TencentImSDKPlugin.v2TIMManager
      .getMessageManager()
      .addAdvancedMsgListener(listener: listener);
```



### 비디오 메시지

비디오 메시지를 받은 후 채팅 페이지에 비디오 미리보기가 표시되고 사용자가 메시지를 클릭하면 비디오가 재생됩니다.

Flutter SDK는 무료일 때 비디오 및 썸네일을 다운로드하여 직접 사용할 수 있으며 App이 제거되면 지워집니다. 다음 예시 코드는 V2TimMessage에서 비디오 콘텐츠를 구문 분석하는 방법을 보여줍니다.

Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.


```dart
     if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_VIDEO){
  			// 썸네일, 재생 주소, 너비와 높이, 크기와 같은 비디오 메시지 속성을 구문 분석합니다.
        message.videoElem.UUID;
        message.videoElem.duration;
        message.videoElem.localSnapshotUrl;
        message.videoElem.localVideoUrl;
        message.videoElem.snapshotHeight;
        message.videoElem.snapshotPath;
        // ...
      }

      // 멀티미디어 메시지 URL 가져오기
      V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
          await TencentImSDKPlugin.v2TIMManager
              .getMessageManager()
              .getMessageOnlineUrl(
                msgID: '', // 메시지 id
              );
      if (getMessageOnlineUrlRes.code == 0) {
        // 가져오기 성공
      }

      // 멀티미디어 메시지 다운로드
      V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .downloadMessage(
              msgID: '', // 메시지 id
              messageType: 5, // 메시지 유형
              imageType: 0, // 이미지 유형, messageType이 이미지 메시지인 경우에만 유효
              isSnapshot: false // 썸네일 여부, messageType이 비디오 메시지인 경우에만 유효
              );
      if (downloadMessageRes.code == 0) {
        // 다운로드 성공
      }
```


### 음성 메시지

Flutter SDK는 무료일 때 음성 메시지를 다운로드하여 직접 사용할 수 있으며 App이 제거되면 지워집니다. 다음 예시 코드는 V2TimMessage에서 비디오 콘텐츠를 구문 분석하는 방법을 보여줍니다.

Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

```dart
    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_SOUND){
  			// 오디오 메시지의 재생 주소, 로컬 주소, 크기 및 지속 시간을 구문 분석합니다.
        message.soundElem.UUID;
        message.soundElem.dataSize;
        message.soundElem.duration;
        message.soundElem.localUrl;
        message.soundElem.url;
        // ...
        // 멀티미디어 메시지 URL 가져오기
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // 메시지 id
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // 가져오기 성공
        }

        // 멀티미디어 메시지 다운로드
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // 메시지 id
                messageType: 4, // 메시지 유형
                imageType: 0, // 이미지 유형, messageType이 이미지 메시지인 경우에만 유효
                isSnapshot: false // 썸네일 여부, messageType이 비디오 메시지인 경우에만 유효
                );
        if (downloadMessageRes.code == 0) {
          // 다운로드 성공
        }
    }
```


### 파일 메시지

Flutter SDK는 무료일 때 파일 메시지를 다운로드하여 직접 사용할 수 있으며 App이 제거되면 지워집니다. 다음 예시 코드는 V2TimMessage에서 비디오 콘텐츠를 구문 분석하는 방법을 보여줍니다.

Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 메시지 목록을 가져올 때 메시지의 url을 반환하지 않으며 getMessageOnlineUrl([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/getMessageOnlineUrl.html))을 통해 가져와야 합니다.
Flutter SDK 5.0.4 이후 버전에서 리치 미디어 메시지는 기본적으로 localurl을 반환하지 않으며 downloadMessage([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Api/V2TIMMessageManager/downloadMessage.html))를 통해 메시지가 성공적으로 다운로드된 후에만 반환됩니다.

```dart

    if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FILE){
  			// 파일 메시지의 파일 이름, 크기, URL 및 기타 정보를 구문 분석합니다
        message.fileElem.UUID;
        message.fileElem.fileName;
        message.fileElem.fileSize;
        message.fileElem.localUrl;
        message.fileElem.path;
        message.fileElem.url;
        // 멀티미디어 메시지 URL 가져오기
        V2TimValueCallback<V2TimMessageOnlineUrl> getMessageOnlineUrlRes =
            await TencentImSDKPlugin.v2TIMManager
                .getMessageManager()
                .getMessageOnlineUrl(
                  msgID: '', // 메시지 id
                );
        if (getMessageOnlineUrlRes.code == 0) {
          // 가져오기 성공
        }

        // 멀티미디어 메시지 다운로드
        V2TimCallback downloadMessageRes = await TencentImSDKPlugin.v2TIMManager
            .getMessageManager()
            .downloadMessage(
                msgID: '', // 메시지 id
                messageType: 6, // 메시지 유형
                imageType: 0, // 이미지 유형, messageType이 이미지 메시지인 경우에만 유효
                isSnapshot: false // 썸네일 여부, messageType이 비디오 메시지인 경우에만 유효
                );
        if (downloadMessageRes.code == 0) {
          // 다운로드 성공
        }
    }
```


### 지리적 위치 메시지

지리적 위치 메시지를 수신한 후 수신기는 `locationElem`에서 직접 위도 및 경도 정보를 구문 분석할 수 있습니다.
다음 샘플 코드는 V2TimMessage에서 지리적 위치 콘텐츠를 구문 분석하는 방법을 보여줍니다.



```dart

if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_LOCATION){
  			// 위도, 경도, 설명과 같은 지리적 위치 정보를 구문 분석합니다
        message.locationElem.desc;
        message.locationElem.latitude;
        message.locationElem.longitude;
}
```


### 이모티콘 메시지

SDK는 그림 이모티콘 메시지에 대해서만 패스스루 채널을 제공합니다. 메시지 콘텐츠 필드에 대해서는 `faceElem` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Message/V2TimFaceElem.html))의 정의를 참고하십시오. 여기에서 `index`와 `data`를 사용자 정의할 수 있습니다.

예를 들어 발신자는 index = 1, data = "x12345"로 설정하여 ‘스마일’ 이모티콘을 나타낼 수 있습니다.
수신자는 수신한 이모지 메시지를 1과 "x12345"로 구문 분석하여 미리 설정된 규칙에 따라 ‘스마일’ 이모티콘으로 표시합니다.

다음 예시 코드는 V2TIMMessage에서 이모티콘 콘텐츠를 구문 분석하는 방법을 보여줍니다.


```dart
if (message.elemType == MessageElemType.V2TIM_ELEM_TYPE_FACE) {
        message.faceElem.data;
        message.faceElem.index;
}
```


### 그룹 tips 메시지

그룹 tips 메시지는 ‘관리자가 그룹 채팅에서 alice를 제거했습니다’ 및 ‘bob이 그룹 이름을 xxxx로 변경했습니다’와 같이 그룹 채팅에서 일반 메시지 외에 사용자가 받는 팁입니다.

> ? 그룹 tips 메시지는 그룹 구성원에게만 수신되며 일대일 채팅 측에는 수신되지 않습니다.

그룹 tips 메시지에는 여러 유형이 있습니다. 자세한 내용은 `V2TIMGroupTipsType` ([상세 보기](https://comm.qq.com/im/doc/flutter/zh/SDKAPI/Class/Group/V2TimGroupTipsElem.html))의 정의를 참고하십시오.

그룹 tips 메시지를 받은 후 수신자는 일반적으로 다음을 수행해야 합니다.
1.`V2TIMGroupTipsElem`의 각 필드를 구문 분석합니다
2. type에 따라 tips 메시지 유형을 식별합니다
3. 유형에 따라 표시할 콘텐츠에 다른 필드를 병합합니다.

예를 들면:
수신자는 type = `V2TIM_GROUP_TIPS_TYPE_GROUP_INFO_CHANGE`로 구문 분석하여 이것이 그룹 프로필 변경 알림임을 나타냅니다.
수신자는 `opMember`에서 운영자 정보를, `groupChangeInfoList`에서 수정된 그룹 이름을 가져올 수 있습니다.
이 시점에서 수신자는 ‘운영자’와 ‘수정된 그룹 이름’을 병합하여 ‘alice가 그룹 이름을 group123으로 이름을 바꿨습니다’와 같은 그룹 팁을 만들 수 있습니다.

다음 예시 코드는 V2TIMMessage에서 tips 콘텐츠를 구문 분석하는 방법을 보여줍니다.



```dart
if(message.elemType == MessageElemType.V2TIM_ELEM_TYPE_GROUP_TIPS){
        message.groupTipsElem.groupID; // 그룹
        message.groupTipsElem.type; // 그룹 Tips 유형
        message.groupTipsElem.opMember; // 운영자 프로필
        message.groupTipsElem.memberList; // 운용 중인 사용자 프로필
        message.groupTipsElem.groupChangeInfoList; // 그룹 정보 변경 내역
        message.groupTipsElem.memberChangeInfoList; // 그룹 구성원 변경 정보
        message.groupTipsElem.memberCount; // 현재 온라인 그룹 구성원 수
}
```


## 여러 Elem이 포함된 메시지 수신

1. Message 객체를 사용하여 첫 번째 Elem 객체를 구문 분석합니다.
2. 첫 번째 Elem 객체의 nextElem 메소드를 통해 다음 Elem 객체를 가져옵니다. 다음 객체가 있으면 Elem 객체 인스턴스가 반환됩니다. 그렇지 않으면 null이 반환됩니다.

예시 코드는 다음과 같습니다.


```dart
if(message.textElem.nextElem!=null){
   // 다음 메시지가 있습니다.
}
```

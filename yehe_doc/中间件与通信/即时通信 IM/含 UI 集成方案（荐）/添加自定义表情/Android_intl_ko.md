TUIChat은 사용자 지정 이모티콘 추가를 지원합니다.

## 사용자 지정 이모티콘 추가
TUIChat은 샌드박스, assets 디렉터리 및 네트워크 경로에서 사용자 지정 이모티콘 경로를 지원합니다.
assets 디렉터리에 programmer 이모티콘을 추가하는 것을 예로 들어 보겠습니다.

### 이모티콘 패키지 리소스 준비

App의 src/main 폴더 아래에 assets 폴더를 생성하고 App의 assets 디렉터리 아래에 이모티콘 폴더를 배치합니다.

<img src="https://im.sdk.qcloud.com/tools/resource/custom_face/android/custom_face_programmer.png" width="300px" />

### 이모티콘 패키지 추가

애플리케이션 실행 시 API를 호출하여 FaceManager에 사용자 지정 이모티콘을 추가합니다.
각 이모티콘 패키지에는 고유한 faceGroupID가 있으며 이모티콘 패키지의 각 이모티콘은 faceKey에 해당합니다. 이모티콘이 FaceManager에 추가되면 ‘이모티콘 더보기’ 입력 인터페이스가 faceGroupID의 크기에 따라 정렬되어 표시됩니다.

```java
public class DemoApplication extends Application {
    @Override
    public void onCreate() {
        FaceGroup programmerGroup = new FaceGroup();
        // 더 많은 이모티콘 입력 인터페이스 줄당 표시 개수
        programmerGroup.setPageColumnCount(5);
        // 더 많은 이모티콘 입력 인터페이스 이모티콘 행 수
        programmerGroup.setPageRowCount(2);
        // 이모티콘 패키지 썸네일
        programmerGroup.setFaceGroupIconUrl("file:///android_asset/programmer/programmer00@2x.png");
        // 이모티콘 패키지 이름
        programmerGroup.setGroupName("programmer");
        for (int i = 0; i < 16; i++) {
            CustomFace customFace = new CustomFace();
            String index = "" + i;
            if (i < 10) {
                index = "0" + i;
            }
            // assets에서 이모티콘의 경로를 설정하고,경로가 샌드박스 경로 또는 네트워크 경로인 경우 setFaceUrl 메소드를 사용할 수 있습니다.
            customFace.setAssetPath("programmer/programmer" + index + "@2x.png");
            // 이모티콘의 식별(key)
            String faceKey = "programmer" + index;
            customFace.setFaceKey(faceKey);
            // 이모티콘 더보기 입력 인터페이스 이모티콘 표시 너비
            customFace.setWidth(170);
            // 더 많은 이모티콘 입력 인터페이스 이모티콘 표시 높이
            customFace.setHeight(170);
            programmerGroup.addFace(faceKey, customFace);
        }
        // FaceManager에 이모티콘 패키지 등록, FaceGroupID는 1
        FaceManager.addFaceGroup(1, programmerGroup);
    }
}
```

### 추가 완료 효과

추가가 완료되면 채팅 인터페이스 ‘더 많은 이모티콘’ 입력 인터페이스를 열어 새로 추가된 이모티콘 패키지를 확인합니다.

<img src="https://im.sdk.qcloud.com/tools/resource/custom_face/android/custom_programmer_face_input.png" width="720px" />

>! faceGroupID는 0보다 큰 정수이며 중복될 수 없습니다.


## 사용자 지정 이모티콘 보내기
사용자 지정 이모티콘을 추가한 후 채팅의 ‘이모티콘 더 보기’ 입력 인터페이스에서 추가된 이모티콘을 볼 수 있으며 이모티콘을 클릭하여 보낼 수 있습니다.


코드를 사용하여 이모티콘 메시지를 생성한 다음 보낼 수도 있습니다. 예를 들면 다음과 같습니다.
```java
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager()
        .createFaceMessage(faceGroupID, faceKey.getBytes());
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage,
        userID,
        null,
        V2TIMMessage.V2TIM_PRIORITY_DEFAULT,
        false,
        null,
        new V2TIMSendCallback<V2TIMMessage>() {...}
```

## 사용자 지정 이모티콘 구문 분석
사용자 지정 이모티콘 메시지를 수신한 후 TUIKit은 IMSDK의 V2TIMMessage를 FaceMessageBean 유형으로 구문 분석하고 사용자 지정 이모티콘의 faceGroupID 및 faceKey는 FaceMessageBean에서 가져올 수 있습니다.
```java
TUIMessageBean messageBean = ChatMessageParser.parseMessage(v2TIMMessage);
FaceMessageBean faceMessageBean = null;
if (messageBean instanceof FaceMessageBean) {
    faceMessageBean = (FaceMessageBean) messageBean;
}
if (faceMessageBean != null) {
    int faceGroupID = faceMessageBean.getIndex();
    String faceKey = null;
    if (faceMessageBean.getData() != null) {
        faceKey = new String(faceMessageBean.getData());
    }
}
```


## 사용자 지정 이모티콘 렌더링

### 기존 API 렌더링 호출

사용자 지정 이모티콘의 faceGroupID 및 faceKey를 가져온 후 FaceManager의 loadFace 메소드를 호출하여 전달한 imageView에 직접 로딩할 수 있습니다.
```java
FaceManager.loadFace(faceGroupID, faceKey, imageView);
```

### 사용자 지정 렌더링

이모티콘의 faceGroupID 및 faceKey를 통해 FaceManager에서 이모티콘의 실제 URL을 가져올 수도 있습니다. 그 다음 가져온 URL을 통해 렌더링을 사용자 지정합니다. 예를 들면 다음과 같습니다.
```java
String faceUrl = "";
List<FaceGroup> faceGroupList = FaceManager.getFaceGroupList();
for(FaceGroup faceGroup : faceGroupList) {
    if (faceGroup.getGroupID() == faceGroupID) {
        ChatFace face = faceGroup.getFace(faceKey);
        if (face != null) {
            faceUrl = face.getFaceUrl();
        }
    }
}

// load faceUrl into view
```

### 렌더링 효과

렌더링 효과는 다음 이미지와 같습니다.

<img src="https://im.sdk.qcloud.com/tools/resource/custom_face/android/custom_programmer_face_render.png" width="320px" />


[](id:feedback)

## 소개

Android Player+ SDK는 Tencent Cloud가 오픈 소스로 제공하는 플레이어 구성 요소로 코드 몇 줄만으로 가로세로 전환, 해상도 선택, 제스처 및 작은 창 등의 기본 기능뿐 아니라 비디오 캐시, 소프트웨어/하드웨어 디코딩 전환 및 배속 재생 등 특수 기능을 포함한 Tencent 비디오와 유사한 강력한 재생 기능을 제공합니다. 시스템 플레이어에 비해 더욱 다양한 포맷을 지원하며 호환성이 뛰어나고 기능이 우수합니다. 또한 첫 화면 바로 재생이 가능하고, 딜레이가 짧은 장점을 가지고 있으며, 비디오 썸네일 등의 고급 기능도 탑재되어 있습니다.

## SDK 다운로드

VOD Android Player+의 프로젝트 주소는 [SuperPlayer_Android](https://github.com/tencentyun/SuperPlayer_Android)입니다.

## 열람 대상

본 문서의 일부 내용은 Tencent Cloud의 독점적 기능이므로, 사용하기 전에 [Tencent Cloud](https://intl.cloud.tencent.com/zh/) 관련 서비스를 활성화해 주십시오. 미등록 사용자는 [무료 베타](https://intl.cloud.tencent.com/login) 계정에 가입하실 수 있습니다.

## 빠른 통합
### aar 통합
1. SDK + Demo 개발 패키지를 다운로드합니다. 프로젝트 주소는 [Android](https://github.com/tencentyun/SuperPlayer_Android)입니다.
2. `SDK/LiteAVSDK_XXX.aar`와 `Demo/superplayerkit` module을 가져와 프로젝트에 복사합니다.
3. `App/build.gradle`에 종속성을 추가합니다.
<dx-codeblock>
::: java java
compile(name: 'LiteAVSDK_Player_7.4.9211', ext: 'aar')
compile project(':superplayerkit')
// Player+ 댓글 자막 통합을 위한 3rd party 라이브러리
compile 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
:::
</dx-codeblock>
4. 프로젝트 `build.gradle`에 다음을 추가합니다.
<dx-codeblock>
::: java java
...
allprojects {
    repositories {
        flatDir {
            dirs 'libs'
        }
        ...
    }
}
...
:::
</dx-codeblock>
5. 권한 성명.
```java
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD 플레이어 플로팅 윈도우 권한-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--저장-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

### 플레이어 사용

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 비디오를 즉시 재생할 수 있습니다.
```java
//링크 도용 방지 비활성화
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileId 설정
mSuperPlayerView.playWithModel(model);

//링크 도용 방지를 활성화하려면 Player+의 서명인 psign을 입력해야 합니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/266/42436
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // FileId 설정
mSuperPlayerView.playWithModel(model);
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
mSuperPlayerView.playWithModel(model);
```



코드를 실행하면 비디오가 휴대폰에서 재생되며, 인터페이스 대부분의 기능을 사용할 수 있음을 확인할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/128c45edfc77b319475868c21caec2de.png" width="550">

### FileId 선택

비디오 FileId는 일반적으로 비디오 업로드 후 서버에서 반환됩니다.

1. 클라이언트에서 비디오 배포 후 서버가 FileId를 클라이언트로 반환합니다.
2. 서버에서 비디오 업로드 시, 해당 FileId가 [업로드 확인](https://intl.cloud.tencent.com/zh/document/product/266) 공지에 포함됩니다.

Tencent Cloud에 이미 파일이 존재하는 경우에는 [미디어 자원 관리](https://console.cloud.tencent.com/vod/media)에서 해당 파일을 찾아 FileId를 조회할 수 있습니다. 아래 이미지와 같이 ID는 FileId를 나타냅니다.
![](https://main.qcloudimg.com/raw/1a3677d5fe618227a117d7502be42793.png)



### 타임스탬프 기능

길이가 긴 비디오 재생 시 타임스탬프를 통해 시청자의 관심 지점을 쉽게 찾을 수 있습니다. [미디어 파일 속성 변경](https://intl.cloud.tencent.com/document/product/266/37570) API를 사용하여 AddKeyFrameDescs.N 매개변수를 통해 비디오에 타임스탬프를 설정할 수 있습니다.

호출 후 플레이어 인터페이스에 새로운 요소가 추가됩니다.
<img src="https://main.qcloudimg.com/raw/55ebce6d0c703dafa1ac131e1852e025.png" width="550">


### 작은 창 재생
작은 창 재생을 통해 모든 Activity 위에 플로팅하여 재생할 수 있습니다. 작은 창 재생은 재생 시작 전에 다음 코드를 호출하기만 하면 쉽게 구현이 가능합니다.

```java
// 플레이어 설정
SuperPlayerGlobalConfig prefs = SuperPlayerGlobalConfig.getInstance();
// 플로팅 윈도우 재생 활성화
prefs.enableFloatWindow = true;
//플로팅 윈도우의 초기 위치와 너비 및 높이 설정
SuperPlayerGlobalConfig.TXRect rect = new SuperPlayerGlobalConfig.TXRect();
rect.x = 0;
rect.y = 0;
rect.width = 810;
rect.height = 540;
// ...기타 설정
```

<img src="https://main.qcloudimg.com/raw/2cab897e43e4a01ee5f8e48372ce79a3.jpg" width="350">

### 재생 종료

플레이어가 필요하지 않은 경우 `resetPlayer`을 호출하여 플레이어 내부를 정리하고 메모리를 확보합니다.

```java
mSuperPlayerView.resetPlayer();
```

## 추가 기능

전체 기능을 사용하려면 비디오 클라우드 툴 킷을 다운로드하거나 프로젝트 데모를 직접 실행하십시오.
<img src="https://main.qcloudimg.com/raw/344d9d41fc5e305a17e22e104b9305da.png" width="150">



## 제품 개요

Android용 Tencent Cloud RT-Cube Superplayer는 Tencent Cloud의 오픈 소스 플레이어 컴포넌트입니다. 품질 모니터링, 비디오 암호화, TESHD, 해상도 선택 및 작은 창 재생을 통합하여 모든 VOD 및 라이브 재생 시나리오에 적합합니다. 전체 기능을 캡슐화하고 상위 계층 UI를 제공하여 인기 있는 비디오 앱에 필적하는 재생 프로그램을 빠르게 만들 수 있도록 도와줍니다.

## 버전 지원

본 문서에서 설명된 기능에 대한 Tencent Cloud RT-Cube 지원 현황은 다음과 같습니다.

| 버전                            | Smart                                               | Live                                                | UGSV                                                  | TRTC                                             | Player                                                | 모든 기능                                                       |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 지원                            | -                                                            | -                                                            | -                                                            | -                                                           | &#10003;                                                     | &#10003;                                                     |
| SDK 다운로드 <div style="width: 90px"/> | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=video) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=player) | [다운로드](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |


## 프로젝트 주소[](id:sdkDownload)

Android용 Tencent Cloud RT-Cube Superplayer의 프로젝트 주소는 [SuperPlayer_Android](https://github.com/tencentyun/SuperPlayer_Android)입니다.

## 타겟 오디언스

본 문서의 일부 내용은 Tencent Cloud의 독점적 기능이므로, 사용하기 전에 [Tencent Cloud](https://intl.cloud.tencent.com) 관련 서비스를 활성화해 주십시오. 미등록 사용자는 [무료 베타](https://intl.cloud.tencent.com/login) 계정에 가입하실 수 있습니다.

## 통합 가이드[](id:guide)
Gradle 자동 로딩 방식을 사용하거나 수동으로 aar을 다운로드한 후, 귀하의 현재 프로그래밍 프로젝트에 가져옵니다.

### 방법1: 자동 로딩(AAR)

1. SDK + Demo 개발 패키지를 다운로드합니다. 프로젝트 주소는 [Android](https://github.com/tencentyun/SuperPlayer_Android)입니다.
2. `Demo/superplayerkit` module을 프로젝트에 복사하고 다음과 같이 구성합니다.
   - `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
   ```xml
   include ':superplayerkit'
   ```
   - `superplayerkit` 프로젝트의 build.gradle 파일을 열고 compileSdkVersion, buildToolsVersion, minSdkVersion, targetSdkVersion 및 rootProject.ext.liteavSdk의 상수 값을 수정합니다.
![](https://main.qcloudimg.com/raw/fd6bc41bfd8b80fe5e82e3345b6ce73f.png)
   ```xmls
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies{
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
   }
   ```
3. gradle에서 mavenCentral 라이브러리를 구성하면 LiteAVSDK를 자동으로 다운로드되고 업데이트됩니다. `app/build.gradle`을 열고 다음과 같이 구성합니다.
![](https://main.qcloudimg.com/raw/65439d399ec584871a7a9bc88ccaef46.png)
   - dependencies에 LiteAVSDK_Player의 종속성을 추가합니다.
   ```xml
   dependencies{
       implementation 'com.tencent.liteav:LiteAVSDK_Player:latest.release'
       implementation project(':superplayerkit')
       // Superplayer 댓글 자막 통합을 위한 3rd party 라이브러리
       implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
   }
   ```
   -  `app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 필요에 따라 구성할 수 있는 armeabi, armeabi-v7a 및 arm64-v8a를 지원합니다).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
   - 프로젝트 디렉터리의 build.gradle에 mavenCentral 라이브러리를 추가합니다.
   ```
   repositories {
       mavenCentral()
   }
   ```

4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) Sync Now를 클릭하여 SDK를 동기화합니다. mavenCentral에 연결할 수 있으면 SDK가 자동으로 다운로드되어 곧 프로젝트에 통합됩니다.

### 방법2: 수동 다운로드(AAR)
1. SDK + Demo 개발 패키지를 다운로드합니다. 프로젝트 주소는 [Android](https://github.com/tencentyun/SuperPlayer_Android)입니다.
2. `SDK/LiteAVSDK_Player_XXX.aar`(XXX는 버전 번호)를 app 아래의 libs 폴더로 가져오고 `Demo/superplayerkit` module을 프로젝트에 복사합니다.
3. `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
   ```
   include ':superplayerkit'
   ```
4. `superplayerkit` 프로젝트의 build.gradle 파일을 열고 compileSdkVersion, buildToolsVersion, minSdkVersion, targetSdkVersion 및 rootProject.ext.liteavSdk의 상수 값을 수정합니다.
![](https://main.qcloudimg.com/raw/479cb6ed7a29621998d1ee670e091437.png)
   ```xml
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   
   dependencies{
       implementation(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
   }
   ```
   - repositories 구성
   ```xml
   repositories {
       flatDir {
           dirs '../app/libs'
       }
   }
   ```
5. `app/build.gradle`에 종속성을 추가합니다.
   ```xml
   compile(name:'LiteAVSDK_Player_8.9.10349', ext:'aar')
   implementation project(':superplayerkit')
   // Superplayer 댓글 자막 통합을 위한 3rd party 라이브러리
   implementation 'com.github.ctiao:DanmakuFlameMaster:0.5.3'
   ```
6. 프로젝트 `build.gradle`에 다음을 추가합니다.
   ```xml
   allprojects {
       repositories {
           flatDir {
               dirs 'libs'
           }
       }
   }
   ```
7. `app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
8. Sync Now를 클릭하여 SDK를 동기화합니다.

### 방법3: SDK 통합(jar + so)
aar 라이브러리를 통합하지 않으려면 jar 및 so 라이브러리를 가져와서 LiteAVSDK를 통합하도록 선택할 수 있습니다.
[](id:smallStep_1)
1. 여기에서 [Android](https://github.com/tencentyun/SuperPlayer_Android)용 SDK + Demo 개발 키트를 다운로드하고 압축을 풉니다. SDK 디렉터리에서 SDK/LiteAVSDK_Player_XXX.zip(XXX는 버전 번호)을 찾습니다. 압축 해제 후 아래와 같이 jar 파일과 so 폴더가 포함된 libs 디렉터리를 얻을 수 있습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9ac0f5b1b9b5d15a005fa2226dd960b6.png)
2. `Demo/superplayerkit` module을 프로젝트에 복사하고 `superplayerkit`을 프로젝트 디렉터리의 setting.gradle로 가져옵니다.
   ```xml
   include ':superplayerkit'
   ```
3. [1단계](#smallStep_1)에서 압축 해제하여 얻은 libs 폴더를 `superplayerkit` 프로젝트 루트 디렉터리에 복사합니다.
4. `superplayerkit/build.gradle` 파일을 수정합니다.
![](https://main.qcloudimg.com/raw/ed66e7d887bc5c28c2eff45807037c23.png)
   ```xml
   compileSdkVersion 26
   buildToolsVersion "26.0.2"
   
   defaultConfig {
       targetSdkVersion 23
       minSdkVersion 19
   }
   ```
   - sourceSets를 구성하고 so 라이브러리 가져오기 코드를 추가합니다.
   ```xml
   sourceSets{
         main{
             jniLibs.srcDirs = [’libs’]
         }
     }
   ```
   - repositories를 구성하고 flatDir을 추가하고 로컬 리포지토리의 경로를 지정합니다.
   ```xml
   repositories {
       flatDir {
           dirs 'libs'
       }
   }
   ```
5. ` app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
   ```xmsl
   ndk {
       abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
   }
   ```
6. Sync Now를 클릭하여 SDK를 동기화합니다.

### App 권한 설정

AndroidManifest.xml에서 App 권한을 구성합니다. LiteAVSDK에는 다음 권한이 필요합니다.

```java
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD 플레이어 플로팅 창 권한-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--저장-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## 재생 기능 사용

### 플레이어 사용[](id:usePlayer)

플레이어의 메인 클래스는 `SuperPlayerView`로, 생성 후 비디오를 즉시 재생할 수 있습니다.
```java
//링크 도용 방지 비활성화
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileId 설정
mSuperPlayerView.playWithModel(model);

//링크 도용 방지를 활성화하려면 Superplayer의 서명인 psign을 입력해야 합니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참조하십시오. https://intl.cloud.tencent.com/document/product/266/38099
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329071;// AppId 설정
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710173650"; // FileId 설정
mSuperPlayerView.playWithModel(model);
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
mSuperPlayerView.playWithModel(model);
```



코드를 실행하면 비디오가 휴대폰에서 재생되며, 인터페이스 대부분의 기능을 사용할 수 있음을 확인할 수 있습니다.


### FileId 선택[](id:FileId)

비디오 FileId는 일반적으로 비디오 업로드 후 서버에서 반환됩니다.

1. 클라이언트에서 비디오 배포 후 서버가 FileId를 클라이언트로 반환합니다.
2. 비디오가 서버에 업로드되면 해당 FileId가 업로드 확인 알림에 포함됩니다.

Tencent Cloud에 이미 파일이 존재하는 경우에는 [미디어 자산 관리](https://console.cloud.tencent.com/vod/media)에서 해당 파일을 찾아 FileId를 조회할 수 있습니다.

### 타임스탬프 기능

길이가 긴 비디오 재생 시 타임스탬프를 통해 시청자의 관심 지점을 쉽게 찾을 수 있습니다. [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API를 사용하여 AddKeyFrameDescs.N 매개변수를 통해 비디오에 타임스탬프를 설정할 수 있습니다.

호출 후 플레이어 인터페이스에 새로운 요소가 추가됩니다.



### 작은 창 재생[](id:smallWindow)
작은 창 재생을 통해 모든 Activity 위에 플로팅하여 재생할 수 있습니다. 작은 창 재생은 재생 시작 전에 다음 코드를 호출하기만 하면 쉽게 구현이 가능합니다.

```java
// 플레이어 설정
SuperPlayerGlobalConfig prefs = SuperPlayerGlobalConfig.getInstance();
// 플로팅 창 재생 활성화
prefs.enableFloatWindow = true;
//플로팅 창의 초기 위치와 너비 및 높이 설정
SuperPlayerGlobalConfig.TXRect rect = new SuperPlayerGlobalConfig.TXRect();
rect.x = 0;
rect.y = 0;
rect.width = 810;
rect.height = 540;
// ...기타 설정
```

<img src="https://main.qcloudimg.com/raw/2cab897e43e4a01ee5f8e48372ce79a3.jpg" width="350">

### 재생 종료[](id:exitPlayer)

플레이어가 필요하지 않은 경우 `resetPlayer`을 호출하여 플레이어 내부를 정리하고 메모리를 확보합니다.

```java
mSuperPlayerView.resetPlayer();
```

## 더 많은 기능[](id:moreFeature)

전체 기능을 사용하려면 비디오 클라우드 툴 킷을 다운로드하거나 프로젝트 Demo를 직접 실행하십시오.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">

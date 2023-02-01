## 환경 준비

- Flutter 2.0 또는 이후 버전.
- Android 개발:
  - Android Studio 3.5 이상 버전
  - Android 4.1 이상 버전의 디바이스
- iOS 개발:
  - Xcode 11.0 이상 버전.
  - OSX 시스템 10.11 이상 버전.
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## SDK 다운로드

Flutter용 Tencent Cloud RT-Cube 플레이어 SDK는 [Player Flutter](https://github.com/LiteAVSDK/Player_Flutter)에서 다운로드할 수 있습니다.

## 빠른 통합

### 프로젝트의 pubspec.yaml에 다음 종속성 추가

필요에 따라 LiteAVSDK Player 또는 LiteAVSDK_Professional을 통합할 수 있습니다.

1. 최신 버전의 LiteAVSDK_Player(기본적으로 통합됨)를 통합하고 `pubspec.yaml`에 다음 구성을 추가합니다:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
```
최신 버전의 LiteAVSDK_Professional을 통합하려면 다음과 같이 `pubspec.yaml`의 구성을 변경하십시오.
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: Professional
```
지정된 버전의 플레이어 SDK를 통합하려면 다음과 같이 ref가 의존하는 tag를 통해 해당 버전을 지정하십시오.
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: release_player_v1.0.6 

# release_player_v1.0.6은 Android용 TXLiteAVSDK_Player_10.6.0.11182 또는 iOS용 TXLiteAVSDK_Player_10.6.11821 통합을 나타냅니다.
```

더 많은 보관된 tag는 [release 목록](https://github.com/LiteAVSDK/Player_Flutter/releases)을 참고하십시오.

2. 통합 후 코드 편집기와 함께 제공되는 UI를 통해 또는 다음 명령을 직접 실행하여 Flutter 종속성을 얻을 수 있습니다.

```yaml
flutter packages get
```

3. 사용 중에 다음 명령을 실행하여 기존 Flutter 종속 항목을 업데이트할 수 있습니다.

```dart
flutter pub upgrade
```

### 기본 구성 추가

#### Android 구성
1. `AndroidManifest.xml`에 다음 구성을 추가합니다.
```xml
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--스토리지-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

2. Android 디렉터리의 `build.gradle`이 mavenCenter를 사용하고 종속성을 성공적으로 다운로드할 수 있는지 확인하십시오.
```groovy
repositories {
  mavenCentral()
}
```

3. 네이티브 SDK의 종속성 버전을 업데이트하려면 Android 디렉터리에서 `build` 폴더를 수동으로 삭제하거나 다음 명령을 실행하여 강제로 새로 고칩니다.
```shell
./gradlew build
```

4. Android의 PIP(picture-in-picture) 기능을 사용하려면 example 컴포넌트의 android 디렉터리에 `FTXFlutterPipActivity.java`를 통합합니다.


#### iOS 구성

참고: **iOS는 현재 시뮬레이터에서 프로젝트 실행 및 디버깅을 지원하지 않습니다. 따라서 실제 장치에서 프로젝트를 개발하고 디버그하는 것이 좋습니다**.

1. iOS의 `Info.plist` 파일에 다음 구성을 추가합니다.
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```
2. iOS는 기본적으로 종속성을 위해 `pod`를 사용합니다. `podfile` 파일을 편집하고 플레이어 SDK 버전을 지정하십시오. TXLiteAVSDK_Player는 기본적으로 통합되어 있습니다.
```xml
pod 'TXLiteAVSDK_Player'        //Player 버전
```
 LiteAVSDK_Professional 통합:
```
pod 'TXLiteAVSDK_Professional' //Professional 버전
```

에디션을 지정하지 않으면 `TXLiteAVSDK_Player`의 최신 버전이 설치됩니다.

3. 새 버전 출시와 같은 일부 경우 iOS 디렉터리에서 다음 명령을 실행하여 iOS 플레이어 종속성을 강제로 업데이트해야 합니다.
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

## 비디오 재생 License 통합
이미 관련 License 권한을 획득한 경우, [Tencent Cloud RT-Cube 콘솔](https://www.tencentcloud.com/account/login)에서 License URL과 License Key를 확인할 수 있습니다.

아직 필요한 License가 없다면 먼저 [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098)의 안내에 따라 License를 받을 수 있습니다.

플레이어를 통합하기 전에 [Sign up for a Tencent Cloud account](https://www.tencentcloud.com/en/account/register)하고, 비디오 재생 License를 신청한 후 다음과 같이 License를 구성해야 합니다. 애플리케이션이 시작될 때 이 작업을 수행하는 것이 좋습니다.

통합 License가 없을 경우 재생 중 예외가 발생할 수 있습니다.
```dart
String licenceURL = ""; // 획득한 licence url
String licenceKey = ""; // 획득한 licence key
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

## 사용자 정의 개발 가이드

Flutter 플러그 인용 Player SDK는 기본 플레이어 기능을 캡슐화합니다. 심층 사용자 정의 개발을 위해 다음 방법을 사용하는 것이 좋습니다.

- VOD 재생(API 클래스는 `TXVodPlayerController`) 또는 라이브 재생(API 클래스는 `TXLivePlayerController`)를 기반으로 사용자 정의 개발을 수행합니다. 이 프로젝트는 example 프로젝트의 `DemoTXVodPlayer` 및 `DemoTXLivePlayer`에서 사용자 정의 개발 Demo를 제공합니다.

- 플레이어 컴포넌트 `SuperPlayerController`는 VOD 및 라이브 방송을 캡슐화하고 간단한 UI 인터랙션을 제공합니다. 코드는 example 디렉터리에 있습니다. 다음과 같이 플레이어 컴포넌트를 사용자 정의할 수 있습니다.

  `exmple/lib/superplayer`의 플레이어 컴포넌트 코드를 사용자 지정 개발을 위해 프로젝트에 복사합니다.

## FAQ

1. iOS에서 `No visible @interface for 'TXLivePlayer' declares the selector 'startLivePlay:type:'`과 같은 누락된 API에 대한 오류가 발생합니다.
다음 명령을 실행하여 iOS SDK를 업데이트합니다.
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

2. tencent_trtc_cloud와 Flutter 플레이어가 동시에 연동되는 경우 SDK 또는 심볼 충돌이 발생합니다.

   일반적인 예외 로그: `java. lang.RuntimeException: Duplicate class com.tencent.liteav.TXLiteAVCode found in modules classes.jar`

   이 경우 tencent_trtc_cloud와 Flutter 플레이어가 모두 LiteAVSDK_Professional의 동일한 버전에 의존하도록 Flutter 플레이어의 Professional 버전을 통합해야 합니다.

   예를 들어 Android용 TXLiteAVSDK_Professional_10.3.0.11196 또는 iOS용 TXLiteAVSDK_Professional to 10.3.12231에 의존하려면 종속성 선언은 다음과 같습니다.
   ```xml
   tencent_trtc_cloud：2.3.8
   
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
       ref: release_pro_v1.0.3.11196_12231
   ```
3. 여러 플레이어 인스턴스를 동시에 사용해야 하는 경우 비디오가 자주 전환되면 비디오 이미지가 흐려집니다.
	각 플레이어 컴포넌트 컨테이너가 종료되면 플레이어의 `dispose` 메소드를 호출하여 플레이어를 해제합니다.
4. Flutter 종속성과 관련된 기타 일반적인 문제:
 - `flutter doctor` 명령을 실행하여, “No issues found!”가 표시될 때까지 런타임 환경을 확인하십시오.
 - `flutter pub get`을 실행하여 모든 종속 컴포넌트가 성공적으로 업데이트되었는지 확인하십시오.

## 추가 기능

프로젝트에서 example을 실행하여 모든 기능을 사용해 볼 수 있습니다.

플레이어 SDK 웹 사이트는 iOS, Android 및 Web용 Demo를 제공합니다. 사용하려면 [여기](https://www.tencentcloud.com/document/product/266/42091)를 클릭하십시오.


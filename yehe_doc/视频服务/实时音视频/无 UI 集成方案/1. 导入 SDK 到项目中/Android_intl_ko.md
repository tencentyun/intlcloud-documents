본 문서에서는 SDK를 프로젝트로 가져오는 방법을 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/956dded61564c3a29ea8e93238d9a4e1.png)

## 개발 환경 요구사항
- Android Studio 3.5+.
- Android 4.1(SDK API 16) 및 이후 버전 시스템.

## 1단계: SDK 가져오기

### 솔루션1: 자동 로딩(aar)
TRTC SDK를 mavenCentral에 이미 배포했다면 gradle 자동 다운로드 설정을 통해 업데이트할 수 있습니다.
1. dependencies에서 TRTCSDK 종속을 추가합니다.
```
dependencies{
        implementation ’com.tencent.liteav:LiteAVSDK_TRTC:latest.release’
}
```
2. defaultConfig에서 App이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
        ndk {
                abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
}
```
>?현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
3. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**를 클릭하여 SDK를 자동으로 다운로드하고 프로젝트에 통합합니다.


### 솔루션2: SDK를 다운로드하여 수동으로 가져오기
1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip) 다운로드 후, 로컬에서 압축을 풉니다.
2. 압축 해제한 aar 파일을 프로그램 **app/libs** 디렉터리에 복사합니다.
3. 프로그램 디렉터리의 build.gradle에 **flatDir**을 추가하고 로컬 라이브러리 경로를 지정합니다.
![](https://main.qcloudimg.com/raw/3b07d38f105167ae52ffdda9a1712cec.png)
4. app/build.gradle에 aar 패킷 레퍼런스 코드를 추가합니다.
![](https://main.qcloudimg.com/raw/143621f900eb6f7b867d89b71c0dd13d.png)
5. app/build.gradle의 defaultConfig에 App이 사용할 CPU 구성을 지정합니다.
```
defaultConfig {
        ndk {
                abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
        }
}
```
>?현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
6. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**를 클릭하여 TRTC SDK 통합을 완료합니다.

## 2단계: App 권한 설정
AndroidManifest.xml에서 App 권한을 설정합니다. TRTC SDK는 다음 권한 허용이 필요합니다.
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

>! `android:hardwareAccelerated="false"`를 설정하지 마십시오. 하드웨어 가속을 비활성화하면 상대방의 비디오 스트리밍을 렌더링할 수 없습니다.

## 3단계: 난독화 규칙 설정
proguard-rules.pro 파일에서 TRTC SDK 관련 사항을 비난독화 리스트에 추가합니다.
```java
-keep class com.tencent.** { *; }
```

[](id:using_cpp)
## C++ 인터페이스를 통해 SDK 사용(옵션)
개발에 Java 대신 C++ 인터페이스 사용을 선호하는 경우 이 단계를 수행할 수 있습니다. Java 언어를 사용하여 TRTC SDK를 호출하는 경우 이 단계를 생략하시기 바랍니다.
1. 먼저 상기 가이드에 따라 jar 및 so 라이브러리 가져오기를 통해 TRTC SDK를 통합합니다.
2. 헤더 파일 복사: SDK의 C++ 헤더 파일을 프로젝트(경로: `SDK/LiteAVSDK_TRTC_xxx/libs/include`)에 복사하고 CMakeLists.txt에 include 폴더 경로 및 so 라이브러리의 동적 링크를 구성합니다.
```java
cmake_minimum_required(VERSION 3.6)

# C++ 인터페이스 헤더 파일 경로 구성
include_directories(
        ${CMAKE_CURRENT_SOURCE_DIR}/include  # SDK/LiteAVSDK_TRTC_xxx/libs/include에서 복사
)

add_library(
        native-lib
        SHARED
        native-lib.cpp)

# libliteavsdk.so 동적 라이브러리 경로 구성
add_library(libliteavsdk SHARED IMPORTED)
set_target_properties(libliteavsdk  PROPERTIES IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/../../../libs/${ANDROID_ABI}/libliteavsdk.so)

find_library(
        log-lib
        log)

# libliteavsdk.so 동적 링크 구성
target_link_libraries(
        native-lib
        libliteavsdk
        ${log-lib})
```
3. 네임스페이스 사용: trtc 네임스페이스에는 C++ 전체 플랫폼 인터페이스의 메소드 및 유형 등이 정의되어 있습니다. 더 간략한 코딩을 위해 trtc 네임스페이스를 사용할 것을 권장합니다.
```
using namespace trtc;
```

>?
>- Android Studio C/C++ 개발 환경을 구성하려면 Android Studio 공식 홈페이지 설명서를 참고하십시오. [Android 프로젝트에 C 및 C++ 코드 추가](https://developer.android.com/studio/projects/add-native-code) . 
>- 현재 TRTC 버전의 SDK만 C++ 인터페이스를 지원합니다. C++ 인터페이스 사용 방법은 [전체 플랫폼 (C++) API 개요](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오.



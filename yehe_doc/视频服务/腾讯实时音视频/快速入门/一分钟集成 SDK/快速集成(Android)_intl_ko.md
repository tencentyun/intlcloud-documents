본 문서에서는 Tencent Cloud TRTC SDK(Android)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 개발 환경 요구사항
- Android Studio 3.5+
- Android 4.1(SDK API 16) 이상 시스템

## SDK 통합(aar)

Gradle 자동 로딩 방식을 사용하거나 수동으로 aar을 다운로드한 후, 현재 프로그래밍 프로젝트에 가져옵니다.

### 방법1: 자동 로딩(aar)
TRTC SDK를 jcenter에 이미 배포했다면 gradle 자동 다운로드 설정을 통해 업데이트할 수 있습니다.
Android Studio를 사용해 통합이 필요한 SDK 프로그램(본 문서는 [TRTCSimpleDemo]를 예시로 함)을 연 후, 간단한 세 단계를 걸쳐 app/build.gradle 파일을 수정하면 SDK 통합이 완료됩니다.
![](https://main.qcloudimg.com/raw/fd01c252724cbf31ec7356286a931661.png)

1. dependencies에서 TRTCSDK 종속을 추가합니다.
 - 3.x 버전의 com.android.tools.build:gradle 툴을 사용하는 경우 다음 명령어를 실행합니다.
```
dependencies {
         implementation 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
 - 2.x 버전의 com.android.tools.build:gradle 툴을 사용하는 경우 다음 명령어를 실행합니다.
```
dependencies {
         compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. defaultConfig에서 앱이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
>
3. [Sync Now]를 클릭하면 SDK가 자동으로 다운로드되고 프로그램에 통합됩니다.


### 방법2: 수동 다운로드(aar)
네트워크에 jcenter 연결 문제가 있을 경우 SDK를 수동으로 다운로드하여 프로그램에 통합할 수 있습니다.

1. 최신 버전 [TRTC SDK](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)를 다운로드합니다.
2. 다운로드한 aar 파일을 프로그램 **app/libs** 디렉터리에 복사합니다.
3. 프로그램 디렉터리의 build.gradle에 **flatDir**을 추가하고 로컬 라이브러리 경로를 지정합니다.
![](https://main.qcloudimg.com/raw/bc3215028103fe980aedcbf011b97b02.png)
4. app/build.gradle에 aar 패킷 레퍼런스 코드를 추가합니다.
![](https://main.qcloudimg.com/raw/449a4a2d8d7cb2503da9fb480beb9c32.png)
5. app/build.gradle의 defaultConfig에 앱이 사용하는 CPU 구성을 지정합니다.
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
>
6. [Sync Now]를 클릭하여 TRTC SDK 통합 작업을 완료합니다.


## SDK 통합(jar)
aar 라이브러리 통합을 원하지 않는다면 jar 및 so 라이브러리 가져오기를 통해 TRTC SDK를 통합할 수도 있습니다.

1. 최신 버전 jar 압축 패킷을 [다운로드](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)합니다. 파일 경로는 `SDK/LiteAVSDK_TRTC_xxx.zip`(xxx는 TRTC SDK 버전 번호)입니다.
2. 압축 해제하면 libs 디렉터리에 jar 파일과 so 파일이 포함되어 있습니다.
3. 압축 해제한 jar 파일과 armeabi, armeabi-v7a, arm64-v8a 폴더를 app/libs 디렉터리에 복사합니다.
![](https://main.qcloudimg.com/raw/5bf82ca89b3a14cca470fcedc048d7fa.png)
4. app/build.gradle에 jar 라이브러리 레퍼런스 코드를 추가합니다.
![](https://main.qcloudimg.com/raw/6ffbb4b79c06555376b137c849b43bb7.png)	
5. app/build.gradle에 so 라이브러리 레퍼런스 코드를 추가합니다.
```
sourceSets {
       main {
           jniLibs.srcDirs = ['libs']
       }
}
```
![](https://main.qcloudimg.com/raw/299eeb5b3e8961e816f3ce17b97b4339.png)
6. app/build.gradle의 defaultConfig에 앱이 사용하는 CPU 구성을 지정합니다. 
```
defaultConfig {
       ndk {
           abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
       }
}
```
>?현재 TRTC SDK는 armeabi, armeabi-v7a, arm64-v8a를 지원합니다.
>
7. [Sync Now]를 클릭하여 TRTC SDK 통합 작업을 완료합니다.


## 앱 권한 설정
AndroidManifest.xml에서 앱 권한을 설정합니다. TRTC SDK는 다음 권한 허용이 필요합니다.

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```
>! `android:hardwareAccelerated="false"`를 설정하지 마십시오. 하드웨어 가속을 비활성화하면 상대방의 비디오 스트리밍을 렌더링할 수 없습니다.

## 난독화 정책 설정
proguard-rules.pro 파일에서 TRTC SDK 관련 사항을 비난독화 리스트에 추가합니다.

```
-keep class com.tencent.** { *; }
```
## 앱 패키징 매개변수 설정
app/build.gradle에서 다음 정보를 추가합니다.

```
packagingOptions {
	pickFirst '**/libc++_shared.so'
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
}
```
![](https://main.qcloudimg.com/raw/e40d5c294a59d56a1f89f20960c7e4c1.png)



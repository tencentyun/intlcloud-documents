Tencent Cloud Game Multimedia Engine(GME) SDK를 이용해주셔서 감사합니다. 안드로이드 개발자 테스트 및 Tencent Cloud GME 프로덕트 API를 원활히 액세스하기 위해 안드로이드 개발 프로그램 설정에 대해 소개드립니다.

## SDK 준비

다음 방법을 통해 SDK를 획득할 수 있습니다.

### SDK 다운로드

[다운로드 매뉴얼](https://intl.cloud.tencent.com/document/product/607/18521)을 참조하여 Demo, SDK를 다운르드하세요.

인터페이스에서 안드로이드 버전용 SDK 리소스를 확인합니다.

다운로드한 SDK 리소스를 압축 해제하면 다음 파트를 포함합니다:

|파일명       | 설명           |
| ------------- |:-------------:|
| Libs     | 개발툴 패키지 Libs     |

## 시스템 사양
SDK는 Android 4.2 및 이상 시스템에서 작동하오나, 오직API 18(Android 4.3) 이상 시스템에서만 하드웨어를 코딩할 수 있습니다.

## 사전 준비 작업

### SDK 파일 추가

개발툴 패키지에 lib 목록의 mobilepb. jar와 wup-1.0.0-SNAPSHOT.jar를 안드로이드 프로그래밍 lib 목록(혹 프로그래밍에 lib 목록이 없다면 스스로 구축하세요. 혹 armeabi, armeabi-v7a가 없다면 함께 lib 목록에 복사하세요)에 복사합니다.  
![](https://main.qcloudimg.com/raw/006cc0fab7b4c2f370b9b31fdbc93f90.png)

### 프로그래밍 사양

프로그래밍 앱 목록 build.gradle에 참조 라이브러리 코드를 추가합니다.  

```
sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
}
```

### 앱 권한 설정

프로그래밍 AndroidManifest.xml 파일에 다음 권한을 추가합니다:


```
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
  <uses-permission android:name="android.permission.BLUETOOTH"/>
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/ >
```

혹 오프라인 음성 메시지를 사용하시려면 티켓 파일 application 노드에 추가하시기 바랍니다:
```
  <application android:usesCleartextTraffic="true" >
```

### 앱 난독화 관련
코드 난독화를 원하시면 하기처럼 설정할 수 있습니다:
```
-dontwarn com.tencent.**
-keep class com.tencent.** { *;}
-keepclassmembers class com.tencent.**{*;}
```


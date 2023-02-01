이 문서는 RT-Cube의 플레이어 SDK를 프로젝트에 빠르게 통합하는 방법을 설명합니다. 여러 버전의 SDK를 동일한 방식으로 통합할 수 있습니다.

## 개발 환경 요구사항
- Android Studio 2.0+.
- Android 4.1(SDK API 16) 및 이후 버전 시스템.

## SDK 통합(aar)
Gradle 자동 로딩 방식을 사용하거나 수동으로 aar을 다운로드한 후, 귀하의 현재 프로그래밍 프로젝트에 가져옵니다.

### 방법1: 자동 로딩(aar) 
플레이어 SDK가 [mavenCentral 리포지토리](https://repo1.maven.org/maven2/com/tencent/liteav/LiteAVSDK_Player_Premium/)에 릴리스되었으며 gradle에서 LiteAVSDK_Player_Premium 업데이트를 자동으로 다운로드하도록 구성할 수 있습니다.
Android Studio로 프로젝트를 열고 아래 설명된 대로 `build.gradle` 파일을 수정하여 통합을 완료합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7de67c57e87f2803217b77ed308d537d.png)

1. 프로젝트의 루트 디렉터리에 있는 build.gradle에 mavenCentral 리포지토리를 추가합니다.
```xml
repositories {
    mavenCentral()
}
```

2. app 디렉터리에서 build.gradle을 열고 LiteAVSDK_Player 종속성을 dependencies에 추가합니다.
```
dependencies{
  // 이 구성은 기본적으로 LiteAVSDK_Player_Premium의 최신 버전을 통합합니다
	implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:latest.release'
  // 10.8.0.29000과 같은 이전 버전을 통합하려면 다음과 같이 구성합니다
  // implementation 'com.tencent.liteav:LiteAVSDK_Player_Premium:10.8.0.29000'
}
```
3. defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK_Player는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
4. ![](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png) Sync Now를 클릭하여 SDK를 동기화합니다. mavenCentral에 연결할 수 있으면 SDK가 자동으로 다운로드되어 곧 프로젝트에 통합됩니다.

### 방법2: 수동 다운로드(aar)
mavenCentral에 액세스하는 데 문제가 있는 경우 SDK를 수동으로 다운로드하여 프로젝트에 통합할 수 있습니다.
1. [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip)을 다운로드하고 파일의 압축을 풉니다.
2. SDK 디렉터리의 aar 파일을 프로젝트의 **app/libs** 디렉터리에 복사합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab00ad0f12a271750d6f84f7333f8cd3.png)
3. **flatDir**을 프로젝트 루트 디렉터리 아래의 build.gradle에 추가하여 리포지토리의 로컬 경로를 지정합니다.
    ![](https://main.qcloudimg.com/raw/726771558714a2b4fae8dc1a59c33ffc.png) 
4. LiteAVSDK_Player_Premium 종속성을 추가한 다음 app/build.gradle에서 aar 파일 레퍼런스 코드를 추가합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ac9ab42dda8992d435832c605f1e6798.png)
```
implementation(name:'LiteAVSDK_Player_10.8.0.29000', ext:'aar')
```
5. `app/build.gradle`의 defaultConfig에서 App에서 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK_Player는 armeabi, armeabi-v7a 및 arm64-v8a 지원).
```
defaultConfig {
	ndk {
		abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
	}
}
```
6. Sync Now를 클릭하여 LiteAVSDK를 동기화합니다.

## SDK 통합(jar)
aar 라이브러리를 통합하지 않으려면 jar 및 so 라이브러리를 가져와서 LiteAVSDK를 통합하도록 선택할 수 있습니다.

1. [LiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_Android_latest.zip)을 다운로드하고 압축을 풉니다. SDK 디렉터리에서 `LiteAVSDK_Player_Premium_xxx.zip`(`xxx`는 버전 번호)을 찾습니다. 압축을 풀면 아래와 같이 jar 파일과 so 파일의 폴더가 포함된 libs 디렉터리를 얻을 수 있습니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab82529bd214ba8488f29b45b38f61f6.png)

  armeabi 아키텍처용 so 파일도 필요한 경우 armeabi-v7a 디렉터리를 복사하고 이름을 armeabi로 바꾸십시오.

2. 해당 jar 파일과 armeabi, armeabi-v7a 및 arm64-v8a 폴더를 `app/libs` 디렉터리에 복사합니다.
    ![](https://main.qcloudimg.com/raw/d9b6339cb52fb85afda42de6001be337.png)
3. `app/build.gradle`에서 jar 라이브러리 레퍼런스 코드를 추가합니다.
    ![](https://main.qcloudimg.com/raw/695520309d9a01b19ce2f50439a42890.png)      
```
dependencies{
	implementation fileTree(dir:'libs',include:['*.jar'])
}
```
4. 프로그램 디렉터리의 build.gradle에 **flatDir**을 추가하고 로컬 라이브러리 경로를 지정합니다.
![](https://main.qcloudimg.com/raw/6c68b846f6f7258ae4d96bc1d95d7816.png)
5. `app/build.gradle`에 so 라이브러리 레퍼런스 코드를 추가합니다.
![](https://main.qcloudimg.com/raw/e0f2f39c5f53a9fd5ca084febdd4e637.png)
6. `app/build.gradle`의 defaultConfig에서 App이 사용할 CPU 아키텍처를 지정합니다(현재 LiteAVSDK는 armeabi, armeabi-v7a 및 
```
defaultConfig {
    ndk {
        abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
    }
}
```
7. Sync Now를 클릭하여 LiteAVSDK를 동기화합니다.

## App 패키징 매개변수 설정
![](https://main.qcloudimg.com/raw/dabfd69ee06e4d38bb3b51fc436c0ad1.png)
```
packagingOptions {
	pickFirst ’**/libc++_shared.so’
	doNotStrip "*/armeabi/libYTCommon.so"
	doNotStrip "*/armeabi-v7a/libYTCommon.so"
	doNotStrip "*/x86/libYTCommon.so"
	doNotStrip "*/arm64-v8a/libYTCommon.so"
} 
```

## App 권한 설정

AndroidManifest.xml에서 App 권한을 구성합니다. LiteAVSDK에는 다음 권한이 필요합니다.

```
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--스토리지-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

## 난독화 규칙 구성
proguard-rules.pro 파일에서 LiteAVSDK 클래스를 난독화 금지 목록에 추가합니다.

```
-keep class com.tencent.** { *; }
```

## License 권한 구성

[Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license)의 안내에 따라 [Applying for a trial license](https://www.tencentcloud.com/document/product/266/51098)를 클릭하여 트라이얼 라이선스를 신청합니다. License가 구성되지 않은 경우 비디오 재생이 실패합니다. licenseURL과 암호 해독 key라는 두 개의 문자열을 받게 됩니다.

App에서 SDK 기능을 사용하기 전에 다음 구성을 완료하십시오(가급적 Application 클래스에서).

```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // 획득한 licence url
        String licenceKey = ""; // 획득한 licence key
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXLiveBase.setListener(new TXLiveBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

## 조회 방법

License가 성공적으로 구성되면 아래 API를 호출하여 License 정보를 볼 수 있습니다. 구성이 적용되는 데 시간이 걸릴 수 있습니다. 정확한 소요 시간은 네트워크 상태에 따라 다릅니다.

```java
TXLiveBase.getInstance().getLicenceInfo();
```

## FAQ

1. 내 프로젝트가 CSS, TRTC 및 Player와 같은 LiteAVSDK의 여러 버전을 통합하여 중복 기호 오류가 발생하면 어떻게 해야 합니까?

둘 이상의 LiteAVSDK 버전(MLVB, Player, TRTC, UGSV)을 통합하면 프로젝트를 빌드할 때 라이브러리 충돌 오류가 발생합니다. SDK의 기본 라이브러리 간에 일부 기호 파일이 공유되기 때문입니다. 문제 해결을 위해 MLVB, Player, TRTC, UGSV의 기능이 포함된 All-in-One SDK를 통합하는 것을 권장합니다. 자세한 내용은 [SDK 다운로드](https://www.tencentcloud.com/document/product/266/50561)를 참고하십시오.

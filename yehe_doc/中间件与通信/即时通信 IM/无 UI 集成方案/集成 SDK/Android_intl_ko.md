본문은 Tencent Cloud IM SDK를 Android 프로젝트에 빠르게 통합하는 방법을 설명합니다.

## 개발 환경 요구사항
- JDK 1.6.
- Android 4.1(SDK API 16) 및 이후 버전 시스템.

## SDK 통합(aar)
Gradle 자동 로딩 방식을 사용하거나 수동으로 aar을 다운로드한 후, 귀하의 현재 프로그래밍 프로젝트에 가져옵니다.

### 방법1: 자동 로딩(aar)
Maven Central 리포지토리에 게시된 IM SDK를 업데이트를 자동으로 다운로드하도록 gradle을 구성할 수 있습니다.
Android Studio를 사용하여 프로젝트를 열고 app/build.gradle 파일을 간단한 3단계로 수정하여 아래와 같이 SDK를 프로젝트에 통합합니다.

#### 1단계: SDK 종속성 추가

1. app의 build.gradle을 찾아 repositories에 mavenCentral() 종속성을 추가합니다.
```
 repositories {
        google()
        jcenter()
        // mavenCentral 리포지토리를 추가합니다
        mavenCentral()
 }
```
2. dependencies에 IM SDK 종속성을 추가합니다.
 - IM SDK 기본 버전을 사용하는 경우 다음 종속성을 추가합니다.
```
dependencies{
		api 'com.tencent.imsdk:imsdk:버전 번호'
}
```
 - IM SDK 인핸스드 버전을 사용하는 경우 다음 종속성을 추가합니다.
```
dependencies{
		api 'com.tencent.imsdk:imsdk-plus:버전 번호'
}
```
 - Pro IM SDK 인핸스드 버전을 사용하는 경우 다음 종속성을 추가합니다.
```
dependencies{
		api 'com.tencent.imsdk:imsdk-plus-pro:버전 번호'
}
```

>?‘버전 번호’를 SDK의 실제 버전 번호로 바꿉니다. [최신 버전]( https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK)을 사용하는 것이 좋습니다.
>버전 번호 `5.4.666`을 예로 들어 보겠습니다.
>```
>dependencies{
>	api 'com.tencent.imsdk:imsdk-plus:5.4.666'
>}
```
>
 
#### 2단계: App 아키텍처 지정
defaultConfig에서 App이 사용하는 CPU 아키텍처를 지정합니다(armeabi-v7a, arm64-v8a, x86 및 x86_64는 IM SDK v4.3.118부터 지원됨).
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

#### 3단계: SDK 동기화
동기화 아이콘을 클릭합니다. jcenter에 대한 연결이 정상이면 SDK가 자동으로 다운로드되어 프로젝트에 통합됩니다.
![](https://main.qcloudimg.com/raw/99c145e1bfdc78b1af5c6fb8cebde90b.png)


### 방법2: 수동 다운로드(aar)
jcenter에 액세스할 수 없는 경우 SDK를 수동으로 다운로드하여 프로젝트에 통합할 수 있습니다.
#### 1단계: IM SDK 다운로드
GitHub에서 최신 버전의 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK)를 다운로드합니다.

#### 2단계: IM SDK를 프로젝트 디렉터리에 복사
다운로드한 aar 파일을 app 프로젝트의 **/libs** 디렉터리에 복사합니다.
![](https://main.qcloudimg.com/raw/4175f483d55c2f99b99c993ada8dd5a0.png)

#### 3단계: App에서 사용하는 아키텍처 지정 및 아키텍처 컴파일 및 실행
app/build.gradle의 defaultConfig에서 App에서 사용하는 CPU 아키텍처를 지정합니다(armeabi-v7a, arm64-v8a, x86 및 x86_64는 IM SDK v4.3.118부터 지원됨).
```
defaultConfig {
	ndk {
		abiFilters "arm64-v8a"
	}
}
```


## SDK 통합
aar 라이브러리를 통합하지 않으려면 jar 및 so 라이브러리 가져와서 IM SDK를 통합할 수 있습니다.

#### 1단계: IM SDK 다운로드 및 압축 해제
GitHub에서 aar 파일의 최신 버전을 [다운로드](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK)하고 압축을 해제합니다. 추출된 폴더에는 jar 파일과 so 서브 폴더가 포함되어 있습니다. **classes.jar**의 이름을 **imsdk.jar**로 바꿉니다.
![](https://main.qcloudimg.com/raw/ecc6ae484565b0170c42698825951eba.png)

#### 2단계: SDK 파일을 프로젝트 디렉터리에 복사
이름이 바뀐 jar 파일과 다른 아키텍처의 so 파일을 Android Studio의 기본 로딩 디렉터리에 복사합니다.
![](https://main.qcloudimg.com/raw/237b44da2ec04ba87a6cef66aa0b5321.png)

#### 3단계: App에서 사용하는 아키텍처 지정 및 아키텍처 컴파일 및 실행
app/build.gradle의 defaultConfig에서 App에서 사용하는 CPU 아키텍처를 지정합니다(armeabi-v7a, arm64-v8a, x86 및 x86_64는 IM SDK v4.3.118부터 지원됨).
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

## 앱 권한 설정
AndroidManifest.xml에서 App 권한을 설정합니다. IM SDK는 다음 권한 허용이 필요합니다.

```
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

## 난독화 정책 설정
proguard-rules.pro 파일에서 IM SDK 클래스를 난독화 금지 목록에 추가합니다.

```
-keep class com.tencent.imsdk.** { *; }
```

본 문서에서는 Tencent Cloud TRTC SDK(QT의 Windows 및 Mac 버전)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 신속하게 완료할 수 있습니다.

## Windows 통합
### 개발 환경 요건
- 운영 체제: Windows 7 이상 버전
- 개발 환경: Visual Studio 2015 이상 버전, Visual Studio 2015 사용 권장. VS 관련 QT 개발 환경 설정이 완료되어 있어야 합니다.
>? VS 관련 QT 개발 환경 설정에 익숙하지 않은 경우, [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md)의 운영 단계 중 4단계를 참고하십시오.

### 작업 단계
이 섹션에서는 간단한 QTTest 프로젝트를 예시로 사용하여 C++용 TRTC SDK를 Visual Studio 프로젝트에 통합하는 방법을 보여줍니다.

1. **C++용 TRTC SDK 다운로드**[](id:win_step1)
	1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip)를 다운로드한 후 파일의 압축을 풀고 엽니다.
	2. QTTestt 프로젝트 디렉터리에 SDK용 빈 폴더를 만들고 SDK의 `TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus`를 폴더로 복사합니다.
2. **QTTest 프로젝트에 대한 종속 환경 구성**[](id:win_step2)
<dx-tabs>
:::  시나리오1: QtCreator 사용
QTTest 프로젝트의 디렉터리로 이동하여 텍스트 편집기([Sublime Text](http://www.sublimetext.com/3) 권장)를 사용해 `QTTest.pro`(Qt Creator로 생성) 를 열고 다음 SDK 참조를 추가하십시오.
<dx-codeblock>
::: windows
INCLUDEPATH += $$PWD/.
               $$PWD/../SDK/CPlusPlus/Win32/include \
               $$PWD/../SDK/CPlusPlus/Win32/include/TRTC

DEPENDPATH += $$PWD/.
               $$PWD/../SDK/CPlusPlus/Win32/include \
               $$PWD/../SDK/CPlusPlus/Win32/include/TRTC

CONFIG += opengl
CONFIG += debug_and_release

debug {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	} else {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}

release {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	} else {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}
:::
</dx-codeblock>
:::
::: 시나리오2: VS 사용
프로젝트가 고도화된 VS 프로젝트인 경우:
1. VS의 프로젝트 속성 **링커** > **입력** > **추가 종속 항목**에 SDK 라이브러리 파일 `liteav.lib`를 추가할 수도 있습니다.
2. **링커** > **일반** > **라이브러리 디렉터리 추가**에서 SDK 라이브러리 경로를 구성합니다. 64비트를 예로 들면 `$(ProjectDir)SDK\CPlusPlus\Win64\lib`입니다.
3. 동시에 **C/C++** > **일반** > **인클루젼 디렉터리 추가**에서 SDK 헤더 파일 경로 `$(ProjectDir)SDK\CPlusPlus\Win64\include` 및 `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`를 설정합니다.

<dx-alert infotype="explain">32비트라면 상기 경로에서 Win64를 Win32로 변경합니다.</dx-alert>
:::
</dx-tabs>

3. **파일 복사**[](id:win_step3)
	- QtCreator로 `QTTest.pro`를 열고 프로그램을 디버깅할 때 `debug/release` 폴더가 자동 생성됩니다. `SDK/CPlusPlus/Win64/lib` (32비트인 경우 `SDK/CPlusPlus/Win32/lib` 복사)의 모든 `.dll` 파일을 프로젝트 디렉터리 `debug/release` 폴더에 복사해야 합니다.
	- VS로 디버깅할 때 `SDK/CPlusPlus/Win64/lib` 아래의 모든 `.dll` 파일을 프로그램의 출력 실행 디렉터리에 수동으로 복사하거나, **이벤트 생성** > **사후 이벤트 생성** > **명령 라인**에서 복사 명령 `copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)`를 추가할 수도 있습니다. 컴파일이 완료되면 SDK의 .dll 파일을 프로그램의 실행 디렉터리에 자동으로 복사할 수 있습니다.
>?32비트인 경우 `copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)` 복사 명령을 추가합니다.
4. **TRTC SDK 참조**[](id:win_step4)
	- 헤더 파일 `#include "ITRTCCloud.h"`를 통해 직접 참조할 수 있습니다.
	- 네임스페이스 사용: 크로스 플랫폼 C++ API의 메소드 및 유형은 trtc 네임스페이스에 정의됩니다. 코드를 단순화하려면 trtc 네임스페이스를 사용하는 것이 좋습니다.

>? 통합 작업이 완료되어 프로젝트를 컴파일할 수 있습니다. 크로스 플랫폼 SDK의 API 사용 Demo에 대한 자세한 내용은 [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)를 다운로드하여 참고하십시오.

## Mac 통합
### 개발 환경 요건

- 운영 체제: Mac10.10 이상 버전
- 개발 환경: Qt Creator 4.10.3 이상 버전, Qt Creator 4.13.3 이상 사용 권장
- 개발 프레임워크: Based on Qt 5.10 이상

### 작업 단계
이 섹션에서는 C++용 TRTC SDK를 Qt Creator의 프로젝트에 통합하는 방법을 보여주기 위해 처음부터 생성된 QTTest 프로젝트를 예시로 사용합니다.

[](id:mac_step1)
1. **C++용 크로스 플랫폼 SDK 다운로드**
	1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2)를 다운로드한 후 파일의 압축을 풀고 엽니다.
	2. QtTest 프로젝트 디렉터리에 SDK용 빈 폴더를 생성하고 SDK의 `TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework`를 해당 폴더에 복사합니다.
2. **QTTest.pro 구성**[](id:mac_step2)
QTTest 프로젝트의 디렉터리로 이동하여 텍스트 편집기로 `QTTest.pro`를 열고 다음 SDK 참조를 추가하십시오.
```MAC
INCLUDEPATH += $$PWD/.
DEPENDPATH += $$PWD/.

LIBS += "-F$$PWD/base/util/mac/usersig"
LIBS += "-F$$PWD/../SDK"
LIBS += -framework TXLiteAVSDK_TRTC_Mac
LIBS += -framework Accelerate
LIBS += -framework AudioUnit

INCLUDEPATH += $$PWD/../SDK/TXLiteAVSDK_TRTC_Mac.framework/Headers/cpp_interface

INCLUDEPATH += $$PWD/base/util/mac/usersig/include
DEPENDPATH += $$PWD/base/util/mac/usersig/include
```

3. **카메라 및 마이크 권한 요청**[](id:mac_step3)
TRTC SDK에서 카메라와 마이크를 사용하려면 `Info.plist`에 권한 요청을 추가해야 합니다. 권한 신청 설명은 다음과 같습니다.
```none
NSMicrophoneUsageDescription: 마이크 사용 권한 신청
NSCameraUsageDescription: 카메라 사용 권한 신청
```
다음 이미지 참고:
![](https://qcloudimg.tencent-cloud.cn/raw/dc42db42bf51f14a8e22326edc3f0a16.png)
4. **TRTC SDK 참조**[](id:mac_step4)
	- 헤더 파일 `#include "ITRTCCloud.h"`를 사용하여 SDK를 참조하십시오.
	- 네임스페이스 사용: 크로스 플랫폼 C++ API의 메소드 및 유형은 trtc 네임스페이스에 정의됩니다. 코드를 단순화하려면 trtc 네임스페이스를 사용하는 것이 좋습니다.

>? 이것으로 통합 프로세스가 완료되고 프로젝트 컴파일을 진행할 수 있습니다. [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)를 다운로드하여 SDK의 크로스 플랫폼 API 사용에 대해 참고하십시오.

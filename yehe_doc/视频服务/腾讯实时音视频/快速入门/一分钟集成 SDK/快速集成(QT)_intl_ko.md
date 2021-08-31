본 문서에서는 Tencent Cloud TRTC SDK(QT의 Mac 및 Windows 버전)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 신속하게 완료할 수 있습니다.

## Mac 통합
### 개발 환경 요건

- 운영 체제: Mac10.10 이상 버전
- 개발 환경: Qt Creator 4.10.3 이상 버전, Qt Creator 4.13.3 이상 사용 권장
- 개발 프레임워크: Based on Qt 5.10 이상

### 작업 순서
본 장에서는 아무 것도 없는 상태에서 간단한 QTTest 프로젝트 생성 예시를 통해 Qt Creator 프로그램에 C++ 크로스 플랫폼 SDK를 통합하는 방법을 소개합니다.

[](id:mac_step1)
#### 1단계: C++ 크로스 플랫폼 SDK 다운로드
1. [SDK](https:/liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2) 다운로드 후 압축을 해제하고 파일을 엽니다.
2. QTTest와 동일한 레벨의 디렉터리에 빈 SDK 폴더를 생성하고, 생성된 SDK 폴더에 1번에서 다운로드한 `TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework`를 복사합니다.

[](id:mac_step2)
#### 2단계: QTTest.pro 설정
QTTest 프로그램 디렉터리를 열고, 임의의 문서 편집기를 사용해 `QTTest.pro` 파일을 열어 다음의 SDK 관련 레퍼런스를 추가합니다.

```
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

[](id:mac_step3)
#### 3단계: 카메라 및 마이크 사용 권한 추가

SDK에서 사용자의 카메라와 마이크를 사용하므로 해당하는 `Info.plist`에 대응하는 권한을 추가해야 합니다. 권한 신청 설명은 다음과 같습니다.
```none
NSMicrophoneUsageDescription: 마이크 사용 권한 신청
NSCameraUsageDescription: 카메라 사용 권한 신청
```
다음 이미지를 참고하십시오.

[](id:mac_step4)
#### 4단계: TRTC SDK 참조
1. 헤더 파일 `#include "ITRTCCloud.h"`를 통해 직접 참조할 수 있습니다.
2. 네임스페이스 사용: trtc 네임스페이스에는 C++ 전체 플랫폼 인터페이스의 메소드 및 유형 등이 정의되어 있습니다. 더 간략한 코딩을 위해 직접 trtc 네임스페이스를 사용하길 권장합니다.

>? 통합 작업이 완료되어 프로젝트를 컴파일할 수 있습니다. 크로스 플랫폼 SDK의 API 사용 Demo에 대한 자세한 내용은 [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac)를 다운로드하여 참조하십시오.

## Windows 통합
### 개발 환경 요건
- 운영 체제: Windows 7 이상 버전
- 개발 환경: Visual Studio 2015 이상 버전, Visual Studio 2015 사용 권장. VS 관련 QT 개발 환경 설정이 완료되어 있어야 합니다.
>? VS 관련 QT 개발 환경 설정에 익숙하지 않은 경우, [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md)의 제2절 내용을 참조하십시오.

### 작업 순서
본 장에서는 간단한 QTTest 프로젝트 생성 예시를 통해 Visual Studio에 C++ 크로스 플랫폼 SDK를 통합하는 방법을 소개합니다.

[](id:win_step1)
#### 1단계: C++ 크로스 플랫폼 SDK 다운로드
1. [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip) 다운로드 후 압축을 해제하고 파일을 엽니다.
2. QTTest와 동일한 레벨의 디렉터리에 빈 SDK 폴더를 생성하고, 생성된 SDK 폴더에 1번에서 다운로드한 `TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus`를 복사합니다.

[](id:win_step2)
#### 2단계: QTTest 프로그램의 종속 환경 설정
##### 시나리오1: QtCreator를 사용한 종속 환경 설정
QTTest 프로그램 디렉터리를 열고, 임의의 문서 편집기([Sublime Text](http://www.sublimetext.com/3) 권장)를 사용해 `QTTest.pro`(Qt Creator로 생성한) 파일을 열어 다음의 SDK 관련 레퍼런스를 추가합니다.
```
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
```
##### 시나리오2: VS를 사용한 종속 환경 설정
프로그램이 이미 안정적인 VS 프로젝트라면, VS의 프로그램 속성 `Properties->Linker->Input과 General`에서 SDK 라이브러리 경로 종속 정보를 설정할 수 있으며, 이와 함께 `Properties -> C/C++ -> General`에서 SDK의 헤더 파일 경로 종속 정보를 설정할 수 있습니다.

[](id:win_step3)
#### 3단계: 파일 복사
VS를 사용해 `QTTest.pro` 프로그램을 열면 자동으로 관련 `debug/release` 폴더가 생성되며, `SDK/CPlusPlus/Win32/lib` 아래에 있는 모든 `.dll` 파일을 각 프로그램 디렉터리의 `debug/release` 폴더로 복사해야 합니다.

[](id:win_step4)
#### 4단계: TRTC SDK 참조
1. 헤더 파일 `#include "ITRTCCloud.h"`를 통해 직접 참조할 수 있습니다.
2. 네임스페이스 사용: trtc 네임스페이스에는 C++ 전체 플랫폼 인터페이스의 메소드 및 유형 등이 정의되어 있습니다. 더 간략한 코딩을 위해 직접 trtc 네임스페이스를 사용하길 권장합니다.

>? 통합 작업이 완료되어 프로젝트를 컴파일할 수 있습니다. 크로스 플랫폼 SDK의 API 사용 Demo에 대한 자세한 내용은 [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)를 다운로드하여 참조하십시오.

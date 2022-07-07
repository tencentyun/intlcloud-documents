본 문서에서는 Tencent Cloud TRTC SDK(QT의 Windows 및 Mac 버전)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 신속하게 완료할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/956dded61564c3a29ea8e93238d9a4e1.png)

## Windows 통합
### 개발 환경 요건
- 운영 체제: Windows 7 이상 버전
- 개발 환경: Visual Studio 2015 이상 버전, Visual Studio 2015 사용 권장. VS 관련 QT 개발 환경 설정이 완료되어 있어야 합니다.
>? VS 관련 QT 개발 환경 설정에 익숙하지 않은 경우, [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md)의 운영 단계 중 4단계를 참고하십시오.

### 작업 단계
본 섹션에서는 간단한 QT 프로젝트를 생성하는 예시를 통해 Visual Studio에 C++ SDK를 통합하는 방법을 소개합니다.

### 1단계: SDK 다운로드
1. [SDK 다운로드](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip) 후, 압축을 풀고 엽니다.
본 문서의 예시에서는 SDK 디렉터리에 있는 C++ 버전의 SDK 파일만 참조하면 됩니다. 64비트를 예로 들면 SDK 위치는 `./SDK/CPlusPlus/Win64/`이며 주로 다음 부분을 포함합니다.
<table>
<thead>
<tr>
<th>디렉터리 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>include</td>
<td>자세한 인터페이스 주석이 있는 API 헤더 파일</td>
</tr>
<tr>
<td>lib</td>
<td>컴파일용 .lib 파일 및 실행 시 로딩하는 .dll 파일</td>
</tr>
</tbody></table>

### 2단계: 프로젝트 생성[](id:using_cpp_qt_step2)
Visual Studio 2015를 예로 들어 [QT](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe) 및 [VS 개발 플러그 인](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix)이 로컬에 설치되었다는 전제 하에 Visual Studio를 엽니다. 아래와 같이 'TRTCDemo'라는 새 QT 응용 프로그램을 만듭니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fa665d6c78420db0da022ae81f2d7c68.png)
신속하게 통합하는 방법을 쉽게 소개하기 위해, 마법사에서 **Qt Widgets Application** 유형을 선택하고 **확인**을 클릭한 후 프로젝트가 생성될 때까지 다음 페이지에서 **Next**를 클릭합니다.

### 3단계: 파일 복사[](id:using_cpp_qt_step3)
다음 이미지와 같이 압축 해제한 SDK 폴더를 TRTCDemo.vcxproj가 있는 디렉터리에 복사합니다.
>?현재는 C++ SDK만 필요하며 SDK 경로 아래의 CSharp 디렉터리는 삭제할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

### 4단계: 프로젝트 구성 수정[](id:using_cpp_qt_step4)
TRTCDemo 속성 페이지를 열어 **솔루션 리소스 관리자** > **TRTCDemo 프로젝트 오른쪽 메뉴** > **속성**을 선택하고 다음 순서에 따라 설정합니다.
1. **포함 디렉터리 추가:**
**C/C++** > **일반** > **인클루젼 디렉터리 추가**에서 64비트를 예로 들어 아래와 같이 SDK 헤더 파일 디렉터리 `$(ProjectDir)SDK\CPlusPlus\Win64\include` 및 `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC`를 추가합니다.
>?32비트인 경우 SDK 헤더 파일 디렉터리를 `$(ProjectDir)SDK\CPlusPlus\Win32\include` 및 `$(ProjectDir)SDK\CPlusPlus\Win32\include\TRTC`로 설정해야 합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/61a49b758ecb52ab6ee576421da5800d.png)
2. **라이브러리 디렉터리 추가:**
**링커** > **일반** > **라이브러리 디렉터리 추가**에서 다음 이미지와 같이 64비트를 예로 들어 SDK 라이브러리 디렉터리 `$(ProjectDir)SDK\CPlusPlus\Win64\lib`를 추가합니다.
>?32비트인 경우 SDK 라이브러리 디렉터리를 `$(ProjectDir)SDK\CPlusPlus\Win32\lib` 으로 설정해야 합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/89b465c893f456edacf3355dc59f0258.png)
3. **라이브러리 파일 추가:**
**링커** > **입력** > **종속 항목 추가**에서 아래와 같이 SDK 라이브러리 파일 `liteav.lib`를 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/7eb6bbe2351dc4cd3e6c7ae817042fae.png)
4. **copy 명령어 추가:**
**이벤트 생성** > **사후 이벤트 생성** > **명령 라인**에 명령어 `copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)`를 복사 및 추가하면 컴파일 완료 후 자동으로 SDK의 .dll 파일이 프로그램 실행 디렉터리에 복사됩니다. 다음 이미지와 같습니다.
>?32비트인 경우 복사 명령을 `copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)` 로 추가합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/c6cb6d0dfd935be7a74313881a306c5f.png)

### 5단계: SDK 버전 번호 출력[](id:using_cpp_qt_step5)
1. `TRTCDemo.cpp` 파일 상단에 헤더 파일 가져오기를 추가합니다. 코드는 다음과 같습니다.
``` c++
#include "ITRTCCloud.h"
#include <QLabel>
```
2. `TRTCDemo.cpp` 파일의 `TRTCDemo::TRTCDemo` 구조 함수에서 다음 테스트 코드를 추가합니다.
```C++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());

QString sdk_version = QString("SDK Version: %1").arg(version.c_str());
QLabel* label_text = new QLabel(this);
label_text->setAlignment(Qt::AlignCenter);
label_text->resize(this->width(), this->height());
label_text->setText(sdk_version);
```
3. F5를 눌러 실행하면 다음 이미지와 같이 SDK 버전이 출력됩니다.  
![](https://qcloudimg.tencent-cloud.cn/raw/bc1ddf818e5f0571c72d34ba212691c7.png)



## Mac 통합
### 개발 환경 요건

- 운영 체제: Mac10.10 이상 버전
- 개발 환경: Qt Creator 4.10.3 이상 버전, Qt Creator 4.13.3 이상 사용 권장
- 개발 프레임워크: Based on Qt 5.10 이상

### 작업 단계
이 섹션에서는 QTTest 프로젝트 생성을 예시로 TRTC C++ SDK를 Qt Creator의 프로젝트에 통합하는 방법을 소개합니다.

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

## FAQ
- 다음 오류가 발생하는 경우 상기 프로그램 설정에 따라 SDK 헤더 파일의 디렉터리를 정확하게 추가했는지 확인합니다.
```
fatal error C1083: 포함된 파일을 열 수 없습니다. “TRTCCloud.h”: No such file or directory
```

- 다음 오류가 발생하는 경우 상기 프로그램 설정에 따라 SDK 라이브러리 디렉터리 및 라이브러리 파일을 정확하게 추가했는지 확인합니다.
```
error LNK2019: 리졸브할 수 없는 외부 부호 "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ), 해당 부호는 "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ) 함수에 참조됩니다.
```
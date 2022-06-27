본 문서는 효율적인 레이아웃과 강력한 적용성을 갖춘 멀티미디어 커뮤니케이션 및 협업 툴인 PC TUIRoom 모듈을 소개합니다. 협업 업무, 원격 채용, 원격 진료, 보험 청구, 온라인 고객 서비스, 화상 면접, 디지털 정부 업무, 금융 디지털화, 온라인 회의 및 온라인 교육과 같은 시나리오에서 사용할 수 있습니다. 다양한 산업 시나리오와의 긴밀한 통합을 통해, 기업은 비용을 절감하고 효율성을 높이며, 디지털 혁신을 가속화하고, 경쟁력을 높일 수 있습니다.
[Windows](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe) 또는 [Mac](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2)용 App을 다운로드 및 설치하여 컴포넌트를 체험해 볼 수 있습니다.

## 효과
<table>
<tr><td><img src="https://qcloudimg.tencent-cloud.cn/raw/74790d1eb59abc94e264e4e8bca3604b.png"></td>
</tr></table>



## 솔루션 장점
- TUIRoom은 초저지연 음성/화상 통화, 채팅방, 화면 공유, 뷰티 필터, 장치 감지, 통계 등의 다양한 기능을 통합하여 그룹 오디오/비디오 룸의 공통 기능을 다룹니다.
- 사용자 정의 UI 및 레이아웃을 빠르게 구현하기 위해 필요에 따라 추가로 개발할 수 있으므로 비즈니스를 빠르게 시작할 수 있습니다.
- 기본 TRTC 및 IM SDK를 캡슐화하여 기본 로직 제어를 구현하고 기능을 쉽게 호출할 수 있는 API를 제공합니다.

## 연결 가이드
그룹 오디오/비디오 룸 기능에 빠르게 연결할 수 있는 두 가지 연결 방법을 권장합니다. 2차 개발에 적합한 방법을 선택할 수 있습니다.
- [외부 프로세스를 통해 시작](#start)
- [나만의 UI 커스터마이징](#ui)

### 환경 준비
- **Windows 환경** :
	- 통합 개발 환경: Visual Studio 2015 이상.
	- QT 5.9.1 이상.
	- Qt Visual Studio Tools 2.2.0 이상.
	- 운영 체제: Windows 8 이상.
	- 통합 개발 환경에서 정상적으로 프로젝트를 개발할 수 있는지 확인하십시오.
- **Mac 환경**:
	- QT5.9.1 이상.
	- QtCreator 개발 환경을 통합합니다. QtCreator를 사용하기 위해서는 QT 설치 시 선택하고 QT 공식 설치 패키지 버전과 동일합니다.
	- QtCreator 통합 개발 환경에서 정상적으로 프로젝트를 개발할 수 있는지 확인하십시오.

### 외부 프로세스를 통해 시작[](id:start)
1. **RoomApp 프로그램 컴파일**
	- 외부 프로세스를 사용하여 RoomApp을 시작하는 방법은 기존 RoomApp의 실행 프로그램에 따라 다르며, 사전에 컴파일해야 합니다.
	- [RoomApp](https://github.com/tencentyun/TUIRoom)으로 이동하여 소스 코드를 Clone하고 RoomApp을 컴파일 및 생성하도록 프로젝트를 구성합니다.
2. **TestApp 프로젝트 생성**
<dx-tabs>
::: Windows 플랫폼
1. VS를 열고 Qt Widgets Application 프로젝트 유형을 선택하고 TestApp 프로젝트를 작성합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/45b191db25ad1a36eb2c10440f1790ce.png" width="600">
2. 프로세스 시작 프로그램을 작성하고 적절한 위치에서 LoadRoomApp 함수를 호출합니다.
```C++
#include <QProcess>
#include <QApplication>
void LoadRoomApp() {
    QString executable_file_path = QApplication::applicationDirPath();
    QString app_path = executable_file_path + "/RoomApp.exe";
    QProcess::startDetached(app_path);
}
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/0943ef183039229ff92cb54b2bdc4b2a.png" width="600">
3. 프로젝트를 컴파일하고 RoomApp 컴파일 결과를 현재 실행 가능한 프로그램의 디렉터리에 복사합니다. 다음은 release x86 프로그램을 예로 들 수 있습니다.
`TUIRoom\Windows-Mac\RoomApp\bin\Win32\Release` 디렉터리의 모든 파일을 현재 프로그램 디렉터리로 복사합니다.
4. TestApp과 RoomApp을 동시에 시작하는 프로그램을 실행합니다.
:::
::: Mac 플랫폼
1. QtCreator를 열고 Qt Widgets Application 프로젝트를 선택하고 TestApp 프로젝트를 생성합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6c90f6f6916843a3360bbc7c3ea3fc67.png" width="600">
2. 프로세스 시작 프로그램을 작성하고 적절한 위치에서 LoadRoomApp 함수를 호출합니다.
```C++
#include <QProcess>
#include <QApplication>
void LoadRoomApp() {
    QString executable_file_path = QApplication::applicationDirPath();
    QString app_path = executable_file_path + "/../../../RoomApp.app/Contents/MacOS/RoomApp";
    QProcess::startDetached(app_path);
}
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/0fd090fbeef17d75a9b119b1a7e4fc9b.png" width="600">

3. 프로젝트를 컴파일하고 RoomApp 컴파일 결과 `RoomApp.app`을 현재 프로젝트의 출력과 동일한 수준으로 복사합니다. 여기서는 상기 이미지에서 생성한 프로젝트의 경로를 예로 들어 설명합니다.
`RoomApp.app`을 `/Users/mac/Desktop/TestApp/build-TestApp-Desktop_Qt_5_9_1_clang_64bit-Release` 디렉터리에 복사합니다.
4. TestApp과 RoomApp을 동시에 시작하는 프로그램을 실행합니다.
:::
</dx-tabs>


### 나만의 UI 커스터마이징[](id:ui)
- 우리가 제공하는 App을 수정하고 필요에 맞게 조정할 수 있습니다. 또한 App 소스 코드에서 Module 모듈을 사용하여 고유한 UI를 사용자 정의할 수 있습니다.
- 소스 코드의 Module 모듈은 TRTC 및 IM SDK를 캡슐화합니다. `TUIRoomCore.h`, `TUIRoomCoreCallback.h` 및 `TUIRoomDef.h` 파일에서 이 모듈에서 제공하는 API 기능 및 기타 정의를 보고 해당 API를 사용하여 고유한 사용자 정의 UI를 구현할 수 있습니다.
- App 디렉터리에는 UI 디자인과 로직이 포함되어 있습니다. 2차 개발을 위해 RoomApp 소스 코드를 수정할 수 있습니다. 주요 기능은 다음과 같습니다.
<table>
<thead>
<tr>
<th>특징</th>
<th>파일 디렉터리</th>
</tr>
</thead>
<tbody><tr>
<td>홈페이지 로그인</td>
<td>Windows-Mac\RoomApp\App\LoginViewController.cpp</td>
</tr>
<tr>
<td>디바이스 테스트</td>
<td>Windows-Mac\RoomApp\App\PresetDeviceController.cpp</td>
</tr>
<tr>
<td>메인 UI</td>
<td>Windows-Mac\RoomApp\App\MainWindow.cpp</td>
</tr>
<tr>
<td>발언자 목록</td>
<td>Windows-Mac\RoomApp\App\StageListController.cpp</td>
</tr>
<tr>
<td>구성원 리스트</td>
<td>Windows-Mac\RoomApp\App\MemberListViewController.cpp</td>
</tr>
<tr>
<td>설정 페이지</td>
<td>Windows-Mac\RoomApp\App\SettingViewController.cpp</td>
</tr>
<tr>
<td>채팅방</td>
<td>Windows-Mac\RoomApp\App\ChatRoomViewController.cpp</td>
</tr>
<tr>
<td>화면 공유</td>
<td>Windows-Mac\RoomApp\App\ScreenShareWindow.cpp</td>
</tr>
<tr>
<td>하단 툴바</td>
<td>Windows-Mac\RoomApp\App\BottomBarController.cpp</td>
</tr>
</tbody></table>

## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.

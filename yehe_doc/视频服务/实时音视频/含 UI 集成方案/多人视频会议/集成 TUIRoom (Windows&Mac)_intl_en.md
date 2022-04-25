This document describes the `TUIRoom` component for PC, an audio/video communication and collaboration tool with flexible layout and high adaptability. It can be used in various scenarios such as online collaboration, remote recruitment, remote diagnosis, insurance claim, online customer service, video interview, digital government services, finance digitization, online conferencing, and online education. It is integrated in depth with many industrial scenarios to help enterprises reduce costs, improve efficiency, and promote digitization for higher competitiveness.
You can download and install the application for [Windows](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe) or [macOS](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2) to try out the component.

## Demo UI
<table>
<tr><td><img src="https://qcloudimg.tencent-cloud.cn/raw/71f2649be2c654e1c5f217dc10e88efc.png" width="600" height="300"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9d927c98a595667d9f3f16d597abc77e.png" width="600" height="340"></td>
</tr></table>



## Solution Strengths
- `TUIRoom` integrates various capabilities such as ultra-low-latency audio/video call, chat room, screen sharing, beauty filter, device detection, and statistics, covering the common features of group audio/video room.
- It can be further developed as needed to quickly implement custom UI and layout, helping you quickly launch your business.
- It encapsulates the basic TRTC and IM SDKs to implement basic logic control and provides APIs for you to call features easily.

## Connection Guide
Two connection methods are recommended to help you quickly connect to the group audio/video room feature. You can select an appropriate method for secondary development.
- [Starting via external process](#start)
- [Customizing your own UI](#ui)

### Preparing the environment
- **Windows environment** :
	- Integrated development environment: Visual Studio 2015 or later.
	- Qt 5.9.1 or later.
	- Qt Visual Studio Tools 2.2.0 or later.
	- Operating system: Windows 8 or later.
	- Make sure that you can develop the project normally in the integrated development environment.
- **macOS environment**:
	- Qt 5.9.1 or later.
	- QtCreator integrated development environment. To use QtCreator, select it when installing Qt, and its version is the same as that of the Qt official installation package.
	- Make sure that you can develop the project normally in the QtCreator integrated development environment.

### Starting via external process[](id:start)
1. **Compile the RoomApp program**.
	- The method of using an external process to start RoomApp depends on the executable program of the original RoomApp, which needs to be compiled in advance.
	- Go to [RoomApp](https://github.com/tencentyun/TUIRoom), clone the source code, and configure the project to compile and generate RoomApp.
2. **Create the `TestApp` project**.
<dx-tabs>
::: Windows
1. Open Visual Studio, select the **Qt Widgets Application** project type, and create the `TestApp` project.
<img src="https://qcloudimg.tencent-cloud.cn/raw/45b191db25ad1a36eb2c10440f1790ce.png" width="600">
2. Write the process starting program and call the `LoadRoomApp` function at an appropriate position.
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

3. Compile the project and copy the RoomApp compilation result to the directory of the current executable program. Here, a `release x86` program is taken as an example:
Copy all files in the `TUIRoom\Windows-Mac\RoomApp\bin\Win32\Release` directory to the current program directory.
4. Run the program to start TestApp and RoomApp at the same time.
:::
::: macOS
1. Open QtCreator, select the **Qt Widgets Application** project, and create the `TestApp` project.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6c90f6f6916843a3360bbc7c3ea3fc67.png" width="600">
2. Write the process starting program and call the `LoadRoomApp` function at an appropriate position.
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

3. Compile the project and copy the RoomApp compilation result `RoomApp.app` to the same level as the output of the current project. Here, the path of the project created in the above figure is taken as an example:
Copy `RoomApp.app` to the `/Users/mac/Desktop/TestApp/build-TestApp-Desktop_Qt_5_9_1_clang_64bit-Release` directory.
4. Run the program to start TestApp and RoomApp at the same time.
:::
</dx-tabs>


### Customizing your own UI[](id:ui)
- You can modify the application we provide and adapt it to your needs. You can also use the `Module` module in the application source code to customize your own UI.
- The `Module` module in the source code encapsulates the TRTC and IM SDKs. You can view the API functions and other definitions provided by this module in `TUIRoomCore.h`, `TUIRoomCoreCallback.h`, and `TUIRoomDef.h` files and use the corresponding APIs to implement your own custom UI.
- The `App` directory contains UI design and logic. You can modify the RoomApp source code for secondary development. The main features are described below:
<table>
<thead>
<tr>
<th>Feature</th>
<th>File Directory</th>
</tr>
</thead>
<tbody><tr>
<td>Homepage login</td>
<td>Windows-Mac\RoomApp\App\LoginViewController.cpp</td>
</tr>
<tr>
<td>Device testing</td>
<td>Windows-Mac\RoomApp\App\PresetDeviceController.cpp</td>
</tr>
<tr>
<td>Main UI</td>
<td>Windows-Mac\RoomApp\App\MainWindow.cpp</td>
</tr>
<tr>
<td>Speaker list</td>
<td>Windows-Mac\RoomApp\App\StageListController.cpp</td>
</tr>
<tr>
<td>Member list</td>
<td>Windows-Mac\RoomApp\App\MemberListViewController.cpp</td>
</tr>
<tr>
<td>Settings page</td>
<td>Windows-Mac\RoomApp\App\SettingViewController.cpp</td>
</tr>
<tr>
<td>Chat room</td>
<td>Windows-Mac\RoomApp\App\ChatRoomViewController.cpp</td>
</tr>
<tr>
<td>Screen sharing</td>
<td>Windows-Mac\RoomApp\App\ScreenShareWindow.cpp</td>
</tr>
<tr>
<td>Bottom toolbar</td>
<td>Windows-Mac\RoomApp\App\BottomBarController.cpp</td>
</tr>
</tbody></table>

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.

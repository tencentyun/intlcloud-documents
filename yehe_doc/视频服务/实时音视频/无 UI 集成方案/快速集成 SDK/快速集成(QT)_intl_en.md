This document describes how to quickly integrate the TRTC Windows or macOS SDK into your project using Qt.

## Integration for Windows
### Environment Requirements
- OS: Windows 7 or later
- Development environment: Visual Studio 2015 or later (you need to set up a Qt development environment). Visual Studio 2015 is recommended.
>? If you are not sure about how to set up a Qt development environment in Visual Studio, see step 4 in [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md).

### Directions
This section uses a simple QtTest project as an example to show you how to integrate the TRTC C++ SDK into your Visual Studio project.

1. **Download the cross-platform C++ SDK**[](id:win_step1)
	1. Download the latest version of the [TRTC SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip). Decompress and open the file.
	2. Create an empty folder for the SDK in the same directory as your QtTest project, and copy `TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus` to the folder.
2. **Configure the dependent environment for the QtTest project**[](id:win_step2)
<dx-tabs>
::: Case 1: Using Qt Creator
Go to the directory of the QtTest project, open `QTTest.pro` (created using Qt Creator) with a text editor ([Sublime Text](http://www.sublimetext.com/3) is recommended), and add the following SDK references.
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
	} else{
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}

release {
	contains(QT_ARCH,i386) {
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win32/lib -lliteav
	} else{
		LIBS += -L$$PWD/../SDK/CPlusPlus/Win64/lib -lliteav
	}
}
:::
</dx-codeblock>
:::
::: Case 2: Using Visual Studio
If you already have a mature Visual Studio project, follow the steps below to configure the environment:
1. On the project’s property page, go to **Linker** > **Input** and add `liteav.lib` to **Additional Dependencies**.
2. Go to **Linker** > **General** and add the path of the SDK library to **Additional Library Directories**. For example, for 64-bit Windows, add `$(ProjectDir)SDK\CPlusPlus\Win64\lib`.
3. Go to **C/C++** > **General** and add `$(ProjectDir)SDK\CPlusPlus\Win64\include` and `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC` to **Additional Include Directories**.
>? For 32-bit Windows, change "Win64" in the paths to "Win32".
:::
</dx-tabs>
3. **Copy files**[](id:win_step3)
	- When you open `QTTest.pro` with Qt Creator to debug your project, a `debug/release` folder will be created automatically. You need to copy all the DLL files in `SDK/CPlusPlus/Win64/lib` or `SDK/CPlusPlus/Win32/lib` to the folder.
	- If you use Visual Studio to debug your project, copy all the DLL files in `SDK/CPlusPlus/Win64/lib` to the output directory of your project, or go to **Build Events** > **Post-build Events** and add the copy command `copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)` to **Command Line**.
>? For 32-bit Windows, add `copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)`.
4. **Reference the TRTC SDK**[](id:win_step4)
	- Reference the SDK via the header file: `#include "ITRTCCloud.h"`.
	- Use the namespace: The methods and types of cross-platform C++ APIs are all defined in the `trtc` namespace. To simplify your code, we recommend you use the `trtc` namespace.

>? This concludes the integration process, and you can proceed to compile your project. You can download [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows). to get more information on the use of cross-platform APIs of the SDK.

## Integration for macOS
### Environment Requirements

- OS: OS X 10.10 or later
- Development environment: Qt Creator 4.10.3 or later (Qt Creator 4.13.3 or later is recommended.)
- Development framework: Qt 5.10 or later

### Directions
This section uses a QtTest project created from scratch as an example to show you how to integrate the TRTC C++ SDK into your project in Qt Creator.

[](id:mac_step1)
1. **Download the cross-platform C++ SDK**
	1. Download the [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2), and decompress and open the file.
	2. Create an empty folder for the SDK in the same directory as your QtTest project, and copy `TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework` to the folder.
2. **Configure QTTest.pro**[](id:mac_step2)
Go to the directory of your QtTest project, open `QTTest.pro` with a text editor, and add the following SDK references.
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

3. **Grant camera and mic permissions**[](id:mac_step3)
The TRTC SDK will use the device’s camera and mic, so you need to add permission requests to `Info.plist`.
```none
NSMicrophoneUsageDescription: requesting mic access
NSCameraUsageDescription: requesting camera access
```
As shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dc42db42bf51f14a8e22326edc3f0a16.png)

4. **Reference the TRTC SDK**[](id:mac_step4)
	- Reference the SDK via the header file: `#include "ITRTCCloud.h"`.
	- Use the namespace: The methods and types of cross-platform C++ APIs are all defined in the `trtc` namespace. To simplify your code, we recommend you use the `trtc` namespace.

>? This concludes the integration process, and you can proceed to compile your project. You can download [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac). to get more information on the use of cross-platform APIs of the SDK.

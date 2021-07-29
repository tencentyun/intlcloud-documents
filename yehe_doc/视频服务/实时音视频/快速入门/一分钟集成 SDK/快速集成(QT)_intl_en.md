This document describes how to quickly integrate the Tencent Cloud TRTC SDK into your project using Qt on macOS and Windows.

## Integration on macOS
### Environment Requirements

- OS: OS X 10.10 or above
- Development environment: Qt Creator 4.10.3 or above (Qt Creator 4.13.3 or above is recommended.)
- Development framework: Qt 5.10 or above

### Directions
This section uses a QtTest project created from scratch as an example to show you how to integrate TRTC SDK for C++ into your project in Qt Creator.

[](id:mac_step1)
#### Step 1. Download TRTC SDK for C++.
1. Download the [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Mac_latest.tar.bz2), and decompress and open the file.
2. Create an empty folder for the SDK in the directory of your QtTest project, and copy `TXLiteAVSDKTRTCMacx.x.x/SDK/TXLiteAVSDKTRTC_Mac.framework` from the package downloaded in step 1 to the folder.

[](id:mac_step2)
#### Step 2. Configure QtTest.pro.
Go to the directory of your QtTest project, open `QTTest.pro` with a text editor, and add the following SDK references.

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
#### Step 3. Request camera and mic permissions.

For the TRTC SDK to use your camera and mic, you need to add permission requests to `Info.plist`.
```none
NSMicrophoneUsageDescription: requesting mic access
NSCameraUsageDescription: requesting camera access
```
This is how your project looks like after the adding of permission requests:

[](id:mac_step4)
#### Step 4. Reference the SDK.
1. Reference the SDK using the header file `#include "ITRTCCloud.h"`.
2. Use the namespace: the methods and types of cross-platform C++ APIs are defined in the `trtc` namespace. To simplify your code, you are advised to use the `trtc` namespace.

>? This concludes the integration process, and you can proceed to compile your project. You can download [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Mac). to get more information on the use of cross-platform APIs of the SDK.

## Integration on Windows
### Environment Requirements
- OS: Windows 7 or above
- Development environment: Visual Studio 2015 or above. Visual Studio 2015 is recommended, provided that you have set up a Qt development environment for Visual Studio.
>? If you are not sure about how to set up a Qt development environment for Visual Studio, see the second part of [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md).

### Directions
This section uses a simple QtTest project as an example to show you how to integrate TRTC SDK for C++ into your Visual Studio project.

[](id:win_step1)
#### Step 1. Download TRTC SDK for C++.
1. Download the [SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip), and decompress and open the file.
2. Create an empty folder for the SDK in the directory of your QtTest project, and copy `TXLiteAVSDKTRTCWin_latest/SDK/CPlusPlus` from the package downloaded in step 1 to the folder.

[](id:win_step2)
#### Step 2. Configure dependent environment for the QtTest project.
##### Scenario 1: using Qt Creator
Go to the directory of the QtTest project, open `QTTest.pro` (created using Qt Creator) with a text editor ([Sublime Text](http://www.sublimetext.com/3) is recommended), and add the following SDK references.
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
##### Scenario 2: using Visual Studio
If your project is a full-fledged Visual Studio project, you can also configure the SDK library path dependency in Visual Studio in **Properties > Linker > Input and General**, and configure the SDK header file path dependency in **Properties >C/C++ > General**.

[](id:win_step3)
### Step 3. Copy files.
When you open `QTTest.pro` with Visual Studio, a `debug/release` folder will be generated automatically in the project directory. You need to copy all the DLL files in `SDK/CPlusPlus/Win32/lib` to the `debug/release` folder.

[](id:win_step4)
#### Step 4. Reference the SDK.
1. Reference the SDK using the header file `#include "ITRTCCloud.h"`.
2. Use the namespace: the methods and types of cross-platform C++ APIs are defined in the `trtc` namespace. To simplify your code, you are advised to use the `trtc` namespace.

>? This concludes the integration process, and you can proceed to compile your project. You can download [QTDemo](https://github.com/tencentyun/TRTCSDK/tree/master/Windows). to get more information on the use of cross-platform APIs of the SDK.

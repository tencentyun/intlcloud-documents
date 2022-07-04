This document describes how to quickly integrate the TRTC Windows or macOS SDK into your project using Qt.

![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)

## Integration for Windows
### Environment requirements
- OS: Windows 7 or later
- Development environment: Visual Studio 2015 or later (you need to set up a Qt development environment). Visual Studio 2015 is recommended.
>? If you are not sure how to set up a Qt development environment in Visual Studio, see step 4 in [README](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/QTDemo/README.md).

### Directions
The following describes how to integrate the TRTC Windows C++ SDK into a Qt project in Visual Studio.

### Step 1. Download the SDK
1. Download the latest version of the [TRTC SDK](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Win_latest.zip).
You only need to import the SDK files for Windows C++ in the `SDK` folder. For example, you can find the SDK files for 64-bit Windows in `./SDK/CPlusPlus/Win64/`. The folder contains the following files:
<table>
<thead>
<tr>
<th>Directory</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>include</td>
<td>API header files with comments</td>
</tr>
<tr>
<td>lib</td>
<td>The LIB file for compilation and DLL files to load</td>
</tr>
</tbody></table>

### Step 2. Create a project[](id:using_cpp_qt_step2)
Take Visual Studio 2015 for example. Make sure you have installed [Qt](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe) and [Qt Visual Studio Add-in](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix). Then, open Visual Studio and create a Qt application named `TRTCDemo`.
![](https://qcloudimg.tencent-cloud.cn/raw/fa665d6c78420db0da022ae81f2d7c68.png)
For the example in this guide, **Qt Widgets Application** is chosen. Click **Add**, and then click **Next** in subsequent steps until the project is created.

### Step 3. Copy and paste files[](id:using_cpp_qt_step3)
Copy the `SDK` folder to the directory where `TRTCDemo.vcxproj` is located.
>? Because you will only need the C++ SDK, you can delete the `CSharp` folder in `SDK`.

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

### Step 4. Modify project configuration[](id:using_cpp_qt_step4)
Select **Solution Explorer**, right-click `TRTCDemo`, and select **Properties**. Configure the project as follows:
1. **Add include directories.**
Go to **C/C++** > **General**. Add the `$(ProjectDir)SDK\CPlusPlus\Win64\include` and `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC` header file directories (for 64-bit Windows) to **Additional Include Directories**.
>? For 32-bit Windows, add `$(ProjectDir)SDK\CPlusPlus\Win32\include` and `$(ProjectDir)SDK\CPlusPlus\Win32\include\TRTC`.

![](https://qcloudimg.tencent-cloud.cn/raw/61a49b758ecb52ab6ee576421da5800d.png)
2. **Add additional library directories**
Go to **Linker** > **General**. Add the `$(ProjectDir)SDK\CPlusPlus\Win64\lib` directory (for 64-bit Windows) to ** Additional Library Directories**.
>? For 32-bit Windows, add `$(ProjectDir)SDK\CPlusPlus\Win32\lib`.

![](https://qcloudimg.tencent-cloud.cn/raw/89b465c893f456edacf3355dc59f0258.png)
3. **Add the library file**
Go to **Linker** > **Input**, and add the library file `liteav.lib` to **Additional Dependencies**.
![](https://qcloudimg.tencent-cloud.cn/raw/7eb6bbe2351dc4cd3e6c7ae817042fae.png)
4. **Add the copy command**
Go to **Build Events** > **Post-build Events** and add the copy command `copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)` (for 64-bit Windows) to **Command Line**. This ensures that the DLL files of the SDK are automatically copied to the project's execution directory after compilation.
>? For 32-bit Windows, add `copy /Y $(ProjectDir)SDK\CPlusPlus\Win32\lib\*.dll  $(OutDir)`.

![](https://qcloudimg.tencent-cloud.cn/raw/c6cb6d0dfd935be7a74313881a306c5f.png)

### Step 5. Print the SDK version number[](id:using_cpp_qt_step5)
1. At the top of the `TRTCDemo.cpp` file, add the code below to import the header file:
``` c++
#include "ITRTCCloud.h"
#include <QLabel>
```
2. In the `TRTCDemo::TRTCDemo` constructor of `TRTCDemo.cpp`, add the following testing code:
```C++
ITRTCCloud * pTRTCCloud = getTRTCShareInstance();
std::string version(pTRTCCloud->getSDKVersion());

QString sdk_version = QString("SDK Version: %1").arg(version.c_str());
QLabel* label_text = new QLabel(this);
label_text->setAlignment(Qt::AlignCenter);
label_text->resize(this->width(), this->height());
label_text->setText(sdk_version);
```
3. Press F5 to run the project and print the version number of the SDK.  
![](https://qcloudimg.tencent-cloud.cn/raw/bc1ddf818e5f0571c72d34ba212691c7.png)



## Integration for macOS
### Environment requirements

- OS: OS X 10.10 or later
- Development environment: Qt Creator 4.10.3 or later (Qt Creator 4.13.3 or later is recommended.)
- Development framework: Qt 5.10 or later

### Directions
This section uses a QtTest project as an example to show you how to integrate the TRTC C++ SDK into your project in Qt Creator.

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
The TRTC SDK will use the device's camera and mic, so you need to add permission requests to `Info.plist`.
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

## FAQs
- If the following error occurs, check whether the SDK header file directories are correctly added as described in the project configuration step above.
```
fatal error C1083: Could not open include file: "TRTCCloud.h": No such file or directory
```

- If the following error occurs, check whether the SDK library directory and library file are correctly added as described in the project configuration step above.
```
error LNK2019: unresolved external symbol "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ), referenced in function "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ)
```
This document describes how to quickly integrate the TRTC Windows C++ SDK using a Qt project.

## Environment Requirements
- OS: Windows 7 or later
- Development environment: Visual Studio 2010 or later (v2015 is recommended)
- [Qt](https://download.qt.io/archive/qt/5.9/5.9.1/qt-opensource-windows-x86-5.9.1.exe) and [Qt Visual Studio Add-in](https://download.qt.io/archive/vsaddin/2.6.0/qt-vsaddin-msvc2015-2.6.0.vsix)

[](id:using_cpp)
## Integrating the C++ SDK via a Qt Project
The following describes how to integrate the TRTC Windows C++ SDK into a Qt project in Visual Studio.

[](id:using_cpp_qt_step1)
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
For the example in this guide, we will choose **Qt Widgets Application**. Click **Add**, and then click **Next** in subsequent steps until the project is created.

### Step 3. Copy and paste files[](id:using_cpp_qt_step3)
Copy the `SDK` folder to the directory where `TRTCDemo.vcxproj` is located.
>? Because you will only need the C++ SDK, you can delete the `CSharp` folder in `SDK`.

![](https://qcloudimg.tencent-cloud.cn/raw/49681d526061bdef063e878879d471a8.png)

### Step 4. Modify project configuration[](id:using_cpp_qt_step4)
Select **Solution Explorer**, right-click `TRTCDemo`, and select **Properties**. Configure the project as follows:
1. **Add include directories.**
Go **C/C++** > **General**. Add the `$(ProjectDir)SDK\CPlusPlus\Win64\include` and `$(ProjectDir)SDK\CPlusPlus\Win64\include\TRTC` header file directories (for 64-bit Windows) to **Additional Include Directories**.
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
Go to **Build Events** > **Post-build Events** and add the copy command `copy /Y $(ProjectDir)SDK\CPlusPlus\Win64\lib\*.dll  $(OutDir)` (for 64-bit Windows) to **Command Line**. This ensures that the DLL files of the SDK are automatically copied to the project’s execution directory after compilation.
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

## FAQs
- If the following error occurs, check whether the SDK header file directories are correctly added as described in the project configuration step above.
```
fatal error C1083: Could not open include file: “TRTCCloud.h”: No such file or directory
```

- If the following error occurs, check whether the SDK library directory and library file are correctly added as described in the project configuration step above.
```
error LNK2019: unresolved external symbol "__declspec(dllimport) public: static class TXString __cdecl TRTCCloud::getSDKVersion(void)" (__imp_?getSDKVersion@TRTCCloud@@SA?AVTXString@@XZ), referenced in function "protected: virtual int __thiscall CTRTCDemoDlg::OnInitDialog(void)" (?OnInitDialog@CTRTCDemoDlg@@MAEHXZ)
```

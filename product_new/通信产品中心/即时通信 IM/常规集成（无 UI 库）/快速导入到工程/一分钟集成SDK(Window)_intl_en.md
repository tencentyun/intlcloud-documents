This document describes how to quickly integrate the Tencent Cloud IM SDK into your projects. Follow these steps to integrate the SDK easily.

## Development Environment Requirements
- Operating system: Windows 7 or later
- Development environment: Visual Studio 2010 or later. Visual Studio 2015 is recommended.

## Integrating the IM SDK
The following section describes how to integrate the SDK into a Visual Studio 2015 project by creating a simple MFC project.

### Step 1. Download the IM SDK

Download the Windows IM SDK from [Github](https://github.com/tencentyun/TIMSDK), as shown below:
 ![](https://main.qcloudimg.com/raw/22f0841537a6314fa7e00581d84a07de.png)

Download and decompress the IM SDK file, which contains the following:

| Directory Name | Description |
| ------------ | ------------------------------------------------ |
| includes | API header files |
| lib\Win32\Debug | **32-bit Debug mode**, with .lib static library files and .dll dynamic library files compiled with /MTd |
| lib\Win32\Release | **32-bit Release mode**, with .lib static library files and .dll dynamic library files compiled with /MT |
| lib\Win64\Debug | **64-bit Debug mode**, with .lib static library files and .dll dynamic library files compiled with /MTd |
| lib\Win64\Release | **64-bit Release mode**, with .lib static library files and .dll dynamic library files compiled with /MT |


### Step 2. Create a project
Open Visual Studio and create an MFC application named IMDemo, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0968bf8f93c69212760bd4651839d29f.png)

For quick integration, on the **Application Type** page of the wizard, select the simple **Dialog-based** type. Do not change the defaults of other wizard configuration items, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8a6372d71853148fe6a6c5073f1512b3.png)


### Step 3. Copy files
Decompress and copy the IM SDK file to the directory where IMDemo.vcxproj is located:
![](https://main.qcloudimg.com/raw/4b13837ffc2662cea6a09f7a6fa5bda4.png)

### Step 4. Modify the project configuration

The IM SDK provides two compiled static libraries, **Debug** and **Release**, which require some special configurations. To do this, go to the IMDemo property page by choosing **Solution Resource Manager** > **right-click menu of the IMDemo project** > **Properties**.

By using **32-bit Debug mode** as an example, configure the project as follows:

1. Add the inclusion directory
  Navigate to **C/C++** > **General** > **Additional Inclusion Directories**, and add the IM SDK header file directory $(ProjectDir)ImSDK\includes, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/7b3dddadf6d3993ab3f83522e7e1f869.png)
2. Add the library directory
  Navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win32\Debug. 
  ![](https://main.qcloudimg.com/raw/57929e1a13b50d9f0c3e9af7c54edf83.png)
3. Add the library file
  Navigate to **Linker** > **Input** > **Additional Dependencies**, add the IM SDK library file imsdk.lib, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/e4e180c8867bb4ad6e7fa09f69c2ff0e.png)
4. Copy the DLL file to the execution directory
  Navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and then run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Debug" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/621b9fe04315985a274316b5215c944d.png)
5. Specify the encoding format of the source file
  The IM SDK header file uses the UTF-8 encoding format, whereas some compilers compile source files in the default system encoding format. This may incur compilation failure. Set this parameter to instruct compilers to compile source files by using UTF-8 encoding.
  Navigate to **C/C++** > **Command Line** > **Additional Options**, and enter `/source-charset:.65001`, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/0c9ab7746d643594fa7cf20e93c60860.png)

The **Release mode** is configured as follows:
1. Add the library directory
  Navigate to **Linker** > **General** > **Additional Library Directory**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win32\Release, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/c393f464e5d74825eeeb9630b7d2e8eb.png)
2. Copy the DLL file to the execution directory 
  Navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Release" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/c48481f2b7ae9a2d87fb405167e097d4.png)


The settings for **64-bit Debug/Release** and **32-bit** are similar, but their library directories of the IM SDK are different, as shown below:
1. Add the library directory
  - For the **Debug mode**: navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win64\Debug, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/2099cc0be32fdc78e066ad370bc0f931.png)
   - For the **Release mode**: navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win64\Release, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/b6a07c37033f9a6a19ceac0569b7d301.png)
2. Copy the DLL file to the execution directory
  - For the **Debug mode**: navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Debug" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/68f3986dbc865a863487cacfa91b2b67.png)
 - For the **Release mode**: navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Release" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory, as shown in the following figure:
  ![](https://main.qcloudimg.com/raw/f75a203a1e576102ea01391d39995bec.png)


### Step 5. Print the IM SDK version number

- In the IMDemo.cpp file, add the inclusion header file:
```c++
#include "TIMCloud.h"
```

- In the CIMDemoDlg::OnInitDialog function, add the following test code:
```c++
std::string version = TIMGetSDKVersion();
CString szText;
szText.Format(L"SDK version: %hs", version.c_str());
CWnd* pStatic = GetDlgItem(IDC_STATIC);
pStatic->SetWindowTextW(szText);
```

- Press F5 to run the code and print the IM SDK version number, as shown in the following figure:
![](https://main.qcloudimg.com/raw/b045866bba49344cc587cc3e406b6024.png)

# FAQs

- If the following error occurs, check whether the directory of the IM SDK header file has been correctly added according to the preceding project configuration:
```
fatal error C1083: failed to open the inclusion file: “TIMCloud.h”: No such file or directory
```

- If the following error occurs, check whether the IM SDK library directory and library file have been correctly added according to the preceding project configuration:
```
LINK : fatal error LNK1104: failed to open the file "imsdk.lib"
```
```
error LNK2019: failed to parse the external symbol __imp__TIMGetSDKVersion, this symbol is referenced in "protected: virtual int __thiscall CIMDemoDlg::OnInitDialog(void)" (?OnInitDialog@CIMDemoDlg@@MAEHXZ)
```

- If the following error occurs, check whether the DLL file of the IM SDK has been copied to the execution directory according to the preceding project configuration:
![](https://main.qcloudimg.com/raw/5d829626978836db0ac9cc1937f7fc27.png)

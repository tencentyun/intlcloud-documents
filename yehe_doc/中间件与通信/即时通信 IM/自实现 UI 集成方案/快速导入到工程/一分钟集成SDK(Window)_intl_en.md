This document describes how to quickly integrate the Tencent Cloud IM SDK into your projects. Follow these steps to integrate the SDK easily.

## Development Environment Requirements
- Operating system: Windows 7 or later
- Development environment: Visual Studio 2010 or later. Visual Studio 2015 is recommended.

## Integrating the IM SDK
The following section describes how to integrate the SDK into a Visual Studio 2015 project by creating a simple MFC project.

### Step 1. Download the IM SDK

Download the Windows IM SDK from [Github](https://github.com/tencentyun/TIMSDK).

Download and decompress the IM SDK file, which contains the following:

| Directory Name | Description |
| ------------ | ------------------------------------------------ |
| includes | API header files |
| lib\Win32\Debug | **32-bit Debug mode**, with .lib static library files and .dll dynamic library files compiled with /MTd |
| lib\Win32\Release | **32-bit Release mode**, with .lib static library files and .dll dynamic library files compiled with /MT |
| lib\Win64\Debug | **64-bit Debug mode**, with .lib static library files and .dll dynamic library files compiled with /MTd |
| lib\Win64\Release | **64-bit Release mode**, with .lib static library files and .dll dynamic library files compiled with /MT |


### Step 2. Create a project
Open Visual Studio and create an MFC application named IMDemo.

For quick integration, on the **Application Type** page of the wizard, select the simple **Dialog-based** type. Do not change the defaults of other wizard configuration items.


### Step 3. Copy files
Decompress and copy the IM SDK file to the directory where IMDemo.vcxproj is located:


### Step 4. Modify the project configuration

The IM SDK provides two compiled static libraries, **Debug** and **Release**, which require some special configurations. To do this, go to the IMDemo property page by choosing **Solution Resource Manager** > **right-click menu of the IMDemo project** > **Properties**.

By using **32-bit Debug mode** as an example, configure the project as follows:

1. Add the inclusion directory
  Navigate to **C/C++** > **General** > **Additional Inclusion Directories**, and add the IM SDK header file directory $(ProjectDir)ImSDK\includes.
2. Add the library directory
  Navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win32\Debug. 

3. Add the library file
  Navigate to **Linker** > **Input** > **Additional Dependencies**, add the IM SDK library file imsdk.lib.
4. Copy the DLL file to the execution directory
  Navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and then run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Debug" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory.
5. Specify the encoding format of the source file
  The IM SDK header file uses the UTF-8 encoding format, whereas some compilers compile source files in the default system encoding format. This may incur compilation failure. Set this parameter to instruct compilers to compile source files by using UTF-8 encoding.
  Navigate to **C/C++** > **Command Line** > **Additional Options**, and enter `/source-charset:.65001`.

The **Release mode** is configured as follows:
1. Add the library directory
  Navigate to **Linker** > **General** > **Additional Library Directory**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win32\Release.
2. Copy the DLL file to the execution directory 
  Navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Release" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory.


The settings for **64-bit Debug/Release** and **32-bit** are similar, but their library directories of the IM SDK are different, as shown below:
1. Add the library directory
  - For the **Debug mode**: navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win64\Debug.
   - For the **Release mode**: navigate to **Linker** > **General** > **Additional Library Directories**, and add the IM SDK library directory $(ProjectDir)ImSDK\lib\Win64\Release.
2. Copy the DLL file to the execution directory
  - For the **Debug mode**: navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Debug" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory.
 - For the **Release mode**: navigate to **Build Events** > **Pre-Built Events** > **Command Line**, and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Release" "$(OutDir)"` to copy the dynamic library file imsdk.dll to the application generation directory.


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

- Press F5 to run the code and print the IM SDK version number.

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


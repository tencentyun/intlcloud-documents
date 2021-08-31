This document describes how to quickly integrate the Tencent Cloud IM SDK into your projects. Follow these steps to integrate the SDK easily.

## Development Environment Requirements
- Operating system: Windows 7 or above.
- Development environment: Visual Studio 2010 or above. Visual Studio 2015 is recommended.

## Integrating the IM SDK
The following describes how to integrate the SDK into a Visual Studio 2015 project by creating a simple MFC project.

### Step 1. Download the IM SDK

Download the Windows IM SDK from [GitHub](https://github.com/tencentyun/TIMSDK).

Download and decompress the IM SDK file folder, which contains the following:

| Directory Name       | Description                                             |
| ------------ | ------------------------------------------------ |
| includes     | API header files                                     |
| lib\Win32\Debug   | **32-bit Debug mode**, using /MTd to link to library files |
| lib\Win32\Release | **32-bit Release mode**, using /MT to link to library files |
| lib\Win64\Debug   | **64-bit Debug mode**, using /MTd to link to library files |
| lib\Win64\Release | **64-bit Release mode**, using /MT to link to library files |


### Step 2. Create a project
Open Visual Studio and create an MFC application named IMDemo.

For quick integration, on the **Application Type** page of the wizard, select the simple **Dialog-based type**. Do not change the defaults of other configuration items.


### Step 3. Copy files
Copy the IM SDK files to the directory where `IMDemo.vcxproj` is located.

### Step 4. Modify the project configuration

The IM SDK provides two compiled static libraries, **Debug** and **Release**, which require some special configurations. To do this, go to the IMDemo property page by clicking **Solution Resource Manager** > **Right-Click Menu of the IMDemo Project** > **Properties**.

Using **32-bit Debug mode** as an example, configure the project as follows:

1. Add the inclusion directory
    In **C/C++** > **General** > **Additional Inclusion Directories**, add the IM SDK header file directory `$(ProjectDir)ImSDK\includes`.
2. Add the library directory
    In **Linker** > **General** > **Additional Library Directories**, add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win32\Debug`. 
3. Add the library file
    In **Linker** > **Input** > **Additional Dependencies**, add the IM SDK library file `imsdk.lib`.
4. Copy the DLL file to the execution directory
    In **Build Events** > **Pre-Built Events** > **Command Line**, enter and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Debug" "$(OutDir)"` to copy the dynamic library file `imsdk.dll` to the application generation directory.
5. Specify the encoding format of the source file
    The IM SDK header file uses the UTF-8 encoding format, whereas some compilers compile source files in the default system encoding format. This may lead to compilation failure. Set this parameter to instruct compilers to compile source files using UTF-8 encoding.
    In **C/C++** > **Command Line** > **Additional Options**, enter `/source-charset:.65001`.

Configure the **Release mode** as follows:
1. Add the library directory
    In **Linker** > **General** > **Additional Library Directories**, add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win32\Release`.
2. Copy the DLL file to the execution directory 
    In **Build Events** > **Pre-Built Events** > **Command Line**, enter and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32\Release" "$(OutDir)"` to copy the dynamic library file `imsdk.dll` to the application generation directory.


The settings for **64-bit Debug/Release** and **32-bit** are similar, but their library directories of the IM SDK are different, as shown below:
1. Add the library directory
  - For the **Debug mode**: in **Linker** > **General** > **Additional Library Directories**, add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win64\Debug`.
   - For the **Release mode**: in **Linker** > **General** > **Additional Library Directories**, add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win64\Release`.
2. Copy the DLL file to the execution directory
  - For the **Debug mode**: in **Build Events** > **Pre-Built Events** > **Command Line**, enter and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Debug" "$(OutDir)"` to copy the dynamic library file `imsdk.dll` to the application generation directory.
 - For the **Release mode**: in **Build Events** > **Pre-Built Events** > **Command Line**, enter and run `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64\Release" "$(OutDir)"` to copy the dynamic library file `imsdk.dll` to the application generation directory.


### Step 5. Print the IM SDK version number

- In the file `IMDemo.cpp`, add the header file:
```c++
#include "TIMCloud.h"
```

- In the function `CIMDemoDlg::OnInitDialog`, add the following test code:
```c++
std::string version = TIMGetSDKVersion();
CString szText;
szText.Format(L"SDK version: %hs", version.c_str());
CWnd* pStatic = GetDlgItem(IDC_STATIC);
pStatic->SetWindowTextW(szText);
```

- Press **F5** to run the code and print the IM SDK version number.

## FAQs

- If the following error occurs, check whether the directory of the IM SDK header file has been correctly added according to the preceding project configuration:
```
fatal error C1083: unable to open the header file: "TIMCloud.h": No such file or directory
```

- If the following error occurs, check whether the IM SDK library directory and library file have been correctly added according to the preceding project configuration:
```
LINK : fatal error LNK1104: unable to open the file "imsdk.lib"
```
```
error LNK2019: unable to parse the external symbol `__imp__TIMGetSDKVersion`; this symbol is referenced in `protected: virtual int __thiscall CIMDemoDlg::OnInitDialog(void)" (?OnInitDialog@CIMDemoDlg@@MAEHXZ)`
```

- If the following error occurs, check whether the DLL file of the IM SDK has been copied to the execution directory according to the preceding project configuration.



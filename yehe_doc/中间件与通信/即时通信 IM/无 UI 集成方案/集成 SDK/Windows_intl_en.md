- This document describes how to quickly integrate the Tencent Cloud IM SDK into your Windows project.

  ## Environment Requirements
  - Operating system: Windows 7 or later.
  - Development environment: Visual Studio 2010 or later. Visual Studio 2019 is recommended.

  ## Integrating the IM SDK
  The following describes how to integrate the SDK into a Visual Studio 2019 project by creating a simple MFC project.
  [](id:step1)
  ### Step 1. Download the IM SDK
  Download the IM SDK for Windows [here](https://github.com/TencentCloud/TIMSDK/tree/master/Windows/IMSDK) as follows:
  ![](https://qcloudimg.tencent-cloud.cn/raw/8381932e86c2ff5cfe448685f16cc495.png)

  Download and decompress the IM SDK. You can rename it "ImSDK". It contains the following parts:

  | Directory Name | Description                                                  |
  | -------------- | ------------------------------------------------------------ |
  | include        | API header file                                              |
  | lib\Win32      | **32-bit Release mode**, which uses the /MT option to link library files. |
  | lib\Win64      | **64-bit Release mode**, which uses the /MT option to link library files. |


  ### Step 2. Create a project
  Open Visual Studio and create an MFC application named "IMDemo". If the MFC application is not one of the first options, you can search for it through the search template at the top.

  For quick integration, select the relatively simple **Dialog-based** type on the **Application Type** page of the wizard. For other configuration items, keep them as default.


  ### Step 3. Copy the files
  Copy the IM SDK folder generated after decompression (the "ImSDK" folder obtained in [step 1](#step1)) to the directory where `IMDemo.vcxproj` is located.

  ### Step 4. Modify the project configuration

  The IM SDK provides 32-bit and 64-bit static libraries in **Release** mode, which require some special configurations. Open the IMDemo attribute page, select **Solution Explorer**, right-click `IMDemo`, and select **Properties**.

  The following takes the **32-bit Release mode** as an example:

  1. Add the include directory.
      Go to **C/C++** > **General** > **Additional Include Directories** and add the IM SDK header file directory `$(ProjectDir)ImSDK\include`.
  2. Add the library directory.
      Go to **Linker** > **General** > **Additional Library Directories** and add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win32`.
  3. Add the library file.
      Go to **Linker** > **Input** > **Additional Dependencies** and add the IM SDK library file `ImSDK.lib`.

  4. Copy the DLL file to the execution directory.
      Go to **Build Events** > **Pre-Build Event** > **Command Line**, enter `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win32" "$(OutDir)"`, and copy the `ImSDK.dll` dynamic library file to the output directory of the project.
  5. Specify the encoding format of the source file.
      The IM SDK header file uses the UTF-8 encoding format, whereas some compilers compile source files in the default system encoding format. This may lead to compilation failure. Set this parameter to instruct compilers to compile source files using UTF-8 encoding.
      Go to **C/C++** > **Command Line** > **Additional Options** and enter `/source-charset:.65001`.


  Most of the settings for the **64-bit Release** are similar to those for the **32-bit Release**. The difference lies in the IM SDK library directory as follows:
  1. Add the library directory.
    - Go to **Linker** > **General** > **Additional Library Directories** and add the IM SDK library directory `$(ProjectDir)ImSDK\lib\Win64`.
  2. Copy the DLL file to the execution directory.
   - In **Release mode**, go to **Build Events** > **Pre-Build Event** > **Command Line**, enter `xcopy /E /Y "$(ProjectDir)ImSDK\lib\Win64" "$(OutDir)"`, and copy the `ImSDK.dll` dynamic library file to the output directory of the project.

  

  ### Step 5. Print the IM SDK version number

  - In the `IMDemoDlg.cpp` file, add the header file inclusion:
  ```c++
  #include "TIMCloud.h"
  #include <string>
  ```

  - In the `IMDemoDlg.cpp` file, find the `CIMDemoDlg::OnInitDialog` function and add the following test code before `return`:
  ```c++
  SetWindowText(L"IMDemo");
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
  LINK : fatal error LNK1104: Unable to open the `ImSDK.lib` file.
  ```
  ```
  error LNK2019: Unresolved external symbol `__imp__TIMGetSDKVersion`, referenced in the `"protected: virtual int __thiscall CIMDemoDlg::OnInitDialog(void)" (?OnInitDialog@CIMDemoDlg@@MAEHXZ)` function
  ```

  - If an error occurs, check whether the IM SDK's DLL has been copied to the execution directory as described in the project configuration step above.

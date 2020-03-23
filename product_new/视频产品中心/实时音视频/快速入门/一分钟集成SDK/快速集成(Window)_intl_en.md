This document describes how to quickly integrate the Tencent Cloud TRTC SDK for C# on Windows into your project.

## Development Environment Requirements

- OS: Windows 7 or above.
- Development environment: Visual Studio 2010 or above (v2015 is recommended).
- Development framework: .Net Framework 4.0 or above.

## Integrating the TRTC SDK

This document uses the creation of a simple Winform project as an example to describe how to integrate the SDK for C# into a Visual Studio project.

### Step 1. Download the SDK for Windows

[Download the SDK](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip), decompress it, and open the files, including:

| Directory Name | Description |
| ------- | -------------------------------------- |
| xxxDemo | Source code of the demos for C++ and C# |
| CPlusPlus | SDK library file depended on by the 32/64-bit SDK for C++ |
| CSharp | SDK library file depended on by the 32/64-bit SDK for C# |

In the example in this document, you only need to import the C# version of the SDK files into the SDK directory.

### Step 2. Create a project

Open Visual Studio and create a Winform application named `TRTCCSharpDemo`.
 ![](https://main.qcloudimg.com/raw/b0f7a80d2f86e73b4cc277bd05c73fd9.png)

### Step 3. Copy the files

Copy the extracted SDK folder to the directory where `TRTCCSharpDemo.csproj` is located.
>?If you only need the SDK for C#, you can delete the `CPlusPlus` directory under the SDK path.

![](https://main.qcloudimg.com/raw/dbd90fce988853c26a832930cef2e9a6.png)

<span id="Step4"></span>
### Step 4. Modify the project configuration
**Step 4.1. Add references**
1. Find **Configuration Manager** in the **Build** directory of Visual Studio and open it.
<span id="step4_1_2"></span>
2. Select **New** from the **Active solution platform** drop-down list and the **New Solution Platform** dialog box will appear.
<span id="step4_1_3"></span>
3. Type or select the new platform and click **OK**.
 ![](https://main.qcloudimg.com/raw/75f07143f2c6a83a4d22e3f95f8f3864.png)
4. Repeat [substep 2](#step4_1_2) to [substep 3](#step4_1_3) as needed to create solution platforms that need to be supported.
 ![](https://main.qcloudimg.com/raw/e7d906cbc18d32848a25cce38f50d20c.png)
5. Open the folder where the TRTCCSharpDemo project is located and edit the `TRTCCSharpDemo.csproj` file with a text editor.
6. Add the following content to the `<itemGroup>` label in the `TRTCCSharpDemo.csproj` file:
  ```
  // Add references to different platforms
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x64'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'AnyCPU'">
		<HintPath>SDK\CSharp\Win64\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  <Reference Include="ManageLiteAV" Condition="'$(Platform)' == 'x86'">
		<HintPath>SDK\CSharp\Win32\lib\ManageLiteAV.dll</HintPath>
  </Reference>
  ```
  ![](https://main.qcloudimg.com/raw/a76052df7be5fb54cfbcdedc7a5afc58.png)

**Step 4.2. Add the copy command**
1. Open the properties page of the TRTCCSharpDemo by selecting **Solution Explorer** > **Right-click Menu of TRTCCSharpDemo Project** > **Properties**.
2. Add the following command in **Build Events** > **Post-build event command line** to implement automatic copying of the .dll files of the SDK on different platforms to the run directory of the program after compilation is completed as shown below:
```
set Platform=Win64
SETLOCAL ENABLEDELAYEDEXPANSION
if $(PlatformName)==x86 ( 
  set Platform=Win32
)
copy /Y "$(ProjectDir)SDK\CSharp\!Platform!\lib\*.dll" "$(ProjectDir)$(OutDir)"
ENDLOCAL
```
![](https://main.qcloudimg.com/raw/1939c8a6702da356fe58d9945c40a60c.png)

**Step 4.3. Modify the debugging environment**
Open the properties page of the TRTCDemo, select **Build**, and set **Platform** to the solution platform in the top menu bar as shown below:
![](https://main.qcloudimg.com/raw/23462af7ca105e5f78c5b5cbd3242063.png)

### Step 5. Print the SDK version number
1. Add a label control in the designer of `Form1.cs` as shown below:
 ![](https://main.qcloudimg.com/raw/fec574b76a4250a3e948816b7cc1728d.png)
2. Open the `Form1.cs` code file and add the following code:
	```c#
	using System.Windows.Forms;
	using ManageLiteAV;   // 1. Add namespace reference

	namespace TRTCCSharpDemo
	{
			public partial class Form1 : Form
			{
					public Form1()
					{
							InitializeComponent();
							// 2. Get an `ITRTCCloud` instance and print the SDK version number
							ITRTCCloud lTRTCCloud = ITRTCCloud.getTRTCShareInstance(); 
							this.label1.Text = "SDK version : " + lTRTCCloud.getSDKVersion();
							// 3. The `IRTTCCloud` instance needs to be manually terminated at the end of use
							ITRTCCloud.destroyTRTCShareInstance();
					}
			}
	}
	```
3. Press F5 to run and print the version number of the SDK as shown below:
 ![](https://main.qcloudimg.com/raw/9bfebaac4fa339af6b7c74b0413cde1d.png)


## FAQs

- If the following error occurs, please check whether the reference to the SDK is added to the project as instructed in [Modify the project configuration](#Step4).
```
Error CS0246: The type or namespace name "ManageLiteAV" could not be found (are you missing a using directive or an assembly reference?)
```
- If the following error occurs, please check whether the project's running platform is the current target platform of the solution as instructed in [Modify the project configuration](#Step4).
```
System.BadImageFormatException: "Could not load file or assembly "ManageLiteAV, Version=2.0.7152.18518, Culture=neutral, PublicKeyToken=null" or one of its dependencies. An attempt was made to load a program with an incorrect format."
```
- If the following error occurs, please check whether the built event is correctly added to the running directory as instructed in [Modify the project configuration](#Step4).
```
System.IO.FileNotFoundException: "Could not load file or assembly "ManageLiteAV.dll" or one of its dependencies. The specified module could not be found."
```
- Due to possible compatibility issues between different Windows versions, the following .dll files have been added to the SDK for C# to solve such issues:
	![](https://main.qcloudimg.com/raw/1467310c3f5b2ab7271376902d23a2be.png)

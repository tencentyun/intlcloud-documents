### Where can I download GME demos and SDKs?

Please download the relevant demos and SDKs as instructed in [Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). Currently, there are demos for Unity, Cocos2d, native Android development, and native iOS development.

### How do I change the account after downloading the GME demo?
- You need to get the `SDKAppID` and permission key from the console.
- To use your own `AppID`, you need to change the key of voice chat in `GetAuthBuffer` in `AVChatViewController`.

### How can I experience the effect locally if there is only myself in the room?
To experience the effect, use the demo on another device to enter the same room.

### What should I do if `errinfo=priv map info error` is displayed when I use the demo?
There is an error in the relevant room entry parameters. Please check whether the `SDKAppID` and permission key have been replaced.

### How do I use a downloaded demo?
Please see the demo user guide.

### How do I get logs?
**When providing logs, please also specify the time point when the problem occurred.**
The file named `QAVSDK_date.log` is the log file, which is in the following directories:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| macOS     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |


### Why there is no `Authbuffer` file in the downloaded SDK documentation and demo?
The `Authbuffer` file has been merged. Please search for it globally in the SDK.


### Is there a lib file for TEA encryption?
We provide an [Authbuffer compilation document and ZIP package](https://intl.cloud.tencent.com/document/product/607/31461).


### Do the SDKs for Cocos2d-x, native Android, and native iOS have different operation efficiency?
They have no difference on the operation efficiency.


### What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?
Some lib files may be missing. Please decompress the APK file and check whether all library files are present in each folder under `lib`.

### Does the SDK for iOS support debugging in a simulator?
Yes. Please use the latest package from the official website for verification.

### What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the `GMESDK.framework` library?
Select "Build Setting" in the project file and check whether the "-all_load" flag is used in "Other Linker Flags"; and if yes, delete it and compile the project again.


### An ARMv7-related error occurred when I tried to export an iOS executable file from the SDK for Unity, but export worked properly after I deleted ARMv7. What should I do?
You are recommended to upgrade Unity. For more information, please see [this thread](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516) in Unity's forums.
If you have no upgrade needs, simply ignore the ARMv7 architecture during packaging.

### What should I do if the downloaded demo for iOS cannot run?
After you download the official demo for iOS, if an error similar to "ld: warning: directory not found for option" occurs during compilation through Xcode (above v10), you need to manually add the `GMESDK.framework` file in the `GME_SDK` folder at the same level of the demo folder to the `Framework` list of the project.

### What should I do if an error occurs when I download the demo for Unity and export an executable file for PC?
If an error similar to "Found plugins with same names and architectures" occurs, it is because that the GME SDK is available for both the x86 and x86_64 architectures by default. Please delete either SDK in the `plugins` folder.

### What should I do if dll files cannot be found when I download the demo for Unreal and export an executable file for PC?
On a Windows x64 PC, for example, copy all dll files in the `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` project directory to the directory where you saved the executable files (.exe) exported.

### What should I do if another player (such as QQ Player) is required to play back accompaniment on the Windows client?
Please call the related API as instructed in the document of player accompaniment for Windows. As accompaniment with a third-party player uses an advanced API, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance and provide the `tmg_adv_win.h` header file.



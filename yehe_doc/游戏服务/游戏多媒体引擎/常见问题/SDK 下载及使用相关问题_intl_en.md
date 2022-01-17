### Where can I download GME demos and SDKs?

Please download GME demos and SDKs as instructed in the [SDK Download Guide](https://cloud.tencent.com/document/product/607/18521). Currently, the demos are available for Unity, Cocos2d, Android (native) and iOS (native).

### How do I change the account after downloading the GME demo?

- You need to get your SDKAppID and access key in the GME console.
- To use your own AppID instead, you need to modify the key for voice chat in GetAuthBuffer in AVChatViewController.

### Does GME allow using only one openid across multiple devices?

openid is used to uniquely identify a user when initializing the GME engine. Sharing an openid across multiple devices, such as for multi-device login, may render your account unable to use GME properly.

### How can I experience the effect locally if I am the only person in the room?

To do so, simply use the demo on another device to enter the same room.

### What should I do if I receive the error message "errinfo=priv map info error" when using the Demo?

If an error occurs for room access parameters, check whether your SDKAppID and access key have been replaced as instructed.

### How do I use a downloaded demo?

- See [Using Demo](https://intl.cloud.tencent.com/document/product/607/36419).
- For Unity users, see [Using Unity Demo](https://intl.cloud.tencent.com/document/product/607/38333).

### How do I get logs?

**Developers should note that when providing logs, they should also specify the time point when the problem occurred.**
Logs are all named in the format of QAVSDK_date.log, and can be found in the following directories:

| OS | Path |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |


### What do I do if there is no Authbuffer file in the downloaded SDK documentation or demo?

The Authbuffer file has been incorporated into another file. Please search for it in the overall SDK.


### Is any LIB file available for TEA encryption?

It is included in the [Authbuffer compiled document and ZIP package](https://intl.cloud.tencent.com/document/product/607/31461) we provide.


### Do the SDKs for Cocos2d-x, Android (native), and iOS (native) have different operation efficiencies?

No, they do not differ in operation efficiency.


### What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?

Some LIB files may be missing. Please decompress the APK file and check whether all library files are present in each folder under `lib`.

### Does the SDK for iOS support debugging in a simulator?

Yes. Please use the latest SDK version for verification.

### What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the `GMESDK.framework` library?

Select "Build Setting" in the project file and check whether the "-all_load" flag is used in "Other Linker Flags". If yes, delete it and compile the project again.


### What should I do if I’m prompted "framework not found GMESDK" after exporting an XCode project using Unity?

To use the Unity engine, please integrate the GME Unity SDK and use the libGMESDK.a library instead of the framework file.

### An ARMv7-related error occurred when I tried to export an iOS executable file from the SDK for Unity, but the export worked properly after I deleted ARMv7. What should I do?

We recommend that you upgrade Unity. For more information, please see [this thread](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516) in Unity's forums.
If you have no upgrade needs, simply ignore the ARMv7 architecture during packaging.

### What should I do if the downloaded demo for iOS cannot run?

After you download the official demo for iOS, if an error similar to "ld: warning: directory not found for option" occurs during compilation through Xcode (v10 or above), you need to manually add the `GMESDK.framework` file in the `GME_SDK` folder at the same level of the demo folder to the `Framework` list of the project.

### What should I do if an error occurs when I download the demo for Unity and export an executable file for PC?

If an error similar to "Found plugins with same names and architectures" occurs, it is because the GME SDK is available for both the x86 and x86_64 architectures by default. Please delete either SDK in the `plugins` folder.

### What should I do if the DLL file cannot be found when I download the demo for Unreal and export an executable file for PC?

Take Windows x64 as an example. Once you export the executable file, you should copy all the DLL files in the directory `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` to the same directory as the executable file.

### What should I do if another player (such as QQ Player) is required to play back the accompaniment on the Windows client?

As the accompaniment with a third-party player feature uses an advanced API, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance and provide the `tmg_adv_win.h` header file.


## Exporting for iOS
### What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the `GMESDK.framework` library?

Select `Build Setting` in the program file and check whether the `-all_load` flag is used in `Other Linker Flags`. If yes, delete it and compile the program again.


### After exporting Xcode program using Unity, an error `framework not found GMESDK` pops up. 

To use the Unity engine, please integrate the GME Unity SDK and use the `libGMESDK.a` library instead of the `framework` file.

### An ARMv7-related error occurred when I tried to export an iOS executable file from the SDK for Unity, but the export worked properly after I deleted ARMv7. 

We recommend upgrading Unity. For more information, please see [this thread](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516) in Unity's forums.
- If it does not require an upgrade, then you do not need to package the ARMv7 architecture.

### What should I do if the downloaded demo for iOS cannot run?

After you download the official demo for iOS, if an error similar to `ld: warning: directory not found for option` occurs during compilation through Xcode (v10 or above), you need to manually add the `GMESDK.framework` file in the `GME_SDK` folder at the same level of the demo folder to the `Framework` list of the program.


### Does the SDK for iOS support debugging in a simulator?

Yes. Please use the [latest version](https://intl.cloud.tencent.com/document/product/607/18521).

### How to fix the certificate error occurred during demo export?
Error message:
```
Showing Recent Messages:-1: Unity-iPhone has conflicting provisioning settings. Unity-iPhone is automatically signed, but code signing identity iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd has been manually specified. Set the code signing identity value to "iPhone Developer" in the build settings editor, or switch to manual signing in the project editor. (in target 'Unity-iPhone')
```
Solution:
Please replace the Tencent Cloud enterprise certificate with your developer certificate.


### The error below occurs when I am exporting the demo to a device. 
Error message:
```
dyld: Library not loaded: @rpath/libLamemp3.framework/libLamemp3
Referenced from: /private/var/containers/Bundle/Application/XXXX
Reason: image not found
dyld: launch, loading dependent libraries
DYLD_LIBRARY_PATH=/usr/lib/system/introspection
DYLD_INSERT_LIBRARIES=/Developer/usr/lib/libBacktraceRecording.dylib:/Developer/usr/lib/libMainThreadChecker.dylib:/Developer/Library/PrivateFrameworks/DTDDISupport.framework/libViewDebuggerSupport.dylib
```
Solution:
- If you use a dynamic library, the loaded dynamic library is under the static library `Linked Frameworks and Libraries` by default. You need to select it, click the `-` icon to delete it, and then click `+` below `Embedded Binaries` to add a dynamic library.
- You can also modify `framework` to the below:
![](https://main.qcloudimg.com/raw/fe01a75aba37436d4cae1dd68b3b9640.jpg)


## Exporting for Windows

### An error occurs when I download the demo for Unity and export an executable file for PC

If an error similar to `Found plugins with same names and architectures` occurs, it is because that the GME SDK is available for both the x86 and x86_64 architectures by default. Please delete either SDK in the `plugins` folder.


### What should I do if the DLL file cannot be found when I download the demo for Unreal and export an executable file for PC?

Take Windows x64 as an example: once you export the executable file, you should copy all the DLL files in the directory `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` to the same directory as the executable file.

## Exporting for Android

### What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?

Some LIB files may be missing. Please decompress the APK file and check whether all library files are present in each folder under `lib`.

### After the APK is exported to an Android mobile phone, when I open the app, an error message pops up indicating that the app is not supported by the device. 

The error is related to the architectures contained in the packaged executable file. If you do not need the v8a architecture, you can untick it from the export bar in the Unity program configuration.

### The exported APK does not support the simulator. 

Please check whether there is any library file containing the x86 architecture SDK in the exported APK. If no, please download the SDK again, import the x86 architecture SDK, and finally export the executable file again.

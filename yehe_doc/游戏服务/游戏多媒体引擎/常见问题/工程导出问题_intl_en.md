
## Export for iOS
### What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the `GMESDK.framework` library?

Select **Build Settings** in the project file and check whether the "-all_load" flag is used in **Other Linker Flags**; if so, delete it and compile the project again.


### What should I do if I'm prompted `framework not found GMESDK` after exporting an Xcode project using Unity?

To use the Unity engine, integrate the GME SDK for Unity and use the `libGMESDK.a` library instead of the framework file.

### An ARMv7-related error occurred when I tried to export an iOS executable file from the SDK for Unity, but the export worked properly after I deleted ARMv7. What should I do?

- We recommend you upgrade Unity. For more information, see [this thread](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516) in Unity's forums.
- If you have no upgrade needs, simply ignore the ARMv7 architecture during the build.

### What should I do if the downloaded demo for iOS cannot run?

After you download the official demo for iOS, if an error similar to `ld: warning: directory not found for option` occurs during compilation through Xcode (v10 or later), you need to manually add the `GMESDK.framework` file in `GME_SDK` at the same level of the demo folder to the `Framework` list of the project.


### Does the SDK for iOS support debugging in a simulator?

Yes. Use the latest package from [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521) for verification.

### What should I do if a certificate error occurs while exporting the demo?
Below is the error message:
```
Showing Recent Messages:-1: Unity-iPhone has conflicting provisioning settings. Unity-iPhone is automatically signed, but code signing identity iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd has been manually specified. Set the code signing identity value to "iPhone Developer" in the build settings editor, or switch to manual signing in the project editor. (in target 'Unity-iPhone')
```
Solutions:
Replace the Tencent Cloud enterprise certificate with your developer certificate during export on a real device.


### What should I do if the following error occurs during export on a real device?
Below is the error message:
```
dyld: Library not loaded: @rpath/libLamemp3.framework/libLamemp3
Referenced from: /private/var/containers/Bundle/Application/XXXX
Reason: image not found
dyld: launch, loading dependent libraries
DYLD_LIBRARY_PATH=/usr/lib/system/introspection
DYLD_INSERT_LIBRARIES=/Developer/usr/lib/libBacktraceRecording.dylib:/Developer/usr/lib/libMainThreadChecker.dylib:/Developer/Library/PrivateFrameworks/DTDDISupport.framework/libViewDebuggerSupport.dylib
```
Solutions:
- If a dynamic library is used, once it is loaded, it will be displayed in **Linked Frameworks and Libraries** by default. Select the dynamic library, click **-** below it to delete it, and click **+** in **Embedded Binaries** to add it again.
- Alternatively, modify the framework as shown below:
![](https://main.qcloudimg.com/raw/fe01a75aba37436d4cae1dd68b3b9640.jpg)


## Export for Windows

### What should I do if an error occurs when I download the demo for Unity and export an executable file for PC?

If an error similar to `Found plugins with same names and architectures` occurs, it is because the GME SDK is available for both the x86 and x86-64 architectures by default. Delete either SDK in the `plugins` folder.


### What should I do if the DLL file cannot be found when I download the demo for Unreal Engine and export an executable file for PC?

Take Windows x64 as an example. Once you export the executable file, you should copy all the DLL files in the directory `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64` to the same directory as the executable file.

## Export for Android

### What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?

Some LIB files may be missing. Please decompress the APK file and check whether all library files are present in each folder under `lib`.

### After the application is exported to an Android phone, when I open the application, an error message pops up indicating that the application is not supported by the device. What should I do?

This problem is relevant to the architecture of the packaged executable file. If you don't need the arm64-v8a architecture, you can deselect it in export configuration in the Unity project configuration.

### What should I do if the exported APK file doesn't support emulators?

First check whether the APK file has x86 library files; if not, download the SDK, import the x86 SDK files, and export an executable file again.




## Export Unity Project to WebGL

### Is the HTTPS or HTTP protocol required for the Unity WebGL export?
The build needs to be deployed over the **HTTPS protocol**. If you use the HTTP protocol, feature exceptions will occur.

### What should I do if error 1004 occurs during room entry after the Unity WebGL build is created?
If error `1004(Invalid Argument)` occurs during room entry, it is because the entered `Openid` is less than 10,000, so **enter a value greater than 10,000**.

### Does Unity WebGL supports mobile devices?
According to Unity's official website, the Unity WebGL build currently cannot run on a mobile device. For more information, see [WebGL Browser Compatibility](https://docs.unity3d.com/2020.1/Documentation/Manual/webgl-browsercompatibility.html).

### After I create a Unity WebGL build, can I use the GME's range voice feature?
Currently, WebGL only supports the most basic voice chat features such as room entry/exit and mic-on/off. If you call an API of an unsupported feature, error code 1006 will be returned. We are trying to adapt the range voice feature to WebGL.

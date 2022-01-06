### What are the differences between TRTC V1 (iLiveSDK) and V2 (LiteAVSDK)?
![](https://qcloudimg.tencent-cloud.cn/raw/66a90ec42a5918f73ec95c2a23339ee6.png)

| Item | Old (V1) | New (V2) |
|:-------:|:-------:|:-------:|
| Architecture | iLiveSDK | LiteAVSDK |
| IM SDK   |  Built-in        |  Not built-in       |
| API |  V1 |  V2 |
| CDN streaming | Must be enabled via RESTful API |  Can be enabled via client |
| Line  |  V1 |   V2 |

### How do I upgrade from TRTC V1 (iLiveSDK) to V2 (LiteAVSDK)?
- If your project **has never integrated the TRTC SDK**, we strongly recommend that you use V2 (LiteAVSDK) from the beginning, which outperforms V1 in terms of call quality, line, ease of integration, and feature extension.
- If your project **is running stably without encountering any problems**, we recommend that you stick to V1 for the time being as the lines of V1 and V2 are not interconnected currently.
- If you are **in the process of integrating the old version SDK (V1) into your project**, we recommend that you switch to V2, which uses brand new APIs and is much faster to integrate than V1.
- If you **are already using V1 and hope to improve your call quality by upgrading to V2**, since the lines of V1 and V2 are not interconnected currently, you need to first integrate the new SDK into your project, wait for the new version to cover your user base, and then switch from V1 to V2 lines in the cloud. See below for details:
 1. Integrate the new SDK into your project and run a test.
 2. Add a field that indicates the SDK version number in the room list so that your application can determine whether to use the V1 or V2 SDK based on this field on the server.
 3. Release the update to your application and wait for it to cover your user base.
 4. Change the field indicating the SDK version number in the room list from V1 to V2 to switch from V1 to V2 lines.


### How do I integrate LiteAVSDK and iLiveSDK for Android at the same time?

Both iLiveSDK and LiteAVSDK use Tencent Real-time Audio Engine (TRAE) to process audio, for example, for noise suppression and echo cancellation. LiteAVSDK uses a newer version of TRAE and includes all the APIs of iLiveSDK. Therefore, you only need to configure the TRAE library of LiteAVSDK for your project.
Integrate the SDKs as AAR files and, in the `build.gradle` file of your subproject (the application directory), add code in the `android{}` closure as described below.
>! You must reference LiteAVSDK before iLiveSDK.

```java
android{
// 1. Configure packaging options in Gradle
packagingOptions {
pickFirst 'lib/armeabi-v7a/libTRAECodec.so'
pickFirst 'lib/armeabi-v7a/libstlport_shared.so'
pickFirst 'lib/armeabi/libTRAECodec.so'
pickFirst 'lib/armeabi/libstlport_shared.so'
}
// 2. Import dependencies
implementation(name:'LiteAVSDK_TRTC_6.4.7108', ext:'aar')  // Make sure that you import LiteAVSDK before iLiveSDK
implementation 'com.tencent.ilivesdk:ilivesdk:1.9.4.6.4'
}
```

### How do I integrate LiteAVSDK, iLiveSDK, and BeautySDK for iOS at the same time?
TRTC V1 uses BeautySDK to implement features including beauty filters and animated effects. These features are built into TRTC V2. As a result, if your project has already integrated iLiveSDK and imported BeautySDK, a file conflict will occur. Below is the solution:

| Edition                                   | Solution                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| BeautySDK Basic (without retouching features) | Add a header search path for BeautySDK in your Xcode project and unlink BeautySDK. |
| BeautySDK Advanced (with retouching features)    | Use LiteAVSDK Enterprise, add a header search path for BeautySDK in your Xcode project, and unlink BeautySDK (LiteAVSDK Enterprise integrates the retouching component, which you can use with the license you have already purchased.) |

### How do I integrate LiteAVSDK and iLiveSDK for Windows at the same time?

Both iLiveSDK and LiteAVSDK for Windows use Tencent Real-time Audio Engine (TRAE) to process audio, for example, for noise suppression and echo cancellation. However, LiteAVSDK uses a newer version of TRAE and differs from iLiveSDK in terms of feature usage. Therefore, you cannot use it to replace the TRAE of iLiveSDK directly. Below is the solution:

#### Project structure

We recommend the following project structure:

	|
	|- Main application.exe
	|- Other files main application.exe depends on
	|- iLiveSDK.dll
	|- Other files iLiveSDK.dll depends on
	|- LiteAV
	|        |- liteav.dll
	|        |- Other files liteav.dll depends on

#### Initialization

You can use iLiveSDK by linking a LIB file into your project or load it dynamically using the code below:
```cpp
HMODULE hiLive = LoadLibrary("iLiveSDK.dll");
```

To use LiteAVSDK, load and initialize it using the code below:

<dx-codeblock>
::: cpp cpp
typedef ITRTCCloud* (*getTRTCShareInstanceMtd)();
typedef void(*destroyTRTCShareInstanceMtd)();

TCHAR dllPath[MAX_PATH];
GetModuleFileName(nullptr, dllPath, MAX_PATH);
PathRemoveFileSpec(dllPath);
wcscat(dllPath, L"\\LiteAV\\");
SetDllDirectory(dllPath);
HMODULE hLiteAV = LoadLibrary(L"liteav.dll");
if (!hLiteAV) {
printf("Failed to load liteav.dll: %d", GetLastError());
return;
}

getTRTCShareInstanceMtd pGetTRTCShareInstance = (getTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "getTRTCShareInstance");
if (!pGetTRTCShareInstance) {
printf("Failed to load the getTRTCShareInstance function");
return;
}

destroyTRTCShareInstanceMtd pDestroyTRTCShareInstance = (destroyTRTCShareInstanceMtd)GetProcAddress(hLiteAV, "destroyTRTCShareInstance");
if (!pDestroyTRTCShareInstance) {
printf("Failed to load the destroyTRTCShareInstance function");
return;
}

ITRTCCloud *pTrtcCloud = m_pGetTRTCShareInstance();
if (!pTrtcCloud) {
printf("Failed to create a TRTC instance");
return;
}
SetDllDirectory(nullptr);

pTrtcCloud->enterRoom(...);
:::
</dx-codeblock>




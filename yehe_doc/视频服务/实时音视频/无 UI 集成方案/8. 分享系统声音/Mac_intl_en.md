## Pain Point and Solution
It is often necessary to share system audio in scenarios such as screen sharing, but the sound cards of Mac computers do not allow the capturing of system audio, making it impossible to share system audio on Mac computers. To solve this problem, TRTC has introduced a feature that records system audio on Mac computers. See below for details on how to enable the feature.

## Directions

[](id:step1)
### Step 1. Integrate the TRTCPrivilegedTask library  

The TRTC SDK uses the [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2) library to get root access and install the virtual sound card plugin `TRTCAudioPlugin.driver` in the system directory `/Library/Audio/Plug-Ins/HAL`.

<dx-tabs>
::: Integration via CocoaPods  
1. Open the `Podfile` file in the root directory of your project and add the following content:
<dx-codeblock>
::: ruby ruby
platform :osx, '10.10'  

target 'Your Target' do
    pod 'TRTCPrivilegedTask', :podspec => 'https://pod-1252463788.cos.ap-guangzhou.myqcloud.com/liteavsdkspec/TRTCPrivilegedTask.podspec'
end
:::
</dx-codeblock>

2. Run the `pod install` command to install the **TRTCPrivilegedTask** library.

>?
>- If you cannot find a `Podfile` file in the directory, run the `pod init` command to create one and then add the above content.
>-  For how to install CocoaPods, see CocoaPods' [official installation document](https://guides.cocoapods.org/using/getting-started.html).
:::
::: Manual integration
1. Download the [TRTCPrivilegedTask](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/TRTCPrivilegedTask/TRTCPrivilegedTask.tar.bz2) library.
2. Decompress the downloaded file, open your Xcode project, and import the file to the project.
3. Select the target to run, select **Build Phases**, expand **Link Binary with Libraries**, click **+**, and add the dependent library `libPrivilegedTask.a`.  
![libPrivilegedTask.a](https://main.qcloudimg.com/raw/cc5b3365e72cee80cda7f0db0a4e1b62.png)  
:::
</dx-tabs> 


[](id:step2)
### Step 2. Disable App Sandbox  
In the entitlements file of the app, delete **App Sandbox**.  
![Sandbox](https://main.qcloudimg.com/raw/98fed5571040f24c2891f4b87ddce15e.png)  


[](id:step3)
### Step 3. Package the virtual sound card plugin  
After you [integrate the TRTCPrivilegedTask library](#step1) and [disable App Sandbox](#step2), when you use the system audio recording feature for the first time, the SDK will download the virtual sound card plugin from the internet and install it. To accelerate this process, you can package the virtual sound card plugin `TRTCAudioPlugin.driver` in the ` PlugIns` directory of `TXLiteAVSDK_TRTC_Mac.framework` to the resources directory of the app's bundle, as shown below.  
![Packaging plugin](https://main.qcloudimg.com/raw/b04b805d4848f2ecd6fd7dcc83176a9e.png)
Alternatively, copy the file to the `PlugIns` directory of the app's bundle.  
![Packaging plugin 2](https://main.qcloudimg.com/raw/05fb5c6ec4dba74c3b5fb880ed28033e.png)  


[](id:step4)
### Step 4. Start capturing system audio  
Call the [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) API to start system audio capturing and mix the audio into the upstream audio stream. The result is called back via [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676).
```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[_trtc startLocalAudio];
[trtcCloud startSystemAudioLoopback];
```

>! After the TRTCPrivilegedTask library is integrated and App Sandbox disabled, when you call `startSystemAudioLoopback` for the first time, the SDK will request root access.  
>After being granted root access, the SDK will start installing the virtual sound card plugin to the computer automatically.



[](id:step5)

### Step 5. Stop capturing system audio 

Call the [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) API to stop capturing system audio.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud stopSystemAudioLoopback];
```

[](id:step6)
### Step 6. Set the volume of system audio capturing

Call the [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) API to set the volume of system audio capturing.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
[trtcCloud setSystemAudioLoopbackVolume:80];
```

## Summary

- TRTC records system audio on Mac computers using the virtual sound card plugin `TRTCAudioPlugin.driver`. For the plugin to work, you need to copy it to the system directory `/Library/Audio/Plug-Ins/HAL` and restart the audio service. You can check whether the plugin is installed successfully using the Audio MIDI Setup app, which can be found in the `Other` folder of Launchpad. The presence of a device named "TRTC Audio Device" in the device list of the app indicates that the plugin is installed successfully.  
- The purpose of [integrating the TRTCPrivilegedTask library](#step1) and [disabling App Sandbox](#step2) is for the SDK to get root access so as to install the virtual sound card plugin; otherwise it cannot automatically install the plugin. However, if a virtual sound card is already installed in the system, you can use the system audio recording feature without integrating the TRTCPrivilegedTask library or disabling App Sandbox.
> ? You can also manually install a virtual sound card to enable the feature.
>
> 1. Copy `TRTCAudioPlugin.driver` in the `PlugIns` directory of `TXLiteAVSDK_TRTC_Mac.framework` to the system directory `/Library/Audio/Plug-Ins/HAL`.
2. Restart the system audio service. 

<dx-codeblock>
::: Bash script for restarting the system audio service
 sudo cp -R TXLiteAVSDK_TRTC_Mac.framework/PlugIns/TRTCAudioPlugin.driver /Library/Audio/Plug-Ins/HAL  
 sudo kill -9 `ps ax|grep 'coreaudio[a-z]' |awk '{print $1}'`
:::
</dx-codeblock>


[](id:note)
## Notes
- Disabling App Sandbox will change the user paths obtained in your app.  
Directories returned via methods such as the calling of `NSSearchPathForDirectoriesInDomains`will change from sandbox directories to user directories. For example, ` ~/Documents` and `~/Library` will become `/Users/UsernameDocuments` and `/Users/Username/Library`.
- You may be unable to release your app to the Mac App Store after integrating the TRTCPrivilegedTask library.  
App Sandbox must be disabled for the SDK to get root access and automatically install a virtual sound card. This may cause your app to be rejected by the Mac App Store. For details, see [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility).  
If you need to release your app to the Mac App Store or want to use the Sandbox feature, consider manually installing a virtual sound card.  

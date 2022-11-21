### What should I do if I receive the error message "The package you purchased does not support this ability"?

If the above error occurs, it indicates that you haven’t activated TRTC or your TRTC package has expired. For directions on how to activate TRTC, see [Step 1. Activate services](https://www.tencentcloud.com/document/product/647/50992#step1). You can get a free trial package after activation.

### How do I buy a TRTC package?

See [Billing Overview](https://www.tencentcloud.com/document/product/647/50553). If you have any questions, please click the icon in the bottom right corner of the page to contact us.

### How do I modify the source code of `TUICallKit`?

Import the component using CocoaPods:

1. Create a `TUICallKit` folder in the same directory as `Podfile` in your project.

2. Go to the component’s [GitHub page](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `TUICallKit` and `Resources` folders and the `TUICallKit.podspec` file in [iOS](https://github.com/tencentyun/TUICalling/tree/main/iOS) to the `TUICallKit` folder in your project.
3. Add the following dependency to your `Podfile`.

```objectivec
# :path => "The relative path of `TUICallKit.podspec`"
pod 'TUICallKit', :path => "TUICallKit/TUICallKit.podspec"
```

4. Execute `pod install`.

>! Make sure `TUICallKit`, `Resources`, and `TUICallKit.podspec` are in the same directory.

**After `TUICallKit` is imported, you will see this directory structure**:

![](https://qcloudimg.tencent-cloud.cn/raw/91afcf4f9c3752222ef4e0589c818eed.png)

>? The folders are organized hierarchically, making it easy for you to view and modify the source code.

### What should I do if TUICallKit conflicts with an audio/video library that I have integrated?

You cannot integrate multiple audio/video libraries of Tencent Cloud at the same time. Otherwise, a duplicate symbol error may occur. You can use the following methods to troubleshoot the issue:

1. If you have integrated `TXLiteAVSDK_TRTC`, a duplicate symbol error will not occur. Just add the following in `Podfile`:
```objectivec
pod 'TUICallKit'
```

2. If you have integrated `TXLiteAVSDK_Professional`, a duplicate symbol error will occur. You can add the following in `Podfile`:
```objectivec
pod 'TUICallKit/Professional'
```

3. If you have integrated `TXLiteAVSDK_Enterprise`, a duplicate symbol error will occur. We recommend you update to `TXLiteAVSDK_Professional` and use `TUICallKit/Professional`.

### What should I do if the "ld: framework not found BoringSSL clang: error: linker command failed with exit code 1  sdk" error occurs when I integrate `TUICallKit`?

Currently, the audio/video libraries `TUICallKit` relies on do not support emulators. Please use a real device for demo run or debugging.

### Can I not integrate the IM SDK if I use only TRTC features?

**No, you can’t.** All components of `TUIKit` rely on the IM SDK for underlying logic such as outgoing call signaling and busy line signaling. If you have already purchased IM’s services, you can use them according to `TUICallKit` logic.

### Does `TUICallKit` support custom ringtones?

Yes. You can implement this by calling [TUICalling#setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell).

### How do I install CocoaPods?

Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```objectivec
sudo gem install cocoapods
```

### Can `TUICallKit` run in the background?

**Yes**. If you want `TUICallKit` to run in the background, select your project, under the **Capabilities** tab, toggle on **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**.

![](https://qcloudimg.tencent-cloud.cn/image/document/970de09ccdab7defb8df741fe671de33.jpeg)

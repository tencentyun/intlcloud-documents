## Supported Platforms

The SDK is supported on iOS 8.0 and above.

## Environment Requirements

+ Xcode 9 or above
+ OS X 10.10 or above

## Directions

### Step 1. Link the SDK and system libraries
1. Decompress the downloaded SDK package, copy framework files whose names start with `TXLiteAVSDK\_` (e.g. TXLiteAVSDK_UGC.framework) in the SDK folder to your project folder, and drag them to the project.
2. Select your project’s target, and add the following system libraries.
  - Accelerate.framework
  - SystemConfiguration.framework
  - libc++.tbd
  - libsqlite3.tbd
The library dependencies of the project after the addition are as shown below:
![](https://main.qcloudimg.com/raw/a5fe16ca046a0aad84224e1ffa766a42.jpg)
3. Select your project’s target, search for `bitcode` in **Building Settings**, and set **Enable Bitcode** to **No**.

### Step 2. Configure app permissions
The app needs access to the photo album, which can be configured in `Info.plist`. Right-click `Info.plist`, select **Open as** > **Source Code**, and copy and modify the code below.
```
<key>NSAppleMusicUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your media library to obtain music files. It cannot add music if you deny it access.</string> 
<key>NSCameraUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your camera to be able to shoot videos with images.</string> 
<key>NSMicrophoneUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your mic to be able to shoot videos with audio.</string> 
<key>NSPhotoLibraryAddUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your photo album to save edited video files.</string> 
<key>NSPhotoLibraryUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your photo album to edit your video files.</string> 
```

### Step 3. Configure the license and get basic information
Follow the steps in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) to apply for a license, and copy the key and license URL in the [console](https://console.cloud.tencent.com/vod/license).
![](https://main.qcloudimg.com/raw/7bbf7fb9e3d13944bc3b6823fd786269.png)
Before using UGSV features in your app, we recommend that you add the following code to `- [AppDelegate application:didFinishLaunchingWithOptions:]`.

```objc
@import TXLiteAVSDK_UGC;
@implementation AppDelegate
- (BOOL)application:(UIApplication*)applicationdidFinishLaunchingWithOptions:(NSDictinoary*)options {
    NSString * const licenceURL = @"<License URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";
    [TXUGCBase setLicenceURL:licenceURL key:licenceKey];
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

>?
>- If you use a **v4.7 license** and have updated the SDK to v4.9, you can click **Switch to New License** in the console to generate a new license key and URL. A new license can be used only on v4.9 or above and should be configured as described above.
- For the Enterprise Edition, see [Animated Effects and Face Changing](https://intl.cloud.tencent.com/document/product/1069/38030).

### Step 4. Configure logs
You can enable/disable console log printing and set the log level in `TXLiveBase`. Below are the APIs used.
- **setConsoleEnabled**
Sets whether to print the SDK output in the Xcode console.
- **setLogLevel**
Sets whether to allow the SDK to print local logs. By default, the SDK writes logs to the **Documents/logs** folder of the current app.
We recommend that you enable local log printing. You may need to provide log files if you run into a problem and need technical support.
- **Viewing log files**
To reduce the storage space taken up by log files, the UGSV SDK encrypts local logs and limits their number. You need a log [decompression tool](http://dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py) to view the content of log files.
```objc
  [TXLiveBase setConsoleEnabled:YES];
  [TXLiveBase setLogLevel:LOGLEVEL_DEBUG];
```

### Step 5. Build and run the project

If the above steps are performed correctly, you will be able to successfully compile the `HelloSDK` project. Run the app in the debug mode, and the following SDK version information will be printed in the Xcode console:
```
2017-09-26 16:16:15.767 HelloSDK[17929:7488566] SDK Version = 5.2.5541
```

## Quick Feature-based Integration
UGCKit is a UI component library built based on the UGSV SDK. It helps you quickly integrate different features of the SDK.

You can find UGCKit in `Demo/TXLiteAVDemo/UGC/UGCKit` of the SDK package, which you can download at [GitHub](https://github.com/tencentyun/UGSVSDK/tree/master/iOS) or [here](https://intl.cloud.tencent.com/document/product/1069/37914).

### Environment Requirements
- Xcode 10 or above
- iOS 9.0 or above


### Step 1. Integrate UGCKit 
1. **Configure the project**:
	1. Use CocoaPods in your project and, based on your actual conditions, do either of the following:
		- In the root directory of your project, run `pod init && pod install` to get the Podfile.
		- Copy **BeautySettingKit** and **UGCKit** to the root directory of your project (the same directory as the Podfile).
	2. Open the Podfile and add the following:
```
pod 'BeautySettingKit', :path => 'BeautySettingKit/BeautySettingKit.podspec'
pod 'UGCKit', :path => 'UGCKit/UGCKit.podspec', :subspecs => ["UGC"]   #subspecs Choose according to your SDK
```
	3. Run **pod install** and open `project name.xcworkspace`. You will find a `UGCKit BeautySettingKit` file in `Pods/Development Pods`.
2. **Import resources of the Enterprise Edition (required only if you use the Enterprise Edition)**:
Drag `EnterprisePITU` (in `App/AppCommon` of the ZIP file of the Enterprise Edition SDK) to your project, click **Create groups**, select your target, and click **Finish**.


### Step 2. Use UGCKit

1. **Shooting**
`UGCKitRecordViewController` provides the video shooting feature. To enable the feature, just instantiate the controller and display it in the UI.
<dx-codeblock>
::: XCode 
UGCKitRecordViewController *recordViewController = [[UGCKitRecordViewController alloc] initWithConfig:nil theme:nil];
[self.navigationController pushViewController:recordViewController]
```
Shooting results are called back via the completion block, as shown below:
```
   recordViewController.completion = ^(UGCKitResult *result) {
       if (result.error) {
           // Shooting error.
          [self showAlertWithError:error];
       } else {
           if (result.cancelled) {
               // User cancelled shooting and left the shooting view.
               [self.navigationController popViewControllerAnimated:YES];
          } else {
               // Shooting successful. Use the result for subsequent processing.
               [self processRecordedVideo:result.media];
           }
       }
   };
:::
</dx-codeblock>
2. **Editing**
`UGCKitEditViewController` provides the slideshow making and video editing features. During instantiation, you need to pass in the media object to be edited. Below is an example that involves the editing of a shooting result:
<dx-codeblock>
::: XCode 
   - (void)processRecordedVideo:(UGCKitMedia *)media {
       // Instantiate the editing view controller.
       UGCKitEditViewController *editViewController = [[UKEditViewController alloc] initWithMedia:media conifg:nil theme:nil];
       // Display the editing view controller.
       [self.navigationController pushViewController:editViewController animated:YES];
```
Editing results are called back via the completion block, as shown below:
```
       editViewController.completion = ^(UGCKitResult *result) {
       if (result.error) {
           // Error.
          [self showAlertWithError:error];
       } else {
           if (result.cancelled) {
               // User cancelled shooting and left the editing view.
               [self.navigationController popViewControllerAnimated:YES];
          } else {
               // Video edited and saved successfully. Use the result for subsequent processing.
               [self processEditedVideo:result.path];
           }
       }
   }
:::
</dx-codeblock>
3. **Selecting video or image from photo album**
`UGCKitMediaPickerViewController` is used to select and splice images or videos. When multiple videos are selected, it returns a spliced video. Below is an example:
<dx-codeblock>
::: XCode 
   // Configure initialization.
   UGCKitMediaPickerConfig *config = [[UGCKitMediaPickerConfig alloc] init];
   config.mediaType = UGCKitMediaTypeVideo;//Select videos.
   config.maxItemCount = 5;                // Up to five can be selected.

   // Instantiate the media picker view controller.
   UGCKitMediaPickerViewController *mediaPickerViewController = [[UGCKitMediaPickerViewController alloc] initWithConfig:config theme:nil];
   // Display the media picker view controller.
   [self presentViewController:mediaPickerViewController animated:YES completion:nil];
   ```
   The selection result is called back via the completion block, as shown below:
   ```
   mediaPickerViewController.completion = ^(UGCKitResult *result) {
     if (result.error) {
         // Error.
         [self showAlertWithError:error];
     } else {
          if (result.cancelled) {
               // User cancelled shooting and left the picker view.
               [self dismissViewControllerAnimated:YES completion:nil];
          } else {
               // Video edited and saved successfully. Use the result for subsequent processing.
               [self processEditedVideo:result.media];
          }
     }
   }
:::
</dx-codeblock>
4. **Clipping**
`UGCKitCutViewController` provides the video clipping feature. As with the editing API, you need to pass in a media project when instantiating the controller and process clipping results in `completion`.
<dx-codeblock>
::: XCode 
   UGCKitMedia *media = [UGCKitMedia mediaWithVideoPath:@"<#video path#>"];
   UGCKitCutViewController *cutViewController = [[UGCKitCutViewController alloc] initWithMedia:media theme:nil];
   cutViewController.completion = ^(UGCKitResult *result) {
        if (!result.cancelled && !result.error) {
             [self editVideo:result.media];
        } else {
             [self.navigationController popViewControllerAnimated:YES];
        }
   }
   [self.navigationController pushViewController: cutViewController]
:::
</dx-codeblock>
   

## Module Description
Read the documents below to learn more about different modules of the SDK.

- [Video shooting](https://intl.cloud.tencent.com/document/product/1069/38007)
- [Video editing](https://intl.cloud.tencent.com/document/product/1069/38013)
- [Video splicing](https://intl.cloud.tencent.com/document/product/1069/38014)
- [Video uploading](https://intl.cloud.tencent.com/document/product/1069/38016)
- [Playback](https://intl.cloud.tencent.com/document/product/1069/38017)
- [Animated effects and face changing (Enterprise)](https://intl.cloud.tencent.com/document/product/1069/38030)

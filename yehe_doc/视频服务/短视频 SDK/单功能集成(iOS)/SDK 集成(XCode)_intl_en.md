### Supported Platforms

The SDK is supported on iOS 8.0 and above.

## Environment Requirements

+ Xcode 9 or above
+ OS X 10.10 or above

## Directions

### Step 1. Link the SDK and system libraries.
1. Decompress the downloaded SDK package, copy framework files whose names start with `TXLiteAVSDK\_` (e.g. TXLiteAVSDK_UGC.framework) in the SDK folder to your project folder, and drag them to the project.
2. Select your project’s target, and add the following system libraries.
  - Accelerate.framework
  - SystemConfiguration.framework
  - libc++.tbd
  - libsqlite3.tbd
The library dependencies of the project after the addition are as shown below:
![](https://main.qcloudimg.com/raw/a5fe16ca046a0aad84224e1ffa766a42.jpg)
3. Select your project’s target, search for `bitcode` in **Building Settings**, and set **Enable Bitcode** to **No**.

### Step 2. Configure app permissions.
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

### Step 3. Set SDK licenses and get basic information.
Follow the steps in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) to apply for a license, and copy the key and license URL in the [console](https://console.cloud.tencent.com/vod/license).
![](https://main.qcloudimg.com/raw/7bbf7fb9e3d13944bc3b6823fd786269.png)
Before using UGSV features in your app, we recommend that you add the following code to `- [AppDelegate application:didFinishLaunchingWithOptions:]`.

```objc
@import TXLiteAVSDK_UGC;
@implementation AppDelegate
- (BOOL)application:(UIApplication*)applicationdidFinishLaunchingWithOptions:(NSDictinoary*)options {
    NSString * const licenceURL = @"<License URL obtained>";
    NSString * const licenceKey = @"<Key obtained>";
    [TXUGCBase setLicenceURL:licenceURL key:licenceKey];
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

>?
 
- For the Enterprise Edition, see [Animated Effects and Face Changing](https://intl.cloud.tencent.com/document/product/1069/38030).

### Step 4. Configure logs.
You can enable/disable console log printing and set the log level in `TXLiveBase`. Below are the APIs used.
- **setConsoleEnabled**
Sets whether to print the SDK output in the Xcode console.
- **setLogLevel**
Sets whether to allow the SDK to print local logs. By default, the SDK writes logs to the **Documents/logs** folder of the current app.
We recommend that you enable local log printing. You may need to provide log files if you run into a problem and need technical support.
- **Viewing log files**
To reduce the storage space taken up by log files, the UGSV SDK encrypts local log files and limits their number. You need to use the log [decompression tool](http://dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py) to view the content of log files.
```objc
  [TXLiveBase setConsoleEnabled:YES];
  [TXLiveBase setLogLevel:LOGLEVEL_DEBUG];
```

### Step 5. Compile and run.

If the above steps are performed correctly, you will be able to successfully compile the `HelloSDK` project. Run the app in the debug mode, and the following SDK version information will be printed in the Xcode console:
```
2017-09-26 16:16:15.767 HelloSDK[17929:7488566] SDK Version = 5.2.5541
```

## Quick Feature-specific Integration
UGCKit is a UI component library built on top of the UGSV SDK. It helps you quickly integrate different features of the SDK.

You can get UGCKit in `Demo/TXLiteAVDemo/UGC/UGCKit` of the SDK package, which you can download at [GitHub](https://github.com/tencentyun/UGSVSDK/tree/master/iOS) or [here](https://intl.cloud.tencent.com/document/product/1069/37914).

### Environment Requirements
- Xcode 10 or above
- iOS 8.0 or above

### Step 1. Integrate UGCKit. 
1. **Import UGCKit and BeautyPannel (BeautySettingKit).**
	1. Copy the `Demo/TXLiteAVDemo/UGC/UGCKit` folder to the directory of your project, and drag `UGCKit.xcodeproj` in `UGCKit` to the project.
	2. Copy the `Demo/TXLiteAVDemo/BeautySettingKit` folder to the directory of your project, and drag `TCBeautyPanel.xcodeproj` in `BeautySettingKit` to the project.
![](https://main.qcloudimg.com/raw/48fa8833ea243bba61eec09bbdb38d33.png)
2. **Configure dependencies.**   
Click your project’s target, select **Build Phase**, click **+** in **Dependencies**, select `UGCKit.framework`, `UGCKitResources`, `TCBeautyPanel.framework` and `TCBeautyPanelResources`, and click **Add**.
![](https://main.qcloudimg.com/raw/098808d270672bd4413fbca2d92b7e4a.png )
3. **Link `UGCKit.framework`, `TCBeautyPannel.framework`, and the SDK.**
  1. Click your project’s target, select **Build Phase**, click **+** in **Link Binary With Libraries**, select `UGCKit.framework` and `TCBeautyPannel.framework`, and click **Add**.
![](https://main.qcloudimg.com/raw/ccbc89f8a0ff68ac4e9159c9388070b7.png)
  2. Go to the directory of the SDK in Finder, drag the SDK to **Link Binary With Libraries**, or find the directory of the SDK in Xcode and click **Add files** to add the SDK, as shown below.
![](https://main.qcloudimg.com/raw/8432ca1427b51e65ff40e10bb460bbf9.png)
  3. Drag `FilterResource.bundle` in `TXLiteAVDemo/App/Resource` to the project and check **App Target**.
4. **Import resources.**
	1. Click your project’s target, select **Build Phase**, and expand `Copy Bundle Resources`.
	2. Expand `UGCKit.xcodeproj` and `Products` in the directory on the left, drag `UGCKitResources.bundle` to `Copy Bundle Resources`, and expand `TCBeautyPannel.xcodeproj` and `Products`.
	3. Drag `TCBeautyPanelResources.bundle` to `Copy Bundle Resources`.
![](https://main.qcloudimg.com/raw/6377d1c7b240e008f240d116e5363a8b.png)
5. **Import resources of the Enterprise Edition (for Enterprise Edition only).**
Drag `EnterprisePITU` (which can be found in `App/AppCommon` of the ZIP package of the Enterprise Edition SDK) to the project, select **Create groups**, check your target, and click **Finish**.

#### Step 2. Use UGCKit.

1. **Shooting**
`UGCKitRecordViewController` provides the shooting feature. To enable the feature, just instantiate the controller and display it in the UI.
```
UGCKitRecordViewController *recordViewController = [[UGCKitRecordViewController alloc] initWithConfig:nil theme:nil];
[self.navigationController pushViewController:recordViewController]
```
Shooting results are called back via the completion block, as shown below.
```
   recordViewController.completion = ^(TCUGCResult *result) {
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
```
2. **Editing**
`UGCKitEditViewController` provides the image transition and video editing features. During instantiation, you need to pass in the media object to be edited. Below is an example that involves the editing of a shooting result.
```
   - (void)processRecordedVideo:(UGCKitMedia *)media {
       // Instantiate the editing view controller.
       UGCKitEditViewController *editViewController = [[UKEditViewController alloc] initWithMedia:media conifg:nil theme:nil];
       // Display the editing view controller.
       [self.navigationController pushViewController:editViewController animated:YES];
```
Editing results are called back via the completion block, as shown below.
```
       editViewController.completion = ^(TCUGCResult *result) {
       if (result.error) {
           // Error.
          [self showAlertWithError:error];
       } else {
           if (result.cancelled) {
               // User cancelled shooting and left the editing view.
               [self.navigationController popViewControllerAnimated:YES];
          } else {
               // Editing and saving successful. Use the result for subsequent processing.
               [self processEditedVideo:result.path];
           }
       }
   }
```
3. **Selecting video or image from photo album**
`UGCKitMediaPickerViewController` can be used to select and splice images or videos. When multiple videos are selected, it returns a spliced video. Below is an example.
```
   // Configure initialization.
   UGCKitMediaPickerConfig *config = [[UGCKitMediaPickerConfig alloc] init];
   config.mediaType = UGCKitMediaTypeVideo;//Select videos.
   config.maxItemCount = 5;                // Up to 5 can be selected.

   // Instantiate the media picker view controller.
   UGCKitMediaPickerViewController *mediaPickerViewController = [[UGCKitMediaPickerViewController alloc] initWithConfig:config theme:nil];
   // Display the media picker view controller.
   [self presentViewController:mediaPickerViewController animated:YES completion:nil];
```
   Selecting results are called via the completion block, as shown below.
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
               // Editing and saving successful. Use the result for subsequent processing.
               [self processEditedVideo:result.media];
          }
     }
   }
   ```
4. **Clipping**
`UGCKitCutViewController` provides the video clipping feature. As with the editing API, you need to pass in a media project when instantiating the controller and process clipping results in `completion`.
```
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
```


## Closer Look
Read the documents below for a closer look at different modules of the SDK.

- [Video shooting](https://intl.cloud.tencent.com/document/product/1069/38007)
- [Video editing](https://intl.cloud.tencent.com/document/product/1069/38013)
- [Video splicing](https://intl.cloud.tencent.com/document/product/1069/38014)
- [Video uploading](https://intl.cloud.tencent.com/document/product/1069/38016)
- [Playback](https://intl.cloud.tencent.com/document/product/1069/38017)
- [Animated effects and face changing](https://intl.cloud.tencent.com/document/product/1069/38030)

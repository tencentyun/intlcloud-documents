## Supported Platforms

The SDK is supported on iOS 8.0 and above.

## Development Environment

+ Xcode 9 or above.
+ OS X 10.10 or above.

## Directions

### Step 1. Link the SDK and system libraries
1. Decompress the downloaded SDK resource package and copy the framework files whose filename starts with `TXLiteAVSDK\_` (such as `TXLiteAVSDK_UGC.framework`) in the SDK folder to the project folder and drag them to the project.
2. Select the project target and add the following system libraries:
  - Accelerate.framework
  - SystemConfiguration.framework
  - libc++.tbd
  - libsqlite3.tbd
Then, the project library dependency is as shown below:
![](https://main.qcloudimg.com/raw/a5fe16ca046a0aad84224e1ffa766a42.jpg)
3. Select the project target, search for "bitcode" in "Build Settings", and set "Enable Bitcode" to "No".

### Step 2. Configure application permissions
As the application may need the permission to access the album, you need to add the corresponding item to `Info.plist`. You can right-click in `Info.plist` and select "Open As" > "Source Code" to paste and modify the following content for configuration:
```
<key>NSAppleMusicUsageDescription</key> 
<string>Video Cloud Toolkit needs the permission to access your media library to get the music files; otherwise, music files cannot be added</string> 
<key>NSCameraUsageDescription</key> 
<string>Video Cloud Toolkit needs the permission to access your camera. The image of the shot video is available only after this permission is granted</string> 
<key>NSMicrophoneUsageDescription</key> 
<string>Video Cloud Toolkit needs the permission to access your mic. The audio of the shot video is available only after this permission is granted</string> 
<key>NSPhotoLibraryAddUsageDescription</key> 
<string>Video Cloud Toolkit needs the permission to access your album. Edited files can be saved only after this permission is granted</string> 
<key>NSPhotoLibraryUsageDescription</key> 
<string>Video Cloud Toolkit needs the permission to access your album. Video files can be edited only after this permission is granted</string> 
```

### Step 3. Set the SDK license and get the basic information
Apply for a license as instructed in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) and copy the key and URL from the [console](https://console.cloud.tencent.com/vod/license) as shown below:
![](https://main.qcloudimg.com/raw/a4c1de10918d04b0b425febe9d0a009b.png)
Before you integrate UGSV features into your application, we recommend you set `- [AppDelegate application:didFinishLaunchingWithOptions:]` as follows:

```objc
@import TXLiteAVSDK_UGC;
@implementation AppDelegate
- (BOOL)application:(UIApplication*)applicationdidFinishLaunchingWithOptions:(NSDictinoary*)options {
    NSString * const licenceURL = @"<obtained licnseUrl>";
    NSString * const licenceKey = @"<obtained key>";
    [TXUGCBase setLicenceURL:licenceURL key:licenceKey];
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

### Step 4. Configure logging
In `TXLiveBase`, you can set whether to print logs in the console and the log level. The following are the relevant APIs:
- **setConsoleEnabled**
It is used to set whether to print the SDK output content in the Xcode Console.
- **setLogLevel**
It is used to set whether the SDK can print local logs. The SDK will write logs into the **Documents/logs** folder of the current application.
If you need Tencent Cloud technical support, we recommend you toggle on this switch and provide the log file after reproducing the problem. We will appreciate your support.
- **View log files**
To reduce the log size of the UGSV SDK, the locally stored log files are encrypted, and the number of logs is limited. Therefore, to view the log content in plaintext, you need to use the log [decompression tool](http://dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py).
``` objc
  [TXLiveBase setConsoleEnabled:YES];
  [TXLiveBase setLogLevel:LOGLEVEL_DEBUG];
```

### Step 5. Compile and run

If the previous steps are correctly performed, the `HelloSDK` project will be compiled successfully. Run the application in `Debug` mode, and the SDK version information will be printed out in the Xcode Console:
```
2017-09-26 16:16:15.767 HelloSDK[17929:7488566] SDK Version = 5.2.5541
```

## Quick Integration of Feature Module
To help you quickly integrate SDK features, we provide `UGCKit`, a UI component library constructed based on the UGSV SDK.

You can get `UGCKit` in the `Demo/TXLiteAVDemo/UGC/UGCKit` directory of the SDK package available at [GitHub](https://github.com/tencentyun/UGSVSDK/tree/master/iOS) or [SDK Download](https://intl.cloud.tencent.com/document/product/1069/37914).

### UGCKit development environment requirements
- Xcode 10 or above.
- iOS 9.0 or above.

### Step 1. Integrate UGCKit 
1. **Import `UGCKit` and `BeautyPannel (BeautySettingKit)`**
	1. Copy the `Demo/TXLiteAVDemo/UGC/UGCKit` folder to the project directory and drag `UGCKit.xcodeproj` in `UGCKit` to the project.
	2. Copy the `Demo/TXLiteAVDemo/BeautySettingKit` folder to the project directory and drag `TCBeautyPanel.xcodeproj` in `BeautySettingKit` to the project.
![](https://main.qcloudimg.com/raw/48fa8833ea243bba61eec09bbdb38d33.png)
2. **Configure dependencies**   
Click the project target, select the "Build Phases" tab, click "+" in "Dependencies", select `UGCKit.framework`, `UGCKitResources`, `TCBeautyPanel.framework`, and `TCBeautyPanelResources`, and click **Add**.
![](https://main.qcloudimg.com/raw/098808d270672bd4413fbca2d92b7e4a.png)
3. **Link `UGCKit.framework` and `TCBeautyPannel.framework` to the SDK**
  1. Click the project target, select the "Build Phases" tab, click "+" in "Link Binary With Libraries", and select `UGCKit.framework` and `TCBeautyPannel.framework` to add them.
![](https://main.qcloudimg.com/raw/ccbc89f8a0ff68ac4e9159c9388070b7.png)
  2. Open the SDK directory in Finder and drag the SDK to "Link Binary With Libraries", or find the corresponding directory of the SDK in Xcode and add it by clicking "Add files" as shown below.
![](https://main.qcloudimg.com/raw/8432ca1427b51e65ff40e10bb460bbf9.png)
  3. Drag `FilterResource.bundle` in the `TXLiteAVDemo/App/Resource` directory to the project and check "App Target".
4. **Import the resources**
	1. Click the project target, select the "Build Phases" tab, and expand "Copy Bundle Resources".
	2. Expand `UGCKit.xcodeproj` and `Products` in the left directory in sequence, drag `UGCKitResources.bundle` to "Copy Bundle Resources", and expand `TCBeautyPannel.xcodeproj` and `Products` in sequence.
	3. Drag `TCBeautyPanelResources.bundle` to "Copy Bundle Resources".
![](https://main.qcloudimg.com/raw/6377d1c7b240e008f240d116e5363a8b.png)
5. **Import Enterprise Edition resources (applicable only to Enterprise Edition)**
Drag the `EnterprisePITU` folder (in the `App/AppCommon` directory) in the ZIP package of the Enterprise Edition SDK to the project, select "Create groups", check your target, and click **Finish**.

### Step 2. Use UGCKit

1. **Shoot**
`UGCKitRecordViewController` provides a complete set of shoot features. You just need to instantiate this controller and display it on the page.
```
UGCKitRecordViewController *recordViewController = [[UGCKitRecordViewController alloc] initWithConfig:nil theme:nil];
[self.navigationController pushViewController:recordViewController]
```
The shoot result will be called back through the completion block. The following is a sample result:
```
   recordViewController.completion = ^(TCUGCResult *result) {
       if (result.error) {
           // An error occurred while shooting
          [self showAlertWithError:error];
       } else {
           if (result.cancelled) {
               // The user canceled shoot and exited the shoot page
               [self.navigationController popViewControllerAnimated:YES];
          } else {
               // The shoot is successful. The result will be used for subsequent processing.
               [self processRecordedVideo:result.media];
           }
       }
   };
```
2. **Editing**
`UGCKitEditViewController` provides a complete set of image transition and video editing features. You need to pass in the media object to be edited during instantiation. The following uses shoot result processing as an example:
```
   - (void)processRecordedVideo:(UGCKitMedia *)media {
       // Instantiate the editing controller
       UGCKitEditViewController *editViewController = [[UKEditViewController alloc] initWithMedia:media conifg:nil theme:nil];
       // Display the editing controller
       [self.navigationController pushViewController:editViewController animated:YES];
```
The editing result will be called back through the completion block. The following is a sample result:
```
       editViewController.completion = ^(TCUGCResult *result) {
       if (result.error) {
           // Error
          [self showAlertWithError:error];
       } else {
           if (result.cancelled) {
               // The user canceled editing and exited the editing page
               [self.navigationController popViewControllerAnimated:YES];
          } else {
               // The editing result is saved successfully, which will be used for subsequent processing
               [self processEditedVideo:result.path];
           }
       }
   }
```
3. **Select a video or image from the album**
`UGCKitMediaPickerViewController` is used to select and splice media files. If multiple video files are selected, a spliced video file will be returned as follows:
```
   // Initialize the configuration
   UGCKitMediaPickerConfig *config = [[UGCKitMediaPickerConfig alloc] init];
   config.mediaType = UGCKitMediaTypeVideo;// Select the video
   config.maxItemCount = 5;                // Up to five ones can be selected

   // Instantiate the media selector
   UGCKitMediaPickerViewController *mediaPickerViewController = [[UGCKitMediaPickerViewController alloc] initWithConfig:config theme:nil];
   // Display the media selector
   [self presentViewController:mediaPickerViewController animated:YES completion:nil];
   ```
   The selection result will be called back through the completion block. The following is a sample result:
   ```
   mediaPickerViewController.completion = ^(UGCKitResult *result) {
     if (result.error) {
         // Error
         [self showAlertWithError:error];
     } else {
          if (result.cancelled) {
               // The user canceled selection and exited the selector page
               [self dismissViewControllerAnimated:YES completion:nil];
          } else {
               // The selection result is saved successfully, which will be used for subsequent processing
               [self processEditedVideo:result.media];
          }
     }
   }
```
4. **Clipping**
`UGCKitCutViewController` provides a video clipping feature. Just like that in the editing API, you only need to pass in the media object during instantiation and process the clipping result in `completion` as follows:
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
   

## Detailed Description
The following is the detailed description of each SDK module:

- [Video shoot](https://intl.cloud.tencent.com/document/product/1069/38007)
- [Video editing](https://intl.cloud.tencent.com/document/product/1069/38013)
- [Video splicing](https://intl.cloud.tencent.com/document/product/1069/38014)
- [Video upload](https://intl.cloud.tencent.com/document/product/1069/38016)
- [Video playback](https://intl.cloud.tencent.com/document/product/1069/38017)
- [Animated effects and face changing (Enterprise Edition)](https://intl.cloud.tencent.com/document/product/1069/38030)

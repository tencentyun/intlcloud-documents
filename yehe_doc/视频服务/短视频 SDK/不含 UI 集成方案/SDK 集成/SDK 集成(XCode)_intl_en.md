## Supported Platforms
The SDK is supported on iOS 8.0 or later.

## Environment Requirements
+ Xcode 9 or later
+ iOS 12.0 or later

## Directions
[](id:step1)
### Step 1. Link the SDK and system libraries
Decompress the downloaded SDK resource package and copy the framework files whose filename starts with `TXLiteAVSDK\_` (such as `TXLiteAVSDK_UGC.framework`) in the SDK folder to the project folder and drag them to the project.
1. Integrate the libraries based on your SDK version:
<dx-tabs>
::: For TXLiteAVSDK on v9.5 or earlier, add the integrated libraries
1. Select the project target and add the following integrated libraries:[](id:9_5)
	- Accelerate.framework
	- SystemConfiguration.framework
	- libc++.tbd
	- libsqlite3.tbd
2. Then, the project library dependency is as shown below:
![](https://main.qcloudimg.com/raw/a5fe16ca046a0aad84224e1ffa766a42.jpg)
:::
::: For TXLiteAVSDK 10.0 or later, add the system libraries
1. Select the project target and add the following system libraries:[](id:10_0)
  - Accelerate.framework
  - SystemConfiguration.framework
  - libc++.tbd
  - libsqlite3.tbd
  - MetalKit.framework
  - VideoToolbox.framework
  - ReplayKit.framework
  - GLKit.framework
  - OpenAL.framework
  - CoreServices.framework
2. In **Build Phases**, add the following dynamic libraries to **Link Binary With Librares** in the SDK directory:
 - TXFFmpeg.xcframework
 - TXSoundTouch.xcframework
3. Add the following frameworks in **Embed Frameworks** and select **Code Sign On Copy**:
 - TXFFmpeg.xcframework
 - TXSoundTouch.xcframework
:::
</dx-tabs>
2. Select the project target, search for `bitcode` in **Build Settings** and set **Enable Bitcode** to **NO**.


[](id:step2)
### Step 2. Configure app permissions
The app needs access to the photo album, which can be configured in `Info.plist`. Right-click `Info.plist`, select **Open as** > **Source Code**, and copy and modify the code below.
```
<key>NSAppleMusicUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your media library to obtain music files. It cannot add music if you deny it access.</string> 
<key>NSCameraUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your camera to be able to shoot video.</string> 
<key>NSMicrophoneUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your mic to be able to shoot videos with audio.</string> 
<key>NSPhotoLibraryAddUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your photo album to save edited video files.</string> 
<key>NSPhotoLibraryUsageDescription</key> 
<string>Video Cloud Toolkit needs to access your photo album to edit your video files.</string> 
```

[](id:step3)
### Step 3. Configure the license and get basic information
Follow the steps in [License Application](https://intl.cloud.tencent.com/document/product/1069/38041) to apply for a license, and copy the key and license URL in the [console](https://console.cloud.tencent.com/vod/license).
![](https://main.qcloudimg.com/raw/7bbf7fb9e3d13944bc3b6823fd786269.png)
2. Before you integrate UGSV features into your application, we recommend you set `- [AppDelegate application:didFinishLaunchingWithOptions:]` as follows:
```objectivec
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

>?If you use a **license for the SDK on v4.7** and have upgraded the SDK to v4.9, you can click **Switch to New License** in the console to generate a new license key and URL. A new license can be used only for the SDK on v4.9 or later and should be configured as described above.

[](id:step4)
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
[](id:step5)
### Step 5. Build and run the project
If the above steps are performed correctly, you will be able to successfully compile the `HelloSDK` project. Run the app in the debug mode, and the following SDK version information will be printed in the Xcode console:
```
2017-09-26 16:16:15.767 HelloSDK[17929:7488566] SDK Version = 5.2.5541
```

## Quick Integration of Feature Module
UGCKit is a UI component library built based on the UGSV SDK. It helps you quickly integrate different features of the SDK.

You can find UGCKit in `Demo/TXLiteAVDemo/UGC/UGCKit` of the SDK package, which you can download at [GitHub](https://github.com/tencentyun/UGSVSDK/tree/master/iOS) or [here](https://intl.cloud.tencent.com/document/product/1069/37914).

### UGCKit development environment requirements
- Xcode 10 or later
- iOS 9.0 or later

[](id:UGCKit_step1)
### Step 1. Integrate UGCKit 

1. Use CocoaPods in your project and, based on your actual conditions, do either of the following:
  - In the root directory of your project, run `pod init && pod install` to get the Podfile.
  - Copy the **UGCKit** folder to the project root directory (the directory of the Podfile).
2. Open the Podfile and add the following:
```
pod 'UGCKit', :path => 'UGCKit/UGCKit.podspec', :subspecs => ["UGC"]   #subspecs Choose according to your SDK
```
3. To integrate basic beauty filters, copy the **BeautySettingKit** folder to the project root directory (the directory of the Podfile) and add the following to the Podfile:
```
pod 'BeautySettingKit', :path => 'BeautySettingKit/BeautySettingKit.podspec'
```
4. To integrate the Tencent Effect SDK, copy the **xmagickit** folder to the project root directory (the directory of the Podfile) and add the following to the Podfile:
```
pod 'xmagickit', :path => 'xmagickit/xmagickit.podspec'
```
5. Run **pod install** and open `project name.xcworkspace`. You will find `UGCKit`, `BeautySettingKit`, and `magickit` in the `Pods/Development Pods` directory.

[](id:UGCKit_step2)
### Step 2. Use UGCKit
1. **Shooting**
`UGCKitRecordViewController` provides the video shooting feature. To enable the feature, just instantiate the controller and display it in the UI.
```objectivec 
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
```
2. **Editing**
   `UGCKitEditViewController` provides the slideshow making and video editing features. During instantiation, you need to pass in the media object to be edited. Below is an example that involves the editing of a shooting result:
```objectivec 
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
```
3. **Selecting video or image from photo album**
	1. `UGCKitMediaPickerViewController` is used to select and splice media files. If multiple video files are selected, a spliced video file will be returned as follows:
```objectivec 
// Configure initialization.
UGCKitMediaPickerConfig *config = [[UGCKitMediaPickerConfig alloc] init];
config.mediaType = UGCKitMediaTypeVideo;//Select videos.
config.maxItemCount = 5;                // Up to five can be selected.

// Instantiate the media picker view controller.
UGCKitMediaPickerViewController *mediaPickerViewController = [[UGCKitMediaPickerViewController alloc] initWithConfig:config theme:nil];
// Display the media picker view controller.
[self presentViewController:mediaPickerViewController animated:YES completion:nil];
```
	2. The selection result will be called back through the completion block. The following is a sample result:
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
```
4. **Clipping**
   `UGCKitCutViewController` provides the video clipping feature. As with the editing API, you need to pass in a media project when instantiating the controller and process clipping results in `completion`.
```objectivec 
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


## Module Description
Read the documents below to learn more about different modules of the SDK.

- [Video shooting](https://intl.cloud.tencent.com/document/product/1069/38007)
- [Video editing](https://intl.cloud.tencent.com/document/product/1069/38013)
- [Video splicing](https://intl.cloud.tencent.com/document/product/1069/38014)
- [Video uploading](https://intl.cloud.tencent.com/document/product/1069/38016)
- [Playback](https://intl.cloud.tencent.com/document/product/1069/38017)

## Overview
**To accurately measure the message reach rate and receive rich media messages**, the SDK provides the Service Extension API that can be called by the client to listen on message arrivals and receive rich media messages. You can use this feature in the following steps:

## Creating a Notification Service Extension Target
1. In the Xcode menu bar, choose **File** > **New** > **Target**.
>?
> - The bundle ID of the primary project must be different from that of the service, and the latter must be prefixed with the former (for example, the former is `com.tencent.tpns` and the latter is `com.tencent.tpns.service`).
> - If the lowest version supported by the target of the primary project is below 10.0, set the extension target system version to 10.0.
> - If the lowest version supported by the target of the primary project is above 10.0, the extension target system version should be the same as the primary project target version.
> 
![](https://main.qcloudimg.com/raw/d742074e3e3814cd449d2b0871a66b4c.png)
2. Go to the **Target** page, select **Notification Service Extension**, and click **Next**.  
![](https://main.qcloudimg.com/raw/329e2575a43a5bb168bb958df16b6110.jpg)
3. Set **Product Name** and click **Finish**.
![](https://main.qcloudimg.com/raw/3cb4636238cf51b60afb9f5d05874077.png)

## Adding TPNS Extension Libraries (Three Methods)
### Method 1: Integrate through CocoaPods
Download through CocoaPods:
``` 
pod 'TPNS-iOS-Extension', '~> Version'  // If the version is not specified, the latest version of the local pod TPNS-iOS-Extension will be downloaded.
```
**Use instructions**:
1. Create a `Notification Service Extension` target in `Application Extension` type, such as `XXServiceExtension`.
2. Add the configuration item of `XXServiceExtension` in the Podfile.
The display effect after the configuration item is added in the Podfile is as shown below:
```
target `XXServiceExtension'do
     platform:ios,'10.0'
     pod 'TPNS-iOS-Extension' , '~>1.2.7.2' 
end
```
>? We recommend that you use TPNS-iOS-Extension together with the pod 'TPNS-iOS' of version 1.2.7.2 or above.
>


### Method 2: Manually integrate

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. On the left sidebar, choose **Toolbox** > **[SDK Download](https://console.cloud.tencent.com/tpns/sdkdownload)**.
3. On the **SDK Download** page, select the iOS platform and click **Download**.
4. Decompress the SDK package, go to the `demo` > `sdk` > `XGPushStatistics` > `extension` directory, and obtain the `XGExtension.h` and `libXGExtension.a` files.
5. Add the `XGExtension.h` and `libXGExtension.a` files obtained to the notification service extension target:
 - System libraries: `libz.tbd`
 - TPNS extension library: libXGExtension.a

After the integration, the directory structure is as follows:
 ![](https://main.qcloudimg.com/raw/4dcaaf779121fa80cb33e7f78e558a09.png)

### Method 3: Integrate through HomeBrew

To install `new_tpns_svc_ext` for the first time, please run the following command in the terminal:
1. Associate the`TPNS homebrew` repository.  
```plaintext
brew tap tpns/serviceExtension https://github.com/TencentCloud/homebrew-tpnsServiceExtension.git
```
2. Install `new_tpns_svc_ext`.  
```plaintext
brew install new_tpns_svc_ext
```
3. Install the TPNS notification service extension plugin.  
```plaintext
new_tpns_svc_ext  "AccessID" "AccessKey" "xxx.xcodeproj"
```

**Parameter description:**  
- AccessID: `AccessID` of your Tencent Cloud TPNS product  
- AccessKey: `AccessKey` of your Tencent Cloud TPNS product  
- xxx.xcodeproj: full path of `.xcodeproj`  

#### Sample
```
new_tpns_svc_ext "1600013400" "IWRNAHX6XXK6" "/Users/yanbiaomu/Developer/tencent/demo2/SDKToolObjcDemo2/SDKToolObjcDemo2.xcodeproj"
```
>? To get `AccessID` and `AccessKey`, go to the [TPNS console](https://console.cloud.tencent.com/tpns), choose **Product Management**, and click **Configuration Management** in the record of a target product. Then you can find `AccessID` and `AccessKey` on the page displayed.  
>  ![](https://main.qcloudimg.com/raw/841fa8076620fa64d952eeb366f429c0.png)
> 
4. Run the `new_tpns_svc_ext` command to verify the result.    
If the following result is displayed after the `new_tpns_svc_ext` command is run in the terminal, the notification extension plugin is successfully integrated.  
```plaintext
TPNS service auto coding done!
New TPNSService Extension Success
```

#### Upgrading `new_tpns_svc_ext`

When a new version of the SDK notification extension plugin is released, you can run the following command in the terminal for upgrade:
``` plaintext
brew update && brew reinstall new_tpns_svc_ext
```
>?
> - You can view the release notes of the latest version in [SDK for iOS](https://intl.cloud.tencent.com/document/product/1024/36192).
> - Currently, the HomeBrew command `new_tpns_svc_ext` supports integrating only the notification service extension plugin `TPNSService` but not basic push capabilities.
>

## Plugin Use Directions
### Calling the SDK's statistics reporting API

1. Import the header file `NotificationService` into the notification extension class `XGExtension.h`.
2. Call the following sample code in the callback method `didReceiveNotificationRequest:withContentHandler`:

```
objective-c
/**
 @brief //TPNS processes rich media notifications and device-reached messages, that is, message receipts.
 @param request //Push request
 @param accessID //TPNS application `AccessID`
 @param accessKey //TPNS application `AccessKey`
 @param handler //Callback of processing messages. Process the associated rich media file in the callback method.
 */
  - (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request
                           accessID:(uint32_t)accessID
                           accessKey:(nonnull NSString *)accessKey
                   contentHandler:(nullable void (^)(NSArray<UNNotificationAttachment *> *_Nullable attachments, NSError *_Nullable error))handler;
```

#### Sample code

```Objective-C
- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent *_Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
	 /// For clusters outside Guangzhou, please enable the corresponding cluster configuration (not required for clusters in Guangzhou)
    //    [XGExtension defaultManager].reportDomainName = @"tpns.hk.tencent.com"; /// Cluster in Hong Kong (China)
    //    [XGExtension defaultManager].reportDomainName = @"tpns.sgp.tencent.com";  /// Cluster in Singapore
    //  [XGExtension defaultManager].reportDomainName = @"tpns.sh.tencent.com";  /// Cluster in Shanghai
    [[XGExtension defaultManager] handleNotificationRequest:request accessID:<your accessID> accessKey:<your accessKey
		> contentHandler:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error) {
        self.bestAttemptContent.attachments = attachments;
        self.contentHandler(self.bestAttemptContent);  // If you need to add business logic before the notification pops up, add it before calling ContentHandler.
    }];
}
```

## Integration Verification

After completing the integration as instructed above, you can verify whether the extension plugin is successfully integrated in the following steps:
1. Close the application and push a notification message to the phone.
2. Without clicking the message, check whether the message arrives on the phone in the console.
If there is arrival data, the integration is successful.

### Debugging
If the device receives the pushed message but there is no arrival data, troubleshoot as follows:
1. Run the primary target (demo example in the figure).
![](https://main.qcloudimg.com/raw/668c47734af4f25b087fbcc33a29d6ec.png)
2. Attach the implementation target (TPNSService-Cloud in the demo) of `UNNotificationServiceExtension` to the primary target by `PID` or `Name`.
![](https://main.qcloudimg.com/raw/e5d7615ad9c6379be595299bc5a2b651.png)
3. Add breakpoints at code lines 34 and 38 as shown in the figure, and send a notification for debugging. Note that the notification must be sent through the APNs channel and that the `mutable-content` field in the notification content must be `1` (since TPNS SDK v1.2.8.0, the APNs channel is used by default in the background, and the TPNS channel is used in the foreground. To debug the notification service extension plugin, you need to make the application run in the background). If the breakpoints are executed, the debugging is successful. Otherwise, stop all targets and start over from step 1.
![](https://main.qcloudimg.com/raw/1667c3db7b2486ea45675cb2036da018.png)

## FAQ

#### Why is there no arrival report after I sent a notification?
The notification service extension plugin must be integrated for client arrival reporting. If no arrival data is reported after integration, check whether `AccessID` and `AccessKey` of the primary project are consistent with those of the notification service extension plugin and whether the `mutable-content` field in the notification content in the web console or RESTful API is `1`.
Only when the two conditions checked are met, the notification service extension plugin on the client will be run, and arrival data will be reported.


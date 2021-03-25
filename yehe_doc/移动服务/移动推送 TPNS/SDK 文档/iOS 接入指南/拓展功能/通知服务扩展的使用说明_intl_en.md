## Overview
To **accurately count the message reach rate and receive rich media messages**, the SDK provides the Service Extension API that can be called by the client to listen on message arrivals and receive rich media messages. You can use this feature in the following steps:

## Creating a Notification Service Extension Target
1. In the Xcode menu bar, choose **File** > **New** > **Target**.
>?
>- The bundle ID of the primary project must be different from that of the service, and the latter must be prefixed with the former (for example, the former is `com.tencent.tpns` and the latter is `com.tencent.tpns.service`).
>- If the lowest version supported by the target of the primary project is below 10.0, set the extension target system version to 10.0.
>- If the lowest version supported by the target of the primary project is above 10.0, the extension target system version should be the same as the primary project target version.

 ![](https://main.qcloudimg.com/raw/d742074e3e3814cd449d2b0871a66b4c.png)
2. Go to the **Target** page, select **Notification Service Extension**, and click **Next**.  
![](https://main.qcloudimg.com/raw/329e2575a43a5bb168bb958df16b6110.jpg)
3. Set **Product Name** and click **Finish**.
![](https://main.qcloudimg.com/raw/3cb4636238cf51b60afb9f5d05874077.png)

## Adding TPNS Extension Libraries (Three Methods)
### Method 1: integrate through CocoaPods
Download through CocoaPods:

``` 
pod 'TPNS-iOS-Extension', '~> Version'  // If the version is not specified, the latest version of the local pod TPNS-iOS-Extension will be downloaded.
```
 **Use instructions**:
1. Create a `Notification Service Extension` target of `Application Extension` type, such as `XXServiceExtension`.
2. Add the configuration item of `XXServiceExtension` to the Podfile.
The display effect after the configuration item is added to the Podfile is as shown below:
```
target `XXServiceExtension'do
     platform:ios,'10.0'
     pod 'TPNS-iOS-Extension' , '~>1.2.7.2' 
end
```

>? We recommend that you use TPNS-iOS-Extension together with the pod 'TPNS-iOS' of version 1.2.7.2 or above.


### Method 2: manually integrate
Select the notification extension target and add the following dependent library files:
 - System libraries: `libz.tbd`, `libsqlite3.tbd`
 - TPNS extension library: libXGExtension.a![](https://main.qcloudimg.com/raw/7587b8d1f108828b6289b402124b200b.jpg)

### Method 3: integrate through HomeBrew

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
>?To get `AccessID` and `AccessKey`, go to the [TPNS console](https://console.cloud.tencent.com/tpns), choose **Product Management**, and click **Configuration Management** for a target product. Then you can find `AccessID` and `AccessKey` on the page displayed.  
![](https://main.qcloudimg.com/raw/f2d19a1e226a8e09d474b0060097ea92.png)  

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
>- You can view the release notes of the latest version in [SDK for iOS](https://intl.cloud.tencent.com/document/product/1024/36192).
>- Currently, the HomeBrew command `new_tpns_svc_ext` supports integrating only the notification service extension plugin `TPNSService` but not basic push capabilities.

## Plugin Use Directions
### Calling the SDK's statistics reporting API

1. Import the header file `XGExtension.h` into the notification extension class `NotificationService`.
2. Call the following sample code in the callback method `didReceiveNotificationRequest:withContentHandler`:
```objective-c
/**
 @brief //TPNS's processing of rich media notification and message arriving at device, i.e., message receipt
 @param request //Push request
 @param accessID //TPNS application `AccessID`
 @param accessKey //TPNS application `AccessKey`
 @param handler //Callback for message processing. The associated rich media file is processed in the callback method
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

#### Arrival statistics
Close the application and push a notification message to the phone. Without clicking the message, check in the console whether it arrives. If there is arrival data, the integration is successful.
![](https://main.qcloudimg.com/raw/cd46e9a775297504ebdab7894edd478c.png)

#### Pushing rich media messages
Close the application, push a rich media message with an image, and check whether the image is displayed when the message arrives on the phone. If it is not displayed, you can troubleshoot as follows:
1. Select **Service Target**, make sure that the target's system version is lower than that of the device, and click the **Run** icon.
![](https://main.qcloudimg.com/raw/1552db45877985ac4bd77e999e01bf8b.png)
2. Select the primary target to mount.
![](https://main.qcloudimg.com/raw/fa75c25c94a9504564f0ea071c7b9a3d.png)
3. Select the notification extension class, add the related print log, and check the print result. If an attachment (rich media push) is returned normally and `error` is `nil`, the push is successful.
![](https://main.qcloudimg.com/raw/0c112c909acff11af75b317a0f97fb77.png)

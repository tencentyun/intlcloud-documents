## Overview
To **accurately count the message reach rate and receive rich media messages**, the SDK provides the Service Extension API that can be called by the client to listen on message arrivals and receive rich media messages. You can follow the instructions below to use this feature.

## Creating Notification Extension Target
1. In the Xcode menu bar, select **File** > **New** > **Target**.
>?
>- The Bundle Id of the Project and Service must be different. The Service Bundle Id must be prefixed with the Project Bundle Id. For example, Project Bundle Id is com.tencent.tpns, and Service Bundle Id is com.tencent.tpns.service.
>- If the lowest version supported by the target of the primary project is below 10.0, set the extension target system version to v10.0.
>- If the lowest version supported by the target of the primary project is above 10.0, the extension target system version should be the same as the primary project target version.

 ![](https://main.qcloudimg.com/raw/d742074e3e3814cd449d2b0871a66b4c.png)
2. Enter the "Target" page, select **Notification Service Extension**, and click **Next**.  
![](https://main.qcloudimg.com/raw/329e2575a43a5bb168bb958df16b6110.jpg)
3. Set "Product Name" and click **Finish**.
![](https://main.qcloudimg.com/raw/3cb4636238cf51b60afb9f5d05874077.png)

## Adding TPNS Extension Library (Two Methods)
### Method 1. Import through CocoaPods
Download through Cocoapods:

``` 
pod 'TPNS-iOS-Extension' 
```
 **Note:**
1. Create a `Notification Service Extension` target in `Application Extension` type, such as `XXServiceExtension`.
2. Add the configuration item of `XXServiceExtension` in Podfile.
**Sample**
Display effect after the configuration item is added in Podfile:
```
target ‘XXServiceExtension'do
pod 'TPNS-iOS-Extension' , '~>1.2.7.2' 
end
```

>? We recommend you use it together with pod 'TPNS-iOS' version 1.2.7.2 or above.


### Method 2. Import manually
Select the notification extension target and add the following dependent library files:
 - Add system libraries: libz.tbd, libsqlite3.tbd
 - Add the TPNS extension library: libXGExtension.a![](https://main.qcloudimg.com/raw/7587b8d1f108828b6289b402124b200b.jpg)
 
## Directions
### Calling SDK's statistics reporting API
Report on the receipt of push messages. This API is used to track statistics of whether push messages reach devices.
```objective-c
/**
 @brief   TPNS's processing of rich media notification and message arriving at device, i.e., message receipt

 @param request   Push request
 @param accessID   TPNS application `accessId`
 @param accessKey   TPNS application `accessKey`
 @param handler   Callback for message processing. The associated rich media file is processed in the callback method
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
    /// For clusters outside Mainland China, please enable the corresponding cluster configuration (not required for clusters in Mainland China)
//    [XGExtension defaultManager].reportDomainName = @"tpns.hk.tencent.com"; /// Cluster in Hong Kong (China)
//    [XGExtension defaultManager].reportDomainName = @"tpns.sgp.tencent.com";  /// Cluster in Singapore
    [[XGExtension defaultManager] handleNotificationRequest:request accessID:<your accessID> accessKey:<your accessKey
		> contentHandler:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error) {
        self.bestAttemptContent.attachments = attachments;
        self.contentHandler(self.bestAttemptContent);
    }];
}
	```

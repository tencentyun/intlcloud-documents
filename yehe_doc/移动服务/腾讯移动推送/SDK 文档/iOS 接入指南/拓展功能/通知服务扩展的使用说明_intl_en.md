## Overview
To collect precise statistics of message arrivals and receive rich media messages, the SDK provides a Service Extension API, which can be called by the client to listen on the arrivals of messages and receive rich media messages. You can use it as follows:

## Creating Notification Extension Target
1. In the Xcode menu bar, select **File** > **New** > **Target**.
2. Enter the **Target** page, select **Notification Service Extension**, and click **Next**.  
![](https://main.qcloudimg.com/raw/329e2575a43a5bb168bb958df16b6110.jpg)
3. Enter **Product Name** and click **Finish**.
![](https://main.qcloudimg.com/raw/3cb4636238cf51b60afb9f5d05874077.png)

## Adding TPNS Extension Library (Two Methods)
### Method 1. Import through Cocoapods
Download through Cocoapods:

``` 
pod 'TPNS-iOS-Extension' 
```
 **Use instructions:**
1. Create a `Notification Service Extension` target in `Application Extension` type, such as `XXServiceExtension`.
2. Add the configuration item of `XXServiceExtension` in Podfile.
**Sample**
Display effect after the configuration item is added in Podfile:
```
target ‘XXServiceExtension'do
pod 'TPNS-iOS-Extension' , '~>1.2.7.1' 
end
```

>? You are recommended to use it together with pod 'TPNS-iOS' version 1.2.7.1 or above.


### Method 2. Import manually
Select the notification extension target and add dependent library files:
 - Add system libraries: libz.tbd, libsqlite3.tbd
 - TPNS extension library: libXGExtension.a![](https://main.qcloudimg.com/raw/7587b8d1f108828b6289b402124b200b.jpg)
 
## How to Use
### Calling SDK's statistics reporting API
Reporting on receipt of push messages. This API is used to track statistics of whether push messages reach devices.
```objective-c
/**
 @brief   the TPNS messages that arrive to the end terminal, that is, message receipt

 @param request   Push request
 @param accessID   TPNS application's `accessId`
 @param accessKey   TPNS application's `accessKey`
 @param handler   Process the associated rich media file in callback method.
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
    /// For clusters outside mainland china, please enable the corresponding cluster configuration (not required for clusters in Mainland China)
//    [XGExtension defaultManager].reportDomainName = @"tpns.hk.tencent.com"; /// Cluster in Hong Kong (China)
//    [XGExtension defaultManager].reportDomainName = @"tpns.sgp.tencent.com";  /// Cluster in Singapore
    [[XGExtension defaultManager] handleNotificationRequest:request accessID:<your accessID> accessKey:<your accessKey
		> contentHandler:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error) {
        self.bestAttemptContent.attachments = attachments;
        self.contentHandler(self.bestAttemptContent);
    }];
}
	```

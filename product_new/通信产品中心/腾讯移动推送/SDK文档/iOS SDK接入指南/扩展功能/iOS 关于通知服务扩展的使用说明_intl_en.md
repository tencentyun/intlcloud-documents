
## Overview
In iOS 10.0+, the operating system provides the Service Extension API, which can be called by the client to listen to the arrival of messages.


## SDK statistics reporting APIs
Reporting on receipt of push messages. This API is used to track statistics of whether push messages reach devices.
```objective-c
/**
 @brief: The TPNS messages that arrive to the end terminal, that is, message receipt
 
 @param request: Push request
 @param appID: TPNS application ID
 @param appKey: TPNS application Key
 @param handler: process the associated rich media file in callback method.
 */
- (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request appID:(uint32_t)appID appKey:(nonnull NSString *)appKey contentHandler:(nullable void(^)( NSArray <UNNotificationAttachment *>* _Nullable attachments,  NSError * _Nullable error))handler;
```

### Parameter descriptions
- request: push request.
- AppID: TPNS application ID.
- handler: process the associated rich media file in callback method.  

## Instructions 
Perform the following steps to use the extension SDK:
1. In the xcode menu bar, select **File** > **New** > **Target**.
2. Enter the **Target** page, select **Notification Service Extension** and click **Next**.  
![](https://main.qcloudimg.com/raw/329e2575a43a5bb168bb958df16b6110.jpg)
3. Enter **Product Name** and click **Finish**.
![](https://main.qcloudimg.com/raw/3cb4636238cf51b60afb9f5d05874077.png)
4. Configure **Target** and add the dependent library files: libXGExtension.a, libz.tbd, libsqlite3.tbd.
![](https://main.qcloudimg.com/raw/7587b8d1f108828b6289b402124b200b.jpg)
5. Call the SDK statistics reporting API. Sample code is as follows:
	```Objective-C
	- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
			self.contentHandler = contentHandler;
			self.bestAttemptContent = [request.content mutableCopy];
			[[XGExtension defaultManager] handleNotificationRequest:request appID:<#appid#> appKey:<#appkey#>  contentHandler:^(NSArray<UNNotificationAttachment *> * _Nullable attachments, NSError * _Nullable error) {
					self.bestAttemptContent.attachments = attachments;
					self.contentHandler(self.bestAttemptContent);
			}];
	}
	```







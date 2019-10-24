

## iOS Extension SDK API (iOS 10+)

### Feature Description
In iOS 10.0+, the operating system provides the Service Extension API, which can be called by the client to listen to the arrival of messages.
**Receipt of push message reporting. This API is used to check if push messages reach the devices.**
SDK notification delivery access rate API
```objective-c
/**
  @brief    TPNS handles messages that reach the devices                         
  @note    The associated rich media file, you need to set the full URL address of its resources in the push frontend, and the file will be  downloaded automatically in the SDK.        
*/
  - (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request
  appID:(uint32_t)appID contentHandler:(nullable void(^)( NSArray
  <UNNotificationAttachment *>* _Nullable attachments,  NSError * _Nullable
  error))handler;
```
#### Parameter Description
request: Push request
appID: The TPNS app ID
handler: Receipt of message processing, the associated rich media file will be processed in callback  
**Use instructions:
Follow the steps below to use the extension SDK.**
1. In the xcode menu bar, select **File**>**New**. Select **Target**
2. Select **Notification Service Extension** and click **Next** 
![](https://main.qcloudimg.com/raw/1ef101e04b10ff75426b56ff7a612fc1.jpg)
3. Enter **Product Name** and click **Finish**
![](https://main.qcloudimg.com/raw/c197119c8c2c7b79406784f37817d6ff.png)
4. Configure **Target** and add the dependent library files: libXGExtension.a, libz.tbd, libsqlite3.tbd

![](https://main.qcloudimg.com/raw/fc4183349bd03bcde6ade639010f43bc.jpg)

3. Call the SDK notification delivery access rate API
**Sample**

```Objective-C
- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request
  withContentHandler:(void (^)(UNNotificationContent *
  _Nonnull))contentHandler {
      [[XGExtension defaultManager] handleNotificationRequest:request appID:
  <#your xg AppID#> contentHandler:nil];
      self.contentHandler = contentHandler;
      self.bestAttemptContent = [request.content mutableCopy];
      self.contentHandler(self.bestAttemptContent);
      }
```







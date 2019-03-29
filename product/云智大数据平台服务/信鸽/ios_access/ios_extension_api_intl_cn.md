** 本文档针对 iOS 信鸽 <font color="#FF0000"> SDK 3.1.0 及以上 </font>  版本 **

##iOS Extension SDK API (iOS 10+)
**上报推送消息回执，此接口的目的是统计推送消息是否抵达终端**
```objective-c
/**
  @brief   信鸽推送处理抵达到终端到消息            
  @param request   推送请求
  @param appID     信鸽应用ID
  @param handler   处理消息的回执，回调方法中处理关联的富媒体文件               
  @note            关联的富媒体文件，需要在推送前端设置资源的完整URL地址，SDK内部会自动下载        
*/
  - (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request
  appID:(uint32_t)appID contentHandler:(nullable void(^)( NSArray
  <UNNotificationAttachment *>* _Nullable attachments,  NSError * _Nullable
  error))handler;
```
**说明 ：
为了使用extension SDK，操作步骤如下：**
1.新增Target
![](/assets/iOSExtension/extension.jpg)

2.配置Target，添加依赖库文件：libXGExtension.a, libz.tbd, libsqlite3.tbd

![](/assets/iOSExtension/extensionConfig.jpg)
3.调用SDK统计上报接口
**示例**

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







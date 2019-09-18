

##iOS Extension SDK API (iOS 10+)

###功能说明
iOS 10.0+，操作系统提供了 Service Extension 接口，可供客户端调用，从而可以监听消息的到达。
**上报推送消息回执，此接口的目的是统计推送消息是否抵达终端**
SDK统计上报接口
```objective-c
/**
  @brief   信鸽推送处理抵达到终端到消息                         
  @note  关联的富媒体文件，需要在推送前端设置资源的完整URL地址，SDK内部会自动下载        
*/
  - (void)handleNotificationRequest:(nonnull UNNotificationRequest *)request
  appID:(uint32_t)appID contentHandler:(nullable void(^)( NSArray
  <UNNotificationAttachment *>* _Nullable attachments,  NSError * _Nullable
  error))handler;
```
####参数说明
request：推送请求
appID：信鸽应用ID
handler：处理消息的回执，回调方法中处理关联的富媒体文件  
**使用说明 ：
为了使用extension SDK，操作步骤如下：**
1.在 xcode 菜单栏选择File-> New,选择Target
2.选择 Notification Service Extension 点击 Next 
![](https://main.qcloudimg.com/raw/1ef101e04b10ff75426b56ff7a612fc1.jpg)
3.输入 Product Name，点击Finish
![](https://main.qcloudimg.com/raw/c197119c8c2c7b79406784f37817d6ff.png)
4.配置Target，添加依赖库文件：libXGExtension.a, libz.tbd, libsqlite3.tbd

![](https://main.qcloudimg.com/raw/fc4183349bd03bcde6ade639010f43bc.jpg)

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







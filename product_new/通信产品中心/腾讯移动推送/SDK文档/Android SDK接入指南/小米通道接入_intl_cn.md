## 操作场景
小米推送通道是由小米官方提供的系统级推送通道。在小米手机上，推送消息能够通过小米的系统通道抵达终端，并且无需打开应用就能够收到推送。

!
- 小米通道支持抵达回调，不支持点击回调，支持透传（但不保证到达）。
- 在测试小米通道推送消息时，应尽量避免使用“test”、“测试”等字眼，否则可能会被小米拦截进入“非重要消息”中。

## 操作步骤
### 获取密钥
进入 [小米开放平台](httpsdev.mi.comconsoleappservicepush.html) ，开通小米开发者账号，并获取小米推送的密钥。 更多详情请参见 [快速接入指南](httpsdev.mi.comconsoledocdetailpId=708)。



### 配置内容
#### 使用 jcenter 依赖接入
AS 开发建议使用 jcenter 依赖接入。引入小米推送的 jar 包。
```js
 implementation 'com.tencent.tpnsxiaomi[VERSION]-release'小米推送 [VERSION] 为当前SDK版本号,版本号可在SDK下载页查看
```




#### 使用 Eclipse 开发接入
1. 下载 [SDK 安装包](httpsconsole.cloud.tencent.comtpnssdkdownload)。
2. 打开 Other-Push-jar 文件夹， 导入小米推送相关 jar 包，将 xm4tpns1.1.2.1.jar 导入项目工程中。
3. 在配置好腾讯移动推送的基础上 ，新增小米推送的配置：
```xml
application
service
androidname=com.xiaomi.push.service.XMPushService
androidenabled=true
androidprocess=pushservice 
service
androidname=com.xiaomi.push.service.XMJobService
androidenabled=true
androidexported=false
androidpermission=android.permission.BIND_JOB_SERVICE
androidprocess=pushservice 
!-- 注：此service必须在3.0.1版本以后（包括3.0.1版本）加入 --
service
androidname=com.xiaomi.mipush.sdk.PushMessageHandler
androidenabled=true
androidexported=true 
service
androidname=com.xiaomi.mipush.sdk.MessageHandleService
androidenabled=true 
!-- 注：此service必须在2.2.5版本以后（包括2.2.5版本）加入 --
receiver
androidname=com.xiaomi.push.service.receivers.NetworkStatusReceiver
androidexported=true 
intent-filter
action androidname=android.net.conn.CONNECTIVITY_CHANGE 
category androidname=android.intent.category.DEFAULT 
intent-filter
receiver
receiver
androidname=com.xiaomi.push.service.receivers.PingReceiver
androidexported=false
androidprocess=pushservice 
intent-filter
action androidname=com.xiaomi.push.PING_TIMER 
intent-filter
receiver
application
!-- 注：小米push 需要的权限 begin --
permission
androidname=应用包名.permission.MIPUSH_RECEIVE
androidprotectionLevel=signature 
!-- 这里com.example.mipushtest改成app的包名 --
uses-permission androidname=应用包名.permission.MIPUSH_RECEIVE 
!-- 这里com.example.mipushtest改成app的包名 --
!-- 注：小米push 需要的权限 end --
```
3. 在 ```AndroidManifest.xml``` 增加 ```Receiver``` ，配置如下：
```xml
receiver
androidexported=true
androidname=com.tencent.android.mipush.XMPushMessageReceiver
intent-filter
action androidname=com.xiaomi.mipush.RECEIVE_MESSAGE 
intent-filter
intent-filter
action androidname=com.xiaomi.mipush.MESSAGE_ARRIVED 
intent-filter
intent-filter
action androidname=com.xiaomi.mipush.ERROR 
intent-filter
receiver
```

### 开启小米推送
设置小米 AppID 和 AppKey。

```java
XGPushConfig.setMiPushAppId(getApplicationContext(), APPID);
XGPushConfig.setMiPushAppKey(getApplicationContext(), APPKEY);
打开第三方推送
XGPushConfig.enableOtherPush(getApplicationContext(), true);


注册成功的日志如下
12-02 161732.299 12584-12584com.qq.xgdemo IXINGE [XGPushManager] Action - Register to xinge server
12-02 161732.996 12584-12584com.qq.xgdemo IXINGE [XGPushManager] Register call back to com.qq.xgdemo
12-02 161732.997 12584-12626com.qq.xgdemo IXINGE [XGPushManager] XG register push success with token  1d31bb3ea6185baebdf05dfc2e586dfe5dc41fb5
12-02 161733.001 12584-12626com.qq.xgdemo IXINGE [XGOtherPush] other push token is  YZQfRxmxdfNlbSKpNWCa3tM4Esnq6op4qeOsQO2qT88= other push type xiaomi
```

如需通过点击回调获取参数或者跳转自定义页面，可以通过使用 Intent 来实现。更多详情请参见 [Android 常见问题](httpscloud.tencent.comdocumentproduct54836674#.E5.A6.82.E4.BD.95.E8.AE.BE.E7.BD.AE.E6.B6.88.E6.81.AF.E7.82.B9.E5.87.BB.E4.BA.8B.E4.BB.B6.EF.BC.9F)。



### 代码混淆

```xml
-keep class com.xiaomi.{;}
-keep public class  extends com.xiaomi.mipush.sdk.PushMessageReceiver
```

混淆规则需要放在 App 项目级别的 proguard-rules.pro 文件中。



# FCM通道集成指南

## 操作场景

FCM 通道是谷歌推出的系统级推送通道，在外国可用谷歌service框架的手机上能够实现不打开应用收到推送消息。在没有fcm的手机rom下依旧走信鸽的推送通道。
## 操作步骤

### 1.获取FCM推送秘钥
1. [FireBase官网](https://firebase.google.com/?hl=en-us)注册应用信息。并将获取到的FCM应用推送服务器密钥和 SenderID，配置到信鸽的管理台。
2. 下载google-services.json 文件。
如图所示：

获取json文件：
![](https://main.qcloudimg.com/raw/a3b3fbb86180fde824d7970f00418513.png)
获取服务器密钥：
![](https://main.qcloudimg.com/raw/35e4dc46af79a52f4f200b1ef085f19f.png)

## 配置内容

1.配置google-services.json文件。如图所示：
![](https://main.qcloudimg.com/raw/60e855aaf46d86e8e32a057dc5a948f3.png)
2. 配置gradle,集成谷歌service.
a)在项目级的build.gradle文件中的dependencies节点中添加下面代码：
```xml
classpath 'com.google.gms:google-services:4.2.0'
```
**注：如果使用低于4.2.0版本出现FCM Register error! java.lang.IllegalStateException: Default FirebaseApp is not initialized in this process com.qq.xg4all. Make sure to call FirebaseApp.initializeApp(Context) first.  
解决：可以尝试在res/values文件夹下的string.xml加上
<string name="google_app_id">YOUR_GOOGLE_APP_ID</string>**

在应用级的build.gradle文件中添加依赖
```xml

implementation 'com.tencent.tpns:fcm:[VERSION]-release' [VERSION] is the current SDK version number. You can view the SDK version number on the SDK download page 

implementation  'com.google.firebase:firebase-messaging:17.6.0'



 //在应用级的gradle文件的最后一行代码中新增并将google-services.json放进你应用model的根路径下

apply plugin: 'com.google.gms.google-services'

```
**注：Google配置google-play-services（信鸽只用到了检测设备是否支持google service功能，要求版本最好大于17.0.0,较低版本有可能出现无法注册fcm风险）：参考文档https://developers.google.com/android/guides/setup#add_google_play_services_to_your_project**


## 启用FCM推送


在调用信鸽注册代码（XGPushManager.registerPush）前面添加以下代码设置

```java
XGPushConfig.enableOtherPush(this, true);
```
注册FCM成功的日志如下：

```xml
 E/XG_fcm: Fcm App has initialize 
 D/XG_fcm: FirebaseAPP初始化完成
 I/XG_fcm: registerPush Token is: eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI
12-02 09:16:31.877 17260-17260/lc.com.xinge.push W/FA: Service connection failed: ConnectionResult{statusCode=SERVICE_VERSION_UPDATE_REQUIRED, resolution=null, message=null}
12-02 09:16:31.892 17260-17278/lc.com.xinge.push V/FA: Using measurement service
12-02 09:16:31.893 17260-17278/lc.com.xinge.push V/FA: Connecting to remote service
12-02 09:16:31.895 17260-17423/lc.com.xinge.push I/XINGE: [XGOtherPush] Reservert info: other push token is : eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI  other push type: fcm
```


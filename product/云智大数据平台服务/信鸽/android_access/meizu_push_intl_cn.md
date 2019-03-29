# 魅族推送通道集成指南

魅族推送通道是由**魅族官方提供**的系统级推送通道。在魅族手机上，推送消息能够通过魅族的系统通道抵达终端，并且无需打开应用就能够收到推送。

**\[注意事项\]**

1. 魅族推送通道通知标题不超过32字符，通知内容不超过100字符

2. 魅族推送通道不支持透传消息

## 获取魅族推送密钥

1.打开[魅族推送官网](https://open.flyme.cn/open-web/views/push.html)

2.注册/登录开发者账号。（如果您是新注册账号，进行实名认证大约需要2天左右时间，具体请咨询魅族侧）

3.在魅族推送平台（[http://push.meizu.com）](http://push.meizu.com）) 中新建应用。注意「应用包名」需跟您在信鸽填写的包名保持一致

4.获取应用相关的信息，并且将这些信息复制，填入信鸽管理台“应用配置”-“厂商&海外通道”栏目，这些信息是AppID，AppKey，AppSecret

![](/assets/魅族图片.png)

注：更多详情请参照[魅族开发文档](http://open.res.flyme.cn/fileserver/upload/file/201709/a271468fe23b47408fc2ec1e282f851f.pdf)

5.在信鸽管理台-应用配置-厂商&海外通道处-魅族推送通道处，将相关推送密钥填入。

## 集成方式

### AndroidStudio集成方式



```js
/* 魅族 3.2.7-Release版
 * 注意：若魅族通道使用此版本,则信鸽sdk版本也需要同时使用v3.2.7-Release
 */
 compile 'com.tencent.xinge:xgmz:3.2.7-Release'
/* 魅族 3.2.8-release版
 * 注意：若魅族通道使用此版本,则信鸽sdk版本也需要同时使用v4.0.5
 */
 compile 'com.tencent.xinge:xgmz:3.2.8-release'
```

### Eclipse集成方式

1.将魅族通道所需要的jar包（pushsdk-3.3.170110.jar）导入libs目录下：

2.在Androidmanifest下配置一下配置：

```xml
<application>
<service
    android:name="com.meizu.cloud.pushsdk.NotificationService"
     android:exported="true"/>

<receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
     <intent-filter>
      <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START"/>
      <category android:name="android.intent.category.DEFAULT" />
     </intent-filter>
 </receiver>
</application>

 <!-- 注：魅族push 需要的权限 begin -->
 <!-- 兼容flyme5.0以下版本，魅族内部集成pushSDK必填，不然无法收到消息-->

  <uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>

  <permission android:name="应用包名.push.permission.MESSAGE" 

                   android:protectionLevel="signature"/>

  <uses-permission android:name="应用包名.push.permission.MESSAGE"></uses-permission>

  <!--  兼容flyme3.0配置权限-->

  <uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />

  <permission android:name="应用包名.permission.C2D_MESSAGE"

              android:protectionLevel="signature">
  </permission>

  <uses-permission android:name="应用包名.permission.C2D_MESSAGE"/>

<!-- 注：魅族push 需要的权限 end -->
```

#### 魅族消息receiver

在 ```AndroidManifest.xml``` 增加自定义 ```Receiver``` 配置如下：

```xml
<receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver">
    <intent-filter>
        <!-- 接收push消息 -->
        <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
        <!-- 接收register消息-->
         <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK"/>
        <!-- 接收unregister消息-->
         <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK"/>

         <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
         <action android:name="com.meizu.c2dm.intent.RECEIVE" />

         <category android:name="应用包名"></category>
     </intent-filter>
</receiver>
```

## 启动代码已经注册日志输出

在启动信鸽\(调用 `XGPushManager.registerPush` \)之前配置如下代码：

```java
//设置魅族APPID和APPKEY
XGPushConfig.enableOtherPush(context, true);
XGPushConfig.setMzPushAppId(this, APP_ID);
XGPushConfig.setMzPushAppKey(this, APP_KEY);
```

注册成功的日志如下：

```java
//成功的获取到信鸽的token和魅族的token，并且绑定成功说明注册成功
INFO16:24:27.94313075XINGE[a] >> bind OtherPushToken success ack with [accId = 2100273138 , rsp = 0] token = 08d7ea8e4b93952cbfdd2cb68461342c314d281a otherPushType = meizu otherPushToken = ULY6c5968627059714a475c63517f675b7f655e62627e
```

**注：如果需要通过点击回调获取参数或者跳转自定义页面，可以通过使用Intent来实现，**[**点击查看教程**](http://docs.developer.qq.com/xg/android_access/android_faq.html#消息点击事件以及跳转页面方法)

## 代码混淆

```xml
-dontwarn com.meizu.cloud.pushsdk.**

-keep class com.meizu.cloud.pushsdk.**{*;}
```

## 厂商通道测试方法\(通用\)

1. 在您的App中集成信鸽V3.2.1以上版本的SDK，并且按照「厂商通道集成指南」集成所需的厂商SDK

2. 确认已在信鸽管理台中「应用配置-厂商&海外通道」中填写相关的应用信息。通常相关配置将在1个小时后生效，请您耐心等待，在生效后再进行下一个步骤

3. 将集成好的App（测试版本）安装在测试机上，并且运行App

4. 保持App在前台运行，尝试对设备进行单推/全推

5. 如果应用收到消息，将App退到后台，并且杀掉所有App进程

6. 再次进行单推/全推，如果能够收到推送，则表明厂商通道集成成功




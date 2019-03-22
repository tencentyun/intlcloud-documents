#FCM通道集成指南

fcm通道是信鸽和谷歌推出的各种推送通道，在外国可用谷歌service框架的手机上能够实现不打开应用收到推送消息。在没有fcm的手机rom下依旧走信鸽的推送通道。

##获取FCM推送秘钥
1. [FireBase官网](https://firebase.google.com/?hl=zh-cn)注册应用信息。并将获取到的FCM应用推送服务器密钥和 SenderID，配置到信鸽的管理台。
2. 下载google-services.json 文件。
如图所示：

获取json文件：
![](/assets/获取fcmjson.jpeg)

获取服务器密钥：
![](/assets/获取服务器密钥.jpeg)


##AS开发集成方法

1.配置google-services.json文件。如图所示：

![](/assets/配置json.png)


2. 配置gradle,集成谷歌service.

a)在项目级的build.gradle文件中的dependencies节点中添加下面代码：
```xml
classpath 'com.google.gms:google-services:3.1.0'
```
在应用级的build.gradle文件中添加依赖
```xml

compile 'com.tencent.xinge:fcm:4.3.0-beta'


compile 'com.google.firebase:firebase-messaging:17.3.1'


 //在应用级的gradle文件的最后一行代码中新增并将google-services.json放进你应用model的根路径下

apply plugin: 'com.google.gms.google-services'

```
##Eclipse开发集成方法

在集成好信鸽的基础下增加以下的配置：

1.配置google-services.json 文件，放在assets的目录下

2.把Xg4FCM-v4.xxx.jar，firebase-common-12.0.1.jar，firebase-iid-12.0.1.jar，firebase-messaging-12.0.1.jar，play-services-base-12.0.1.jar，play-services-basement-12.0.1.jar放到libs目录下

3.在AndroidManifest.xml中添加以下配置：

```xml
<application>
	 <!-- [START fcm_receiver] -->
  <receiver
            android:name="com.google.firebase.iid.FirebaseInstanceIdReceiver"
            android:exported="true"
            android:permission="com.google.android.c2dm.permission.SEND" >
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                             <!-- 下面修改为应用的包名 -->
                <category android:name="com.qq.xgdemo" />
            </intent-filter>
        </receiver>
        <!-- [END fcm_receiver] -->
        <receiver
            android:name="com.google.firebase.iid.FirebaseInstanceIdInternalReceiver"
            android:exported="false" />
        <!-- [START fcm_listener] -->
     <service
            android:name="com.tencent.android.fcm.XGFcmListenerService"
            android:exported="true" >
            <intent-filter android:priority="-500" >
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
     </service>
        <!-- [END fcm_listener] -->
        <!-- [START instanceId_listener] -->
     <service
            android:name="com.tencent.android.fcm.XGFcmInstanceIDListenerService"
            android:exported="true" >
            <intent-filter android:priority="-500" >
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
            </intent-filter>
     </service>
        <!-- 9080000是google-play-services.jar的版本，要求手机上的google play service版本大于此值 -->
        <meta-data android:name="com.google.android.gms.version" android:value="9080000" /> 
        <!-- [END instanceId_listener] -->

</application>

<!-- [START gcm_permission] -->
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    <!-- 声明并使用一个自定义的权限以此来确保只有这个程序可以接收你的GCM消息, 如果是4.1或更高版本的系统就不需要这个权限，com.qq.xgdemo改成应用包名 -->
    <permission android:name="应用包名.permission.C2D_MESSAGE"  android:protectionLevel="signature" />
    <uses-permission android:name="应用包名.permission.C2D_MESSAGE" />
    <!-- [END gcm_permission] -->
```

##启用FCM推送


在调用信鸽注册代码（XGPushManager.registerPush）前面添加以下代码设置

```java
XGPushConfig.enableFcmPush(this,true);
XGPushConfig.enableOtherPush(this, true);
```
注册FCM成功的日志如下：

```xml
12-02 09:16:31.874 17260-17423/lc.com.xinge.push E/XG_fcm: Fcm App has initialize 
12-02 09:16:31.874 17260-17423/lc.com.xinge.push D/XG_fcm: FirebaseAPP初始化完成
12-02 09:16:31.875 17260-17423/lc.com.xinge.push I/XG_fcm: registerPush Token is: eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI
12-02 09:16:31.877 17260-17260/lc.com.xinge.push W/FA: Service connection failed: ConnectionResult{statusCode=SERVICE_VERSION_UPDATE_REQUIRED, resolution=null, message=null}
12-02 09:16:31.892 17260-17278/lc.com.xinge.push V/FA: Using measurement service
12-02 09:16:31.893 17260-17278/lc.com.xinge.push V/FA: Connecting to remote service
12-02 09:16:31.895 17260-17423/lc.com.xinge.push I/XINGE: [XGOtherPush] Reservert info: other push token is : eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI  other push type: fcm
```
# 信鸽Android SDK 版本集成指南

<hr>

## 通过AndroidStudio自动集成

###  导入依赖
AndroidStudio 上可以使用 jcenter 远程仓库自动接入，不需要在项目中导入jar包和so文件；
在 AndroidManifest.xml 中不需要配置信鸽相关的内容，jcenter 会自动导入。
导入依赖过后修改应用配置，书写注册代码就能够实现信鸽快速接入。 
对应的依赖版本号均是官网上最新的版本。
用户自定义的recevier.依然需要在Androidmanifest.xml配置相关节点。

在```app build.gradle```文件下配置 以下内容

```java
    
    android {
        ......
        defaultConfig {

            //信鸽官网上注册的包名.注意application ID 和当前的应用包名以及 信鸽官网上注册应用的包名必须一致。
            applicationId "你的包名" 
            ......

            ndk {
                //根据需要 自行选择添加的对应cpu类型的.so库。 
                abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a' 
                // 还可以添加 'x86', 'x86_64', 'mips', 'mips64'
            }

            manifestPlaceholders = [

                XG_ACCESS_ID:"注册应用的accessid",
                XG_ACCESS_KEY : "注册应用的accesskey",
            ]
            ......
        }
        ......
    }

    dependencies {
        ......   
    
    //信鸽普通版本jar，不包含厂商通道
    implementation  'com.tencent.xinge:xinge:4.0.5-release'
    //implementation'com.tencent.xinge:xinge:4.3.2-beta'
    //jg包
    implementation'com.tencent.jg:jg:1.1'
    //wup包
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    //mid包，minSdkVersion 14
    implementation 'com.tencent.mid:mid:4.0.7-Release'
        
    }
```

** 注意: **

- 如果在添加以上 abiFilter 配置之后 Android Studio 出现以下提示：

NDK integration is deprecated in the current plugin. Consider trying the new experimental plugin.

则在 Project 根目录的 gradle.properties 文件中添加：

android.useDeprecatedNdk=true


- 如需监听消息请参考XGBaseReceiver接口或者是 demo 的 MessageReceiver 类。自行继承XGBaseReceiver并且在配置文件中配置如下内容：

```xml
<receiver android:name="完整的类名如:com.qq.xgdemo.receiver.MessageReceiver"
android:exported="true" >
<intent-filter>
<!-- 接收消息透传 -->
<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
<!-- 监听注册、反注册、设置/删除标签、通知被点击等处理结果 -->
<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
</intent-filter>
</receiver>
```
- 4.X以上版本已经兼容了 Android P，默认支持HTTPS，如果要使用HTTP，需要自行配置（[点击查看配置方法](http://docs.developer.qq.com/xg/android_access/android_p_compatibility.html)）


## 手动配置来进行集成
### 注册并下载SDK

<hr>

前往信鸽管理台 xg.qq.com，使用QQ号码登陆，进入应用注册页，填写“应用名称”和“应用包名”（必须要跟APP一致），选择“操作系统”和“分类”，最后点击“创建应用”。

应用创建成功后，点击“应用配置”即可看到 APP 专属的 AccessId 和 AccessKey 等信息。

注册完成后，请下载最新版本的 Android SDK 到本地，并解压。

### 工程配置

<hr>

将SDK导入到工程的步骤为：

（1）创建或打开Android工程（关于如何创建Android工程，请参照开发环境的章节）。

（2）将信鸽 SDK目录下的libs目录所有文件拷贝到工程的libs（或lib）目录下。

（3）选中libs（或lib）目录下的信鸽jar包，右键菜单中选择Build Path， 选择Add to Build Path将SDK添加到工程的引用目录中。
（4）.so文件是信鸽必须的组件，支持armeabi、armeabi-v7a、misp和x86平台，请根据自己当前.so支持的平台添加

a）如果你的项目中没有使用其它.so，建议复制四个平台目录到自己工程中；

b）如果已有.so文件，只需要复制信鸽对应目录下的文件；

c）若是MSDK接入的游戏，通常只需要armeabi目录下的.so；

d）若当前工程已经有armeabi，那么只需要添加信鸽的armeabi下的.so，其它目录无需添加。其它情况类似，只添
加当前 平台存在的平台即可。

e）若在Androidstudio中导入so文件出错（错误10004.SOERROR），在main文件目录下 添加jniLibs命名的文件
夹将所有的架构文件复制进去也就是SDK文档中的Other-Platform-SO下的所有文件夹。如图：
![![](/assets/so配置.png)



（5）打开Androidmanifest.xml，添加以下配置（建议参考下载包的Demo修改），其中YOUR_ACCESS_ID和YOUR_ACCESS_KEY替换为APP对应的accessId和accessKey,请确保按照要求配置，否则可能导致服务不能正常使用。

```xml
<application
<!-- 【必须】 信鸽receiver广播接收 -->
<receiver android:name="com.tencent.android.tpush.XGPushReceiver"
android:process=":xg_service_v4" >
<intent-filter android:priority="0x7fffffff" >
<!-- 【必须】 信鸽SDK的内部广播 -->
<action android:name="com.tencent.android.tpush.action.SDK" />
<action android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
<!-- 【必须】 系统广播：开屏和网络切换 -->
<action android:name="android.intent.action.USER_PRESENT" />
<action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
<!-- 【可选】 一些常用的系统广播，增强信鸽service的复活机会，请根据需要选择。当然，你也可以添加APP自定义的一些广播让启动service -->
<action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
<action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
<action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
</intent-filter>
</receiver>

<!-- 【可选】APP实现的Receiver，用于接收消息透传和操作结果的回调，请根据需要添加 -->
<!-- YOUR_PACKAGE_PATH.CustomPushReceiver需要改为自己的Receiver： -->
<receiver android:name="com.qq.xgdemo.receiver.MessageReceiver"
android:exported="true" >
<intent-filter>
<!-- 接收消息透传 -->
<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
<!-- 监听注册、反注册、设置/删除标签、通知被点击等处理结果 -->
<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
</intent-filter>
</receiver>

<!-- 【注意】 如果被打开的activity是启动模式为SingleTop，SingleTask或SingleInstance，请根据通知的异常自查列表第8点处理-->
<activity
android:name="com.tencent.android.tpush.XGPushActivity"
android:exported="false" >
<intent-filter>
<!-- 若使用AndroidStudio，请设置android:name="android.intent.action"-->
<action android:name="" />
</intent-filter>
</activity>

<!-- 【必须】 信鸽service -->
<service
android:name="com.tencent.android.tpush.service.XGPushServiceV4"
android:exported="true"
android:persistent="true"
android:process=":xg_service_v4" />


<!-- 【必须】 提高service的存活率 -->
<service
android:name="com.tencent.android.tpush.rpc.XGRemoteService"
android:exported="true">
<intent-filter>
<!-- 【必须】 请修改为当前APP包名 .PUSH_ACTION, 如demo的包名为：com.qq.xgdemo -->
<action android:name="当前应用的包名.PUSH_ACTION" />
</intent-filter>
</service>


<!-- 【必须】 【注意】authorities修改为 包名.AUTH_XGPUSH, 如demo的包名为：com.qq.xgdemo-->
<provider
android:name="com.tencent.android.tpush.XGPushProvider"
android:authorities="当前应用的包名.AUTH_XGPUSH"
android:exported="true"/>

<!-- 【必须】 【注意】authorities修改为 包名.TPUSH_PROVIDER, 如demo的包名为：com.qq.xgdemo-->
<provider
android:name="com.tencent.android.tpush.SettingsContentProvider"
android:authorities="当前应用的包名.TPUSH_PROVIDER"
android:exported="false" />

<!-- 【必须】 【注意】authorities修改为 包名.TENCENT.MID.V3, 如demo的包名为：com.qq.xgdemo-->
<provider
android:name="com.tencent.mid.api.MidProvider"
android:authorities="当前应用的包名.TENCENT.MID.V3"
android:exported="true" >
</provider>



<!-- 【必须】 请将YOUR_ACCESS_ID修改为APP的AccessId，“21”开头的10位数字，中间没空格 -->
<meta-data
android:name="XG_V2_ACCESS_ID"
android:value="YOUR_ACCESS_ID" />
<!-- 【必须】 请将YOUR_ACCESS_KEY修改为APP的AccessKey，“A”开头的12位字符串，中间没空格 -->
<meta-data
android:name="XG_V2_ACCESS_KEY"
android:value="YOUR_ACCESS_KEY" />
</application>
<!-- 【必须】 信鸽SDK所需权限 -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.VIBRATE" />
<!-- 【常用】 信鸽SDK所需权限 -->
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_SETTINGS" />
<!-- 【可选】 信鸽SDK所需权限 -->
<uses-permission android:name="android.permission.RESTART_PACKAGES" />
<uses-permission android:name="android.permission.BROADCAST_STICKY" />
<uses-permission android:name="android.permission.KILL_BACKGROUND_PROCESSES" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.READ_LOGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.BATTERY_STATS" />

```




###     3.x升级4.x手动配置来进行集成

1.	【必须】提取SDK文档中的最新jar包替换当前信鸽SDK版本。                         
2.	【必须】根据所需平台，提取```libtpnsSecurity.so```替换老版本和删除原先```libxguardian.so```

3.     【必须】检查是否配置正确（v3升级V4）
```
com.tencent.android.tpush.service.XGPushServiceV4
com.tencent.android.tpush.XGPushReceiver
```


```xml
<!-- 【必须】 信鸽service -->
       <service
           android:name="com.tencent.android.tpush.service.XGPushServiceV4"
           android:exported="true"
           android:persistent="true"
           android:process=":xg_service_v4" />

<!-- 【必须】 通知service，此选项有助于提高抵达率 -->
       <receiver
            android:name="com.tencent.android.tpush.XGPushReceiver"
            android:process=":xg_service_v4" >
            <intent-filter android:priority="0x7fffffff" >

                <!-- 【必须】 信鸽SDK的内部广播 -->
                <action android:name="com.tencent.android.tpush.action.SDK" />
                android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
                <!-- 【必须】 系统广播：网络切换 -->
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

                <!-- 【可选】 系统广播：开屏 -->
                <action android:name="android.intent.action.USER_PRESENT" />

                <!-- 【可选】 一些常用的系统广播，增强信鸽service的复活机会，请根据需要选择。当然，你也可以添加APP自定义的一些广播让启动service -->
                <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
                <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
            </intent-filter>
            <!-- 【可选】 usb相关的系统广播，增强信鸽service的复活机会，请根据需要添加 -->
            <intent-filter android:priority="0x7fffffff" >
                <action android:name="android.intent.action.MEDIA_UNMOUNTED" />
                <action android:name="android.intent.action.MEDIA_REMOVED" />
                <action android:name="android.intent.action.MEDIA_CHECKING" />
                <action android:name="android.intent.action.MEDIA_EJECT" />

                <data android:scheme="file" />
            </intent-filter>
        </receiver>
        
        ```
         

 ###	【可选】如果是需要使用多通道，增加以下配置：

<!-- 小米配置 -->
```xml


		<service
            android:name="com.xiaomi.push.service.XMPushService"
            android:enabled="true"
            android:process=":pushservice" />
        <service
            android:name="com.xiaomi.push.service.XMJobService"
            android:enabled="true"
            android:exported="false"
            android:permission="android.permission.BIND_JOB_SERVICE"
            android:process=":pushservice" />
        <!-- 注：此service必须在3.0.1版本以后（包括3.0.1版本）加入 -->
        <service
            android:name="com.xiaomi.mipush.sdk.PushMessageHandler"
            android:enabled="true"
            android:exported="true" />
        <service
            android:name="com.xiaomi.mipush.sdk.MessageHandleService"
            android:enabled="true" />
        <!-- 注：此service必须在2.2.5版本以后（包括2.2.5版本）加入 -->
        <receiver
            android:name="com.xiaomi.push.service.receivers.NetworkStatusReceiver"
            android:exported="true" >
            <intent-filter>
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </receiver>
        <receiver
            android:name="com.xiaomi.push.service.receivers.PingReceiver"
            android:exported="false"
            android:process=":pushservice" >
            <intent-filter>
                <action android:name="com.xiaomi.push.PING_TIMER" />
            </intent-filter>
        </receiver>


        <receiver
            android:name="com.tencent.android.mipush.XMPushMessageReceiver"
            android:exported="true" >
            <intent-filter>
                <action android:name="com.xiaomi.mipush.RECEIVE_MESSAGE" />
            </intent-filter>
            <intent-filter>
                <action android:name="com.xiaomi.mipush.MESSAGE_ARRIVED" />
            </intent-filter>
            <intent-filter>
                <action android:name="com.xiaomi.mipush.ERROR" />
            </intent-filter>
        </receiver>
		
		 <!-- 注：魅族push -->
        <service
            android:name="com.meizu.cloud.pushsdk.NotificationService"
            android:exported="true" />

        <receiver android:name="com.meizu.cloud.pushsdk.SystemReceiver" >
            <intent-filter>
                <action android:name="com.meizu.cloud.pushservice.action.PUSH_SERVICE_START" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </receiver>
        <receiver android:name="com.tencent.android.mzpush.MZPushMessageReceiver" >
            <intent-filter>

                <!-- 接收push消息 -->
                <action android:name="com.meizu.flyme.push.intent.MESSAGE" />
                <!-- 接收register消息 -->
                <action android:name="com.meizu.flyme.push.intent.REGISTER.FEEDBACK" />
                <!-- 接收unregister消息 -->
                <action android:name="com.meizu.flyme.push.intent.UNREGISTER.FEEDBACK" />
                <action android:name="com.meizu.c2dm.intent.REGISTRATION" />
                <action android:name="com.meizu.c2dm.intent.RECEIVE" />
                <!-- 你的应用包名 -->
                <category android:name="你的应用包名" >
                </category>
            </intent-filter>
        </receiver>
		
		<!-- 注：华为push 需要的 begin -->
		<meta-data
        android:name="com.huawei.hms.client.appid"
        android:value="你的华为注册APPID" >
        </meta-data>

		
		<activity
            android:name="com.huawei.hms.activity.BridgeActivity"
            android:configChanges="orientation|locale|screenSize|layoutDirection|fontScale"
            android:excludeFromRecents="true"
            android:exported="false"
            android:hardwareAccelerated="true"
            android:theme="@android:style/Theme.Translucent" >
            <meta-data
                android:name="hwc-theme"
                android:value="androidhwext:style/Theme.Emui.Translucent" />
        </activity>

        <provider
            android:name="com.huawei.hms.update.provider.UpdateProvider"
            android:authorities="你的应用包名.hms.update.provider"
            android:exported="false"
            android:grantUriPermissions="true" >
        </provider>



        <receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
            <intent-filter>

                <!-- 接收通道发来的通知栏消息，兼容老版本PUSH -->
                <action android:name="com.huawei.intent.action.PUSH" />
            </intent-filter>
        </receiver>
        <receiver android:name="com.tencent.android.hwpush.HWPushMessageReceiver" >
            <intent-filter>

                <!-- 必须,用于接收TOKEN -->
                <action android:name="com.huawei.android.push.intent.REGISTRATION" />
                <!-- 必须，用于接收消息 -->
                <action android:name="com.huawei.android.push.intent.RECEIVE" />
                <!-- 可选，用于点击通知栏或通知栏上的按钮后触发onEvent回调 -->
                <action android:name="com.huawei.android.push.intent.CLICK" />
                <!-- 可选，查看PUSH通道是否连接，不查看则不需要 -->
                <action android:name="com.huawei.intent.action.PUSH_STATE" />
            </intent-filter>
        </receiver>
		
		 <!-- 云控相关 -->
        <receiver
            android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadReceiver"
            android:exported="true">
            <intent-filter>
                <action android:name="com.tencent.android.tpush.cloudcontrol.action.DOWNLOAD_FILE_FINISH" />
            </intent-filter>
        </receiver>
        <service
            android:name="com.tencent.android.tpush.cloudctr.network.CloudControlDownloadService"
            android:exported="true"
            android:persistent="true" />
        <!-- 云控相关 - 完 -->
        
     <!-- 增加厂商权限 -->
	 <!-- 兼容flyme5.0以下版本，魅族内部集成pushSDK必填，不然无法收到消息-->
    <uses-permission android:name="com.meizu.flyme.push.permission.RECEIVE"></uses-permission>
    <permission android:name="你的应用包名.push.permission.MESSAGE" android:protectionLevel="signature"/>
    <uses-permission android:name="你的应用包名.push.permission.MESSAGE"></uses-permission>
    <!--  兼容flyme3.0配置权限-->
    <uses-permission android:name="com.meizu.c2dm.permission.RECEIVE" />
    <permission android:name="你的应用包名.permission.C2D_MESSAGE"
        android:protectionLevel="signature"></permission>
    <uses-permission android:name="你的应用包名.permission.C2D_MESSAGE"/>
    <!-- 注：魅族push 需要的权限 end -->
	<!--小米所需权限-->
    <permission
        android:name="你的应用包名.permission.MIPUSH_RECEIVE"
        android:protectionLevel="signature" />
    <uses-permission android:name="你的应用包名.permission.MIPUSH_RECEIVE" />
    ```




##注册以及部分日志输出。

<hr>

1.根据<a href="http://docs.developer.qq.com/xg/android_access/manual.html" target="_blank" >手动接入</a>或者<a href="http://docs.developer.qq.com/xg/android_access/jcenter.html" target="_blank" >自动接入</a>，配置好信鸽过后，获取信鸽注册日志（接入过程中建议调用有回调的注册接口，开启信鸽的debug日志输出。AndroidStudio 建议采用jcenter自动接入，无需在配置文件中配置信鸽各个节点，全部由依赖导入）。

**开启debug日志数据**

```java
XGPushConfig.enableDebug(this,true);
```

**开启厂商通道初始化代码**


使用otherpush版本需要在你的Application的attachBaseContext函数里面增加
```java
 StubAppUtils.attachBaseContext(context);
 ```

在初始化或者主页面onCreat函数里添加
```java

 XGPushConfig.enableOtherPush(getApplicationContext(), true);
 XGPushConfig.setHuaweiDebug(true);
 XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
 XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
 XGPushConfig.setMzPushAppId(this, "APPID");
 XGPushConfig.setMzPushAppKey(this, "APPKEY");
```


**token注册**

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
@Override
public void onSuccess(Object data, int flag) {
//token在设备卸载重装的时候有可能会变
Log.d("TPush", "注册成功，设备token为：" + data);
}
@Override
public void onFail(Object data, int errCode, String msg) {
Log.d("TPush", "注册失败，错误码：" + errCode + ",错误信息：" + msg);
}
})
```
过滤"TPush"注册成功的日志如下：

```xml
10-09 20:08:46.922 24290-24303/com.qq.xgdemo I/XINGE: [TPush] get RegisterEntity:RegisterEntity [accessId=2100250470, accessKey=null, token=5874b7465d9eead746bd9374559e010b0d1c0bc4, packageName=com.qq.xgdemo, state=0, timestamp=1507550766, xgSDKVersion=3.11, appVersion=1.0]
10-09 20:08:47.232 24290-24360/com.qq.xgdemo D/TPush: 注册成功，设备token为：5874b7465d9eead746bd9374559e010b0d1c0bc4
```
**厂商通道token注册**

1.开启厂商通道初始化，等待云控下载对应设备的厂商dex包 。
以小米为例，下载成功的日志如下：
```xml
10-25 15:16:31.067 16551-16551/? D/XINGE: [DownloadService] onCreate()
10-25 15:16:31.073 16551-16757/? D/XINGE: [DownloadService] action:onHandleIntent
10-25 15:16:31.083 16551-16757/? V/XINGE: [CloudCtrDownload] Create downloadControl
10-25 15:16:31.089 16551-16757/? I/XINGE: [CloudCtrDownload] action:download - url:https://pingjs.qq.com/xg/Xg-Xm-plug-1.0.2.pack, saveFilePath:/data/user/0/com.qq.xgdemo1122/app_dex/XG/5/, fileName:Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.097 16551-16757/? V/XINGE: [CloudCtrDownload] Download file: Xg-Xm-plug-1.0.2.pack
10-25 15:16:31.641 16551-16757/? D/XINGE: [DownloadService] download file Succeed
10-25 15:16:31.650 16551-16757/? D/XINGE: [CloudCtrDownload] Download succeed.
10-25 15:16:31.653 16551-16551/? D/XINGE: [CloudControlDownloadReceiver] onReceive
10-25 15:16:31.673 16551-16738/? I/test: Download file SuccessXg-Xm-plug-1.0.2.pack to /data/user/0/com.qq.xgdemo1122/app_dex/XG/5/
```
2.观察到下载完成的日志后杀死应用进程，再次启动应用即可完成注册：
```xml
10-25 15:34:26.423 18700-18700/? D/TPush: +++ register push sucess. token:22dc455f79d36dec1065418e1d284639bac776b4
10-25 15:34:26.432 18700-18731/? I/XINGE: [XGOtherPush] other push token is : lYDvOWispXGoVADhRyiVdw3krLIolEd21JqdmjqBqDISK+gwl/PBm3tA9U43jxfH other push type: xiaomi
```
**设置账号**

```java
//注意在3.2.2 版本信鸽对账号绑定和解绑接口进行了升级具体详情请参考API文档。
XGPushManager.bindAccount(getApplicationContext(), "XINGE");
```
过滤“TPush”账号注册成功的日志如下：

```xml
//如推送返回48账号无效，请确认账号接口调用成功
10-11 15:55:57.810 29299-29299/com.qq.xgdemo D/TPushReceiver: TPushRegisterMessage [accessId=2100250470, deviceId=853861b6bba92fb1b63a8296a54f439e, account=XINGE, ticket=0, ticketType=0, token=3f13f775079df2d54e1f82475a28bccd3bfef8c1]注册成功
```

**设置标签**

```java
XGPushManager.setTag(this,"XINGE");
```

设置标签成功的日志：

```xml
10-09 20:11:42.558 27348-27348/com.qq.xgdemo I/XINGE: [XGPushManager] Action -> setTag with tag = XINGE
```

**收到消息日志**

```xml
10-16 19:50:01.065 5969-6098/com.qq.xgdemo D/XINGE: [i] Action -> handleRemotePushMessage
10-16 19:50:01.065 5969-6098/com.qq.xgdemo I/XINGE: [i] >> msg from service, @msgId=1 @accId=2100250470 @timeUs=1508154601660412 @recTime=1508154601076 @msg.date= @msg.busiMsgId=0 @msg.timestamp=1508154601 @msg.type=1 @msg.multiPkg=0 @msg.serverTime=1508154601000 @msg.ttl=259200 @expire_time=1508154860200076 @currentTimeMillis=1508154601076
10-16 19:50:01.095 5969-6098/com.qq.xgdemo D/XINGE: [m] Action -> handlerPushMessage
10-16 19:50:01.105 5969-6098/com.qq.xgdemo I/XINGE: [m] Receiver msg from server :PushMessageManager [msgId=1, accessId=2100250470, busiMsgId=0, content={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token 推送","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, timestamps=1508154601, type=1, intent=Intent { act=com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE cat=[android.intent.category.BROWSABLE] pkg=com.qq.xgdemo (has extras) }, messageHolder=BaseMessageHolder [msgJson={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token 推送","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, msgJsonStr={"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token 推送","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}, title=XGDemo, content=token 推送, customContent=null, acceptTime=null]]
10-16 19:50:01.105 5969-6098/com.qq.xgdemo V/XINGE: [XGPushManager] Action -> msgAck(com.qq.xgdemo,1)
10-16 19:50:01.115 5969-6098/com.qq.xgdemo I/XINGE: [TPush] title encry obj:{"cipher":"YZXM+CuPhqaBn4eK0SE9ApWieHznugNT2uKo0OaXtlDDHLJiY7NlvSL2ZnlSb8E7yd7E7i9JU3g0PlFyYNLjokNp1buJuPoMYEHaJ0s6vmUMY+cq0Sv782XHxNzekV4a9mRcJ5xsOccIjH1VoskUmikfZJo3XLhZveWNYGPaoto="}
10-16 19:50:01.125 5969-6098/com.qq.xgdemo E/XINGE: [MessageInfoManager] delOldShowedCacheMessage Error! toDelTime: 1507981801138
10-16 19:50:01.145 5969-6098/com.qq.xgdemo I/XINGE: [MessageHelper] Action -> showNotification {"n_id":0,"title":"XGDemo","style_id":1,"icon_type":0,"builder_id":1,"vibrate":0,"ring_raw":"","content":"token 推送","lights":1,"clearable":1,"action":{"aty_attr":{"pf":0,"if":0},"action_type":1,"activity":""},"small_icon":"","ring":1,"icon_res":"","custom_content":{}}

```

##代码混淆


如果您的项目中使用proguard等工具做了代码混淆，请保留以下选项，否则将导致信鸽服务不可用。

```xml
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {* ;}
-keep class com.tencent.mid.** {* ;}
-keep class com.qq.taf.jce.** {*;}
-keep class com.tencent.bigdata.** {* ;}

华为通道
-ignorewarning
-keepattributes *Annotation*
-keepattributes Exceptions
-keepattributes InnerClasses
-keepattributes Signature
-keepattributes SourceFile,LineNumberTable
-keep class com.hianalytics.android.**{*;}
-keep class com.huawei.updatesdk.**{*;}
-keep class com.huawei.hms.**{*;}
-keep class com.huawei.android.hms.agent.**{*;}

小米通道
-keep class com.xiaomi.**{*;}
-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver

魅族通道
-dontwarn com.meizu.cloud.pushsdk.**
-keep class com.meizu.cloud.pushsdk.**{*;}

```





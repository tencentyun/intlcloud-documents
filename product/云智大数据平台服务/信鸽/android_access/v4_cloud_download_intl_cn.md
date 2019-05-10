#关于4.*信鸽以及厂商通道集成说明
<hr>

###概述
 动态加载厂商通道版本可根据设备系统自动适配相应的厂商推送服务，无需另外手动集成厂商通道，大大减少了开发者接入时间和```app```的体量。
##（AS集成）使用动态加载厂商通道方式：

1. 在你app模块的```build.gradle``` 文件里添加

```java

    ndk {
                //根据需要 自行选择添加的对应cpu类型的.so库。
                abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
                // 还可以添加 'x86', 'x86_64', 'mips', 'mips64'
            }
    manifestPlaceholders = [
                XG_ACCESS_ID:"注册应用的accessid",
                XG_ACCESS_KEY : "注册应用的accesskey",
              //如果需要华为通道，则加上华为的APPID 
                HW_APPID: "华为的APPID"
                 ]
    //增加以下依赖
    implementation  'com.tencent.xinge:xinge:4.3.2-xgotherpush-beta'
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    implementation 'com.tencent.mid:mid:4.0.7-Release'
    //需要集成fcm增加以下依赖并将google-services.json放进你应用model的根路径下:
    implementation 'com.tencent.xinge:fcm:4.3.2-beta'
    implementation 'com.google.firebase:firebase-messaging:17.3.1'
    apply plugin: 'com.google.gms.google-services'


 ```
 2.代码上需要在你的```Application```的```attachBaseContext```函数里面增加
```java
     StubAppUtils.attachBaseContext(context);
 ```


初始化页面添加 
```java
    XGPushConfig.enableOtherPush(getApplicationContext(), true);
    XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
    XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
    XGPushConfig.setMzPushAppId(this, "APPID");
    XGPushConfig.setMzPushAppKey(this, "APPKEY");
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



###（AS集成）不使用动态加载厂商通道方式：
1.在你app模块的```build.gradle ```文件里添加
```java
    ndk {
                //根据需要 自行选择添加的对应cpu类型的.so库。
                abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
                // 还可以添加 'x86', 'x86_64', 'mips', 'mips64'
            }
     manifestPlaceholders = [
                XG_ACCESS_ID:"注册应用的accessid",
                XG_ACCESS_KEY : "注册应用的accesskey",
              //如果需要华为通道，则加上华为的APPID 
                HW_APPID: "华为的APPID"
                 ]
    //增加以下依赖

    implementation 'com.tencent.xinge:xinge:4.3.2-beta'
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    implementation 'com.tencent.mid:mid:4.0.7-Release'
    implementation 'com.tencent.xinge:mipush:4.3.2-xiaomi-beta'
    implementation 'com.tencent.xinge:xgmz:4.3.2-meizu-beta'
    implementation 'com.tencent.xinge:xghw:4.3.2-huawei-beta'
    //fcm通道需要增加以下依赖并将google-services.json放进你应用model的根路径下。
    implementation 'com.tencent.xinge:fcm:4.3.2-beta'
    implementation 'com.google.firebase:firebase-messaging:17.3.1'
    apply plugin: 'com.google.gms.google-services'

```
2.初始化页面添加 
```java
    XGPushConfig.enableOtherPush(getApplicationContext(), true);
    XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
    XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
    XGPushConfig.setMzPushAppId(this, "APPID");
    XGPushConfig.setMzPushAppKey(this, "APPKEY");
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
###注意事项
1. 动态下载插件目前只支持华为、小米、魅族通道,有可能在某些机型上出现未知异常，导致注册失败。
2. 能否成功加载厂商通道的dex配置包依赖于终端网络环境和设备厂商系统的限制，如多次注册失败请使用<a href="#（AS集成）不使用动态加载厂商通道方式">（AS集成）不使用动态加载厂商通道方式</a>。
3. 使用AS动态加载方式无需手动集成XG4HWPush.jar，XG4MZPush.jar，小米XG4XMPush.jar等对应通道的jar或者是gradle对应依赖。
4. 如果Eclipse集成需使用动态加载方式，则需要增加XgOtherPush.jar包，否则不要增加此包。(注意：XgOtherPush.jar和手动导入的XG4XMPush.jar，XG4MZPush，XG4HWPush的jar或者是小米，华为，魅族的gradle对应依赖是互斥的。)
5. Eclipse使用动态加载需增加XgOtherPush.jar，manifest必须要配上云控配置：
```xml
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
```
在代码接入上，需要在你的应用```Application```的```attachBaseContext```函数里面增加```StubAppUtils.attachBaseContext(context);```初始化动态加载框架。
**如果不使用动态加载厂商第4点就无需添加**。


# Integrating TPNS with Vendor-specific Channels
<hr>

### Overview
 The dynamically loaded vendor-specific channel version can automatically adapt to the corresponding vendor-specific push service according to the device operating system, without the need to manually integrate the vendor-specific channel, which greatly reduces the access time and ```app``` size.
##(AS Integration) Using the Dynamically Loaded Vendor-specific Channel

1. Add the following to the ```build.gradle``` file in your app module

```java

    ndk {
                // Choose and add the .so libraries corresponding to the cpu type as needed.
                abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
                // You can also add 'x86', 'x86_64', 'mips', and 'mips64'.
            }
    manifestPlaceholders = [
                XG_ACCESS_ID:"accessid of the registered app",
                XG_ACCESS_KEY : "accesskey of the registered app",
              // If you need the Huawei channel, add the Huawei APPID 
                HW_APPID: "Huawei APPID"
                 ]
    // Add the following dependencies
    implementation  'com.tencent.xinge:xinge:4.3.2-xgotherpush-beta'
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    implementation 'com.tencent.mid:mid:4.0.7-Release'
    // If you need to integrate the FCM channel, add the following dependencies and place google-services.json into the root path of your app's model:
    implementation 'com.tencent.xinge:fcm:4.3.2-beta'
    implementation 'com.google.firebase:firebase-messaging:17.3.1'
    apply plugin: 'com.google.gms.google-services'


 ```
 2. In the code, add the following to the ```attachBaseContext``` function in your ```Application```
```java
     StubAppUtils.attachBaseContext(context);
 ```


Add on the initialization page: 
```java
    XGPushConfig.enableOtherPush(getApplicationContext(), true);
    XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
    XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
    XGPushConfig.setMzPushAppId(this, "APPID");
    XGPushConfig.setMzPushAppKey(this, "APPKEY");
    XGPushManager.registerPush(this, new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
    // token may change after the app is uninstalled and then reinstalled on the device
    Log.d("TPush", "The registration succeeded, and the device token is: " + data);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
    Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
    }
    })
```



### (AS Integration) Not Using the Dynamically Loaded Vendor-specific Channel
1. Add the following to the ```build.gradle``` file in your app module
```java
    ndk {
                // Choose and add the .so libraries corresponding to the cpu type as needed.
                abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
                // You can also add 'x86', 'x86_64', 'mips', and 'mips64'.
            }
     manifestPlaceholders = [
                XG_ACCESS_ID:"accessid of the registered app",
                XG_ACCESS_KEY : "accesskey of the registered app",
              // If you need the Huawei channel, add the Huawei APPID 
                HW_APPID: "Huawei APPID"
                 ]
    // Add the following dependencies

    implementation 'com.tencent.xinge:xinge:4.3.2-beta'
    implementation 'com.tencent.wup:wup:1.0.0.E-release'
    implementation 'com.tencent.mid:mid:4.0.7-Release'
    implementation 'com.tencent.xinge:mipush:4.3.2-xiaomi-beta'
    implementation 'com.tencent.xinge:xgmz:4.3.2-meizu-beta'
    implementation 'com.tencent.xinge:xghw:4.3.2-huawei-beta'
    // If you need to integrate the FCM channel, add the following dependencies and place google-services.json into the root path of your app's model:
    implementation 'com.tencent.xinge:fcm:4.3.2-beta'
    implementation 'com.google.firebase:firebase-messaging:17.3.1'
    apply plugin: 'com.google.gms.google-services'

```
2. Add on the initialization page: 
```java
    XGPushConfig.enableOtherPush(getApplicationContext(), true);
    XGPushConfig.setMiPushAppId(getApplicationContext(), "APPID");
    XGPushConfig.setMiPushAppKey(getApplicationContext(), "APPKEY");
    XGPushConfig.setMzPushAppId(this, "APPID");
    XGPushConfig.setMzPushAppKey(this, "APPKEY");
    XGPushManager.registerPush(this, new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
    // token may change after the app is uninstalled and then reinstalled on the device
    Log.d("TPush", "The registration succeeded, and the device token is: " + data);
    }
    @Override
    public void onFail(Object data, int errCode, String msg) {
    Log.d("TPush", "The registration failed; error code: " + errCode + ", error message: " + msg);
    }
    })
```
### Precautions
1. The dynamic download plugin currently only supports Huawei, Mi, and Meizu channels. Unknown exceptions may occur on some models, resulting in registration failure.
2. Whether the dex configuration package of the vendor-specific channel can be loaded successfully depends on the device network environment and limitations of the vendor on the device system. If registration fails many times, please use the method in <a href="#（AS集成）不使用动态加载厂商通道方式">(AS Integration) Not Using the Dynamically Loaded Vendor-specific Channel</a>.
3. When using AS dynamic loading mode, you do not need to manually integrate the jar packages (such as XG4HWPush.jar, XG4MZPush.jar, or XG4XMPush.jar) of the corresponding channel  or the dependencies corresponding to the gradle.
4. For Eclipse integration, if you need to use the dynamic loading mode, you need to add the   XgOtherPush.jar package; otherwise, ignore this package. (Note: XgOtherPush.jar is mutually exclusive with the manually imported XG4XMPush.jar, XG4MZPush.jar, and XG4HWPush.jar, or Mi, Huawei, and Meizu gradle dependencies.)
5. For Eclipse, if you want to use dynamic loading, you need to add XgOtherPush.jar, and the manifest must be equipped with the following cloud control configuration:
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
In code access, you need to add the initialization dynamic loading framework ```StubAppUtils.attachBaseContext(context);``` to the ```attachBaseContext``` function in your ```Application```.
**If you do not use dynamically loaded vendor-specific channels, you do not need to add the 4th point**.


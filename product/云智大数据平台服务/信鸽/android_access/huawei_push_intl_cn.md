# 华为推送通道集成指南

华为推送通道是由**华为官方提供**的系统级推送通道。在华为手机上，推送消息能够通过华为的系统通道抵达终端，并且无需打开应用就能够收到推送。

**注意事项：**

1. 华为推送只有在**签名发布包环境**下才可以收到推送消息

2. 华为手机中的**移动推送服务**，必须升级到 <font color=#FF0000>2.5.3</font> 以上版本，华为通道会注册失败（依旧走信鸽通道）。

## 获取华为推送密钥

1.访问 [华为开放平台](http://developer.huawei.com)

2.注册/登录开发者账号。（如果您是新注册账号，需进行实名认证）

3.在华为推送平台中新建应用。注意：```应用包名```需跟您在信鸽填写的包名保持一致

4.获取应用相关的信息，并且将这些信息复制，填入信鸽管理台的```应用配置-厂商&海外通```栏目中，
  这些信息是```AppID```，```AppSecret```
  如下图所示：
![](/assets/huaweikey.jpeg)

		
## 配置SHA256证书指纹

**[配置示例]**
 
![](/assets/huaweisha.jpg)

获取```SHA256```证书指纹方法请参照 [华为推送接入文档](http://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_introduction_agent)

<hr>

## 集成指南

### AndroidStudio集成方法

在app模块下的build.gradle文件内先配置好信鸽所需要的配置之后再增加以下的华为节点：

1.配置华为APPID

```xml
 manifestPlaceholders = [
	 HW_APPID: "华为的APPID"
        ]
```

2.导入华为推送相关依赖


```js
/* 华为 3.2.7-release版
 * 注意：若华为通道使用此版本,则信鸽sdk版本也需要同时使用v3.2.7-Release
 */
 compile 'com.tencent.xinge:xghw:3.2.7-release'

/* 华为 3.2.8-Release
 * 注意：若华为通道使用此版本,则信鸽sdk版本也需要同时使用v4.0.5
 */
 compile 'com.tencent.xinge:xghw:3.2.8-Release'
```




### Eclipes集成方法

1.导入华为推送相关jar包 将```HMSSdkBase_*.jar```，```HMSSdkPush_*.jar```放在```libs```文件夹里。

2.在 ```Androidmanifest.xml``` 文件中新增如下配置：

```xml
<meta-data
            android:name="com.huawei.hms.client.appid"
            android:value="你的APPID（来自华为官网）" >
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
            android:authorities="应用包名.hms.update.provider"
            android:exported="false"
            android:grantUriPermissions="true" >
        </provider>      

        <receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
            <intent-filter>

                <!-- 接收通道发来的通知栏消息，兼容老版本PUSH -->
                <action android:name="com.huawei.intent.action.PUSH" />
            </intent-filter>
        </receiver>
        
<!-- 注：华为push 需要的 end -->

```
3.配置 <a href="#华为消息receiver">华为消息receiver</a>.

#### 华为消息receiver

1.自定义类，继承```com.huawei.hms.support.api.push.PushReceiver```，
  并且在```Androidmanifest.xml```中配置相关的节点。

示例代码：

```java
public class MyReceiver extends PushReceiver {

	@Override
	public void onEvent(Context context, Event arg1, Bundle arg2) {
		super.onEvent(context, arg1, arg2);
		
		showToast("onEvent" + arg1 + " Bundle " + arg2 ,  context);
	}

	@Override
	public boolean onPushMsg(Context context, byte[] arg1, Bundle arg2) {
		
		showToast("onPushMsg" + new String(arg1) + " Bundle " + arg2 ,  context);
		return super.onPushMsg(context, arg1, arg2);
	}

	@Override
	public void onPushMsg(Context context, byte[] arg1, String arg2) {
		
		showToast("onPushMsg" + new String(arg1) + " arg2 " + arg2 ,  context);
		super.onPushMsg(context, arg1, arg2);
	}

	@Override
	public void onPushState(Context context, boolean arg1) {
		
		showToast("onPushState" + arg1,  context);
		super.onPushState(context, arg1);
	}

	@Override
	public void onToken(Context context, String arg1, Bundle arg2) {
		super.onToken(context, arg1, arg2);
		
		 showToast(" onToken" + arg1 + "bundke " + arg2,  context);
	}

	@Override
	public void onToken(Context context, String arg1) {
		super.onToken(context, arg1);
		 showToast(" onToken" + arg1 ,  context);
	}

	public  void showToast(final String toast, final Context context)
    {
	
    	new Thread(new Runnable() {
			
			@Override
			public void run() {
				Looper.prepare();
				Toast.makeText(context, toast, Toast.LENGTH_SHORT).show();
				Looper.loop();
			}
		}).start();
    }
	
	private void  writeToFile(String conrent) {
		String SDPATH = Environment.getExternalStorageDirectory() + "/huawei.txt";
		try {
			FileWriter fileWriter = new FileWriter(SDPATH, true);
			
			fileWriter.write(conrent+"\r\n");
			fileWriter.flush();
			fileWriter.close();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}

```
2 . 在 ```AndroidManifest.xml``` 增加自定义 ```Receiver``` 配置如下：

```xml
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
```
### 启动华为推送以及注册日志
- 在调用信鸽（```XGPushManager.registerPush```）之前开启第三方推送接口：

```java
//打开第三方推送
XGPushConfig.enableOtherPush(getApplicationContext(), true);
```

注册成功的日志如下：
```xml
01-15 16:40:41.116 17916-17934/? I/XINGE: [XGOtherPush] other push token is : 0865551032618726300001294600CN01 other push type: huawei
01-15 16:40:41.122 15730-15846/? I/XINGE: [a] binder other push token with accid = 2100274337  token = 17c32948df0346d5837d4748192e9d2f14c81e08 otherPushType = huawei otherPushToken = 0865551032618726300001294600CN01
```

如果日志中出现：

```
otherPushType = huawei otherPushToken = null
```

请在注册代码之前调用：

```
XGPushConfig.setHuaweiDebug(true);
```
并手动确认给**应用存储权限**，然后查看SD卡目录下的 ```huawei.txt``` 文件内输出的注册华为失败的错误原因。
然后根据 [华为开发文档](http://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_api_reference_errorcode) 对应的错误码查找原因，以及解决办法。

若还不能解决，可以在cmd里执行```adb shell setprop log.tag.hwpush VERBOSE```和```adb shell logcat -v time > D:/log.txt``` 开始抓日志，然后进行测试，测完再关闭cmd窗口。将log发给我们的技术支持。

- **如果需要通过消息点击回调来获取参数或者跳转自定义页面，可以通过使用Intent方式来实现，[点击查看教程](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95)**

### 代码混淆

```xml
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

```

## 厂商通道测试方法

1. 在您的App中集成信鸽V3.2.1以上版本的SDK，并且按照「厂商通道集成指南」集成所需的厂商SDK

2. 确认已在信鸽管理台中「应用配置-厂商&海外通道」中填写相关的应用信息。通常，相关配置将在1个小时后生效，请您耐心等待，在生效后再进行下一个步骤

3. 将集成好的App（测试版本）安装在测试机上，并且运行App

4. 保持App在前台运行，尝试对设备进行单推/全推

5. 如果应用收到消息，将App退到后台，并且杀掉所有App进程

6. 再次进行单推/全推，如果能够收到推送，则表明厂商通道集成成功

**注：如果需要通过点击回调获取参数或者跳转自定义页面，可以通过使用Intent来实现，[点击查看教程](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95)**



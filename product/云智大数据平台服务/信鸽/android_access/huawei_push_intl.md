# Integration Guide for Huawei Push Channel

Huawei push channel is a system-level push channel **powered by Huawei**. On a Huawei phone, push messages can be delivered through Huawei's system channel without opening the app.

**Precautions:**

1. Huawei Push can only receive push messages in a **signed package environment**.

2. **Mobile Push Service** on the Huawei phone must be upgraded to <font color=#FF0000>v2.5.3</font> or higher. Otherwise, Huawei channel registration will fail and TPNS channel will be used.

## Getting Huawei Push Key

1. Go to [Huawei's development platform](http://developer.huawei.com).

2. Sign up for or log in to a developer account. (If you are registering a new account, you need to verify your identity.)

3. Create an app on the Huawei Push platform. Note: The ``` app package name``` must be the same as that entered in TPNS console.

4. Get app-related information and copy it into ```App configuration > Vendor-specific and global channels``` in TPNS console.
  This information includes ```AppID``` and ```AppSecret```.
  See the figure below:
![](/assets/huaweikey.jpeg)

		
## Configuring SHA256 Certificate Fingerprint

**[Configuration sample]**
 
![](/assets/huaweisha.jpg)

For more information about how to get the ```SHA256``` certificate, see [Huawei Push Access Document](http://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_introduction_agent).

<hr>

## Integration Guide

### Android Studio Integration Method

Complete the configuration required by TPNS in the build.gradle file under the app module and then add the following Huawei nodes:

1. Configure Huawei APPID

```xml
 manifestPlaceholders = [
	 HW_APPID: "Huawei APPID"
        ]
```

2. Import Huawei Push-related dependencies


```js
/* Huawei v3.2.7-release
 * Note: If the Huawei channel uses this version, the TPNS SDK also needs to use v3.2.7-release at the same time.
 */
 compile 'com.tencent.xinge:xghw:3.2.7-release'

/* Huawei v3.2.8-Release
 * Note: If the Huawei channel uses this version, the TPNS SDK also needs to use v4.0.5 at the same time.
 */
 compile 'com.tencent.xinge:xghw:3.2.8-Release'
```




### Eclipse Integration Method

1. Import the Huawei Push-related jar packages by placing ```HMSSdkBase_*.jar``` and ```HMSSdkPush_*.jar``` in the ```libs`` folder.

2. Add the following configuration to the ```Androidmanifest.xml``` file:

```xml
<meta-data
            android:name="com.huawei.hms.client.appid"
            android:value="Your APPID (from Huawei's official website)" >
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
            android:authorities="app package name.hms.update.provider"
            android:exported="false"
            android:grantUriPermissions="true" >
        </provider>      

        <receiver android:name="com.huawei.hms.support.api.push.PushEventReceiver" >
            <intent-filter>

                <!-- Receive notification bar messages from the channel, which is compatible with the old version of PUSH -->
                <action android:name="com.huawei.intent.action.PUSH" />
            </intent-filter>
        </receiver>
        
<!-- Note: This is the end required by Huawei Push -->

```
3. Configure the <a href="#华为消息receiver">Huawei message receiver</a>

#### Huawei Message Receiver

1. This is a custom class. Inherit ```com.huawei.hms.support.api.push.PushReceiver```,
  and configure the relevant nodes in ```Androidmanifest.xml```.

Sample code:

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
2. Add a custom ```Receiver``` in ```AndroidManifest.xml``` with the following configuration:

```xml
        <receiver android:name="com.tencent.android.hwpush.HWPushMessageReceiver" >
            <intent-filter>

                <!-- Required; used to receive TOKEN -->
                <action android:name="com.huawei.android.push.intent.REGISTRATION" />
                <!-- Required; used to receive message -->
                <action android:name="com.huawei.android.push.intent.RECEIVE" />
                <!-- Optional; used to trigger the onEvent callback after the notification bar or a button in the notification bar is tapped -->
                <action android:name="com.huawei.android.push.intent.CLICK" />
                <!-- Optional; used to check whether the PUSH channel is connected; not needed if there is no need to view -->
                <action android:name="com.huawei.intent.action.PUSH_STATE" />
            </intent-filter>
        </receiver>
```
### Huawei Push Start and Registration Log
- Turn on the third-party push API before calling TPNS (```XGPushManager.registerPush```):

```java
// Enable the third-party push
XGPushConfig.enableOtherPush(getApplicationContext(), true);
```

The log of successful registration is as follows:
```xml
01-15 16:40:41.116 17916-17934/? I/XINGE: [XGOtherPush] other push token is : 0865551032618726300001294600CN01 other push type: huawei
01-15 16:40:41.122 15730-15846/? I/XINGE: [a] binder other push token with accid = 2100274337  token = 17c32948df0346d5837d4748192e9d2f14c81e08 otherPushType = huawei otherPushToken = 0865551032618726300001294600CN01
```

If the log displays the following:

```
otherPushType = huawei otherPushToken = null
```

Please call the following before registering the code:

```
XGPushConfig.setHuaweiDebug(true);
```
And manually confirm that the **storage permission** is granted to the app, check the reason of error of Huawei registration failure outputted in the ```huawei.txt``` file in the SD card directory
Then, find the cause corresponding to the error code and the solution in [Huawei development documentation](http://developer.huawei.com/consumer/cn/service/hms/catalog/huaweipush_agent.html?page=hmssdk_huaweipush_api_reference_errorcode).

If the error persists, run ```adb shell setprop log.tag.hwpush VERBOSE``` and ```adb shell logcat -v time > D:/log.txt``` in cmd to start to capture the log, test, and then close the cmd window. Send the log to our technical support.

- **Note: If you need to get parameters through message tap callback or redirect to a custom page, you can use the Intent to do so. Click [here](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95) to view the tutorials.**

### Code Obfuscation

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

## Vendor-specific Channel Testing Method

1. Integrate the TPNS SDK v3.2.1 or higher in your app and integrate the required vendor-specific SDK according to the Integration Guide for Vendor-specific Channels.

2. Confirm that the relevant app information has been enter in "App configuration > Vendor-specific and global channels" in the TPNS console. Usually, the relevant configuration will take effect after 1 hour. Please wait patiently and proceed to the next step after it takes effect.

3. Install the integrated app (testing version) on a test device and run the app.

4. Keep the app running in the foreground and try to make unicast/full push to the device.

5. If the app receives the message, switch the app to the background and kill all app processes.

6. Make unicast/full push again, and if the push is received, the vendor-specific channel integration is successful.

**Note: If you need to get parameters through tap callback or redirect to a custom page, you can use the Intent to do so. Click [here](http://docs.developer.qq.com/xg/android_access/android_faq.html#%E6%B6%88%E6%81%AF%E7%82%B9%E5%87%BB%E4%BA%8B%E4%BB%B6%E4%BB%A5%E5%8F%8A%E8%B7%B3%E8%BD%AC%E9%A1%B5%E9%9D%A2%E6%96%B9%E6%B3%95) to view the tutorials.**



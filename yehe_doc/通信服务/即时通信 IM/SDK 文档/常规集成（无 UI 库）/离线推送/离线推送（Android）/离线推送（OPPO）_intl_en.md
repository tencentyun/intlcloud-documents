## Process
The following is the process of offline message push:
1. Register with the vendor and complete the developer verification process. Apply to enable the push service.
2. Create a push service and bind app information to obtain the push certificate, password, key, and other data.
3. Log in to the [IM Console](https://console.qcloud.com/avc) to upload the certificate and enter other required information. The IM server uses the certificate to generate a unique certificate ID.
4. Integrate the push messaging SDK provided by the vendor with your project and configure it according to the vendor’s instructions.
5. Send your certificate ID and device information to IM server. 
6. If the user did not log out of IM but the client was terminated by the system or user, the IM server will send push messages as notifications.

## Procedure

OPPO mobile phones use a highly customized Android system, with very strict management of the auto-start permissions of third-party apps. By default, third-party apps are not placed in the auto-start allowlist of the system. As apps running in the background are often killed by the system, we recommend that OPPO push be integrated on OPPO devices. OPPO push is a system-grade service for OPPO devices, with a high delivery rate. Currently, **IM only supports the notification bar messages of OPPO push**.

>!
>- This guide was prepared with direct reference to the official documentation of OPPO push. If OPPO push is changed, please refer to the [OPPO push documentation on the official website](https://open.oppomobile.com/wiki/doc#id=10194).
>- If you do not plan to implement an OPPO-specific offline push solution, skip this section.

[](id:Step1)
### Step 1: Apply for an OPPO PUSH certificate
1. Refer to [How to enable OPPO PUSH](https://open.oppomobile.com/wiki/doc#id=10195) for instructions on how to enable OPPO PUSH.
2. Navigate to [OPPO PUSH](https://push.oppo.com/) > **Configuration Management** > **Application Management** for detailed app information.
[](id:Step1_3)
3. Record the following: `AppId`, `AppKey`, `AppSecret`, and `MasterSecret`.

[](id:Step2)
### Step 2: Create a ChannelID

The official OPPO documentation states that ChannelIDs are required for push messages on OPPO Android 8.0 and above. Therefore, create a ChannelID for your app. Below is a sample code that creates a ChannelID called `tuikit`:

```
public void createNotificationChannel(Context context) {
        // Create the NotificationChannel, but only on API 26+ because
        // the NotificationChannel class is new and not in the support library
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            CharSequence name = "oppotest";
            String description = "this is opptest";
            int importance = NotificationManager.IMPORTANCE_DEFAULT;
            NotificationChannel channel = new NotificationChannel("tuikit", name, importance);
            channel.setDescription(description);
            // Register the channel with the system; you can't change the importance
            // or other notification behaviors after this
            NotificationManager notificationManager = context.getSystemService(NotificationManager.class);
            notificationManager.createNotificationChannel(channel);
        }
    }
```

[](id:Step3)
### Step 3: Generate a Certificate ID
1. Log in to the [IM Console](https://console.qcloud.com/avc) and click the desired app. The app configuration page appears.
2. Click **Add a certificate** under **Android push configuration**.
 >? If you already have a certificate and only need to change its information, click **Edit**.
 >
 ![](https://main.qcloudimg.com/raw/15c0ca00b00ddcc5c269489d5be93d8c.png)
3. Use the information you obtained in [Step 1](#Step1_3) and [Step 2](#Step2) to configure the following parameters:
 - **Push platform**: select **OPPO**.
 - **AppKey**: enter the **AppKey** you got from OPPO PUSH.
 - **AppID**: enter the **AppID** you got from OPPO PUSH.
 - **MasterSecret**: enter the **MasterSecret** you got from OPPO PUSH.
 - **ChannelID**: enter the **ChannelID** generated in Step 2.
 - **Click event**: the event to take place after the notification bar message is clicked. Valid values include **Open app**, **Open URL**, and **Open specific app interface**. For more information, see [Configuring Click Event](#click).
    **Open app** or **Open specific app interface** allows [custom content pass through(#Trans).
![](https://main.qcloudimg.com/raw/b4f1c81290a40c972d95cc2e63ffbbed.png)
4. Click **OK** to save the information. Certificate information takes effect 10 minutes after you save it.
5. Record the Certificate ID once it is generated.


[](id:Step4)
### Step 4: Integrate push SDK

1. Follow the instructions in the [OPPO PUSH SDK API documentation](https://open.oppomobile.com/wiki/doc#id=10196) to integrate the SDK. Use the OPPO console to test notification messages to ensure the SDK was integrated properly.
2. Use `PushManager.getInstance().register(…)`, which is part of the OPPO PUSH SDK, to initialize the Opush service.
 After the call is successfully registered, use `onRegister`, which is a `PushCallback` method, to obtain `regId`.
3. Record your `regId`.

[](id:Step5)
### Step 5: Report the push information to the IM server

If you need to use OPPO push to push IM message notification, then after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** returned by the OPPO push service to the IM server.
>! After the regId and certificate ID are correctly reported, the IM service can bind users with the corresponding device information. This enables the use of the OPPO push service to push notifications.

The following is a sample code defining Certificate ID as a constant:

```java
/****** OPPO offline push parameter start ******/
// Certificate ID generated after uploading a third-party push certificate in the Tencent Cloud console
public static final long OPPO_PUSH_BUZID = 7005;
/****** OPPO offline push parameter start end ******/
```

The following is a sample code that reports Certificate ID and regId to the IM server:

```java
/**
 * Report Certificate ID and regId to IM in ThirdPushTokenMgr.java
 */
public class ThirdPushTokenMgr {
    private static final String TAG = "ThirdPushTokenMgr";
    private String mThirdPushToken;
   
    public static ThirdPushTokenMgr getInstance () {
        return ThirdPushTokenHolder.instance;
    }
    private static class ThirdPushTokenHolder {
        private static final ThirdPushTokenMgr instance = new ThirdPushTokenMgr();
    }

    public void setThirdPushToken(String mThirdPushToken) {
        this.mThirdPushToken = mThirdPushToken;  // The regId value is passed here Describe it in accordance with the above-mentioned custom BroadcastReciever class documentation.
    }
    public void setPushTokenToTIM(){
        String token = ThirdPushTokenMgr.getInstance().getThirdPushToken();
        if(TextUtils.isEmpty(token)){
            QLog.i(TAG, "setPushTokenToTIM third token is empty");
            mIsTokenSet = false;
            return;
        }
        TIMOfflinePushToken param = null;
        if(IMFunc.isBrandXiaoMi()){     // Select different push services for different vendors.
            param = new TIMOfflinePushToken(Constants.XM_PUSH_BUZID, token);
        }else if(IMFunc.isBrandHuawei()){
            param = new TIMOfflinePushToken(Constants.HW_PUSH_BUZID, token);
        }else if(IMFunc.isBrandMeizu()){
            param = new TIMOfflinePushToken(Constants.MZ_PUSH_BUZID, token);
        }else if(IMFunc.isBrandOppo()){
            param = new TIMOfflinePushToken(Constants.OPPO_PUSH_BUZID, token);
        }else if(IMFunc.isBrandVivo()){
            param = new TIMOfflinePushToken(Constants.VIVO_PUSH_BUZID, token);
        }else{
            return;
        }
        TIMManager.getInstance().setOfflinePushToken(param, new TIMCallBack() {
            @Override
            public void onError(int code, String desc) {
                Log.d(TAG, "setOfflinePushToken err code = " + code);
            }
            @Override
            public void onSuccess() {
                Log.d(TAG, "setOfflinePushToken success");
                mIsTokenSet = true;
            }
        });
    }
}
```

### Step 6: Offline push

After the Certificate ID and regId are successfully sent, the IM server will push the notification to the client through OPPO PUSH when the app is killed by the system before the user logs out.

>?
>- For a list of frequently asked questions, refer to [OPPO PUSH FAQ](https://open.oppomobile.com/wiki/doc#id=10200).
>- If the user logs out, or is logged out by IM (such as when the user logs in on another device), the device will no longer receive push messages.

[](id:click)
## Configuring Click Events

You can select one of the following events: **Open app**, **Open URL**, or **Open specific app interface**.

[](id:App)
### Open app

This is the default event, which opens the app once the notification bar message is clicked.

[](id:Webpage)
### Open URL

You need to select **Open URL** in [Step 2](#Step2) and enter a URL that starts with either `http` or `https`, such as `https://cloud.tencent.com/document/product/269`.

[](id:AppInterface)
### Open specific app interface

These are the ways you can open a specific app interface:

**Activity** (recommended)
  This is rather simple. Enter the whole name of an Activity, such as `com.tencent.qcloud.tim.demo.SplashActivity`

**Intent action**
1. Open AndroidManifest with a text editor and configure the Activity, as follows. You must add category but no data.
```
<intent-filter>
		<action android:name="android.intent.action.VIEW" />
		<category android:name="android.intent.category.DEFAULT" />
</intent-filter>
```
2. Enter `android.intent.action.VIEW` in the console.


[](id:Trans)
## Custom Content Pass Through

### Step 1: Custom content configuration (Sender)
Set the custom content for the notification bar message before sending the message.
>! OPPO requires custom data to be in JSON format.

- Android sample:
```
  JSONObject jsonObject = new JSONObject();
  try {
  	jsonObject.put("extKey", "ext content");
  } catch (JSONException e) {
  	e.printStackTrace();
  }
  String extContent = jsonObject.toString();

  TIMMessageOfflinePushSettings settings = new TIMMessageOfflinePushSettings();
  settings.setExt(extContent.getBytes());
  timMessage.setOfflinePushSettings(settings);
  mConversation.sendMessage(false, timMessage, callback);
```

- For information on configurations for the IM server, refer to the [OfflinePushInfo Format Example](https://intl.cloud.tencent.com/document/product/1047/33527).


### Step 2: Custom content configuration (receiver)

On the console, after you set [Open app](#App) or [Open specific app interface](#AppInterface) as the click event for the push message and configure an Intent action or Activity, the client will be able to obtain the custom content from the corresponding `Activity` once the notification bar message is clicked.
```
  Bundle bundle = intent.getExtras();
  Set<String> set = bundle.keySet();
  if (set != null) {
      for (String key : set) {
      	// key and value correspond to extKey and ext content set in Step 1.
          String value = bundle.getString(key);
          Log.i("oppo push custom data", "key = " + key + ":value = " + value);
      }
  }
```

## FAQ


### Can I set a custom notification sound?

OPPO does not support custom notification sounds.

### I cannot receive push messages. What should I do?
1. No push service is 100% successful in reaching target users, and vendor push is no exception. Therefore, if one or two push messages fail to reach users during a fast, continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. Make sure the correct push certificate information from OPPO is properly configured in the [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [OPPO push SDK integration](#Step4) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#Step5) to the IM server correctly.
5. Manually kill the app on your device, send a few messages, and confirm whether you receive notifications within one minute.


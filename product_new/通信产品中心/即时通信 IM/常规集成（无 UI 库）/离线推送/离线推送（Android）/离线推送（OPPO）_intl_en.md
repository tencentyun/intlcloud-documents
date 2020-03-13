## Process Description
The process of implementing offline message push is as follows:
1. A developer registers an account on a vendor’s platform, and after passing developer verification, the developer applies for the push service.
2. Create the push service, bind it with an app, and obtain information such as the push certificate, password, and key.
3. Log in to [IM Console](https://console.qcloud.com/avc) and specify the push certificate and relevant information. The IM server generates a different certificate ID for each certificate.
4. Integrate the push SDK provided by the vendor with the developer’s project and configure it based on the vendor’s requirements.
5. After integrating the IM SDK with the project, report the certificate ID, device information, and other information to the IM server.
6. When the client app is killed by the system or user without IM logout, the IM server sends notifications to the user through message push.

## Directions

OPPO mobile phones use a highly customized Android system, with very strict management of the auto-start permissions of third-party apps. By default, third-party apps are not included in the auto-start whitelist of the system. As apps running in the background are often killed by the system, we recommend that OPPO push be integrated on OPPO devices. OPPO push is a system-grade service for OPPO devices, with a high delivery rate. Currently, **IM only supports the notification bar messages of OPPO push**.

>
>- **At present, the OPPO push service is available only to apps that are already in OPPO’s app store. Therefore, the current demo has no sample of OPPO push.**
>- This document was prepared with direct reference to the official documentation of OPPO push. If OPPO push is updated, refer to OPPO push documentation on the official website.
>- If you do not need to implement special offline push adaptation for OPPO devices, ignore this section.

<span id="Step1"></span>
### Step 1: Apply for an OPPO push certificate
1. Refer to the OPPO push service activation guide to activate the push service.
2. Go to the OPPO push platform and choose **Configuration Management** > **App Configuration** to view detailed app information.
<span id="Step1_3"></span>
3. Record the `AppId`, `AppKey`, `AppSecret`, and `MasterSecret` items.

<span id="Step2"></span>
### Step 2: Host the certificate to IM
1. Log in to Tencent Cloud [IM Console](https://console.qcloud.com/avc) and click the target app card to go to the basic configuration page of the app.
2. Click **Add Certificate** in the **Android Platform Push Settings** area.
 > If you already have a certificate and only want to change its information, you can click **Edit** in the **Android Platform Push Settings** to modify and update the certificate.
 >
3. Set the following parameters based on the information obtained in [Step 1](#step-1.3A-apply-for-a-oppo-push-certificate):
 - **Push Platform**: select **OPPO**.
 - **AppKey**: enter the **AppKey** of the OPPO push service app.
 - **AppID**: enter the **AppId** of the OPPO push service app.
 - **MasterSecret**: enter the **MasterSecret** of the OPPO push service app.

4. Click **OK** to save the settings. The certificate information will take effect within 10 minutes after being saved.
5. Record the **`ID`** of the certificate after the push certificate information is generated.


<span id="Step3"></span>
### Step 3: Integrate the push SDK

1. Refer to OPPO PUSH SDK API documentation to integrate the SDK and test notification messages in the OPPO console to ensure that it has been integrated successfully.
2. Call `PushManager.getInstance().register(…)` in the OPPO SDK to initialize the Opush service.
 After successful registration, you can obtain `regId` in the `onRegister` callback method of `PushCallback`.
3. Record the `regId` information.

<span id="Step4"></span>
### Step 4: Report the push information to the IM server

If you need to use OPPO push to push IM message notifications, then after **successful user login**, you must use the `setOfflinePushToken` method of `TIMManager` to report the **certificate ID** generated and hosted by the IM console and **regId** returned by the OPPO push service, to the IM server.
> After the regId and certificate ID are correctly reported, the IM service can bind users with the corresponding device information. This enables the use of the OPPO push service to push notifications.

Sample code for defining the certificate ID constant:

```java
/****** Start of OPPO offline push parameters ******/
// Certificate ID assigned for the third-party push certificate uploaded to the Tencent Cloud console
public static final long OPPO_PUSH_BUZID = 7005;
/****** End of OPPO offline push parameters ******/
```

Sample code for reporting the certificate ID and regId:

```java
/**
 * Report the push certificate ID and device information in ThirdPushTokenMgr.java
 */
public class ThirdPushTokenMgr {
    private static final String TAG = "ThirdPushTokenMgr";
    private String mThirdPushToken;
    private boolean mIsTokenSet = false;
    private boolean mIsLogin = false;
    public static ThirdPushTokenMgr getInstance () {
        return ThirdPushTokenHolder.instance;
    }
    private static class ThirdPushTokenHolder {
        private static final ThirdPushTokenMgr instance = new ThirdPushTokenMgr();
    }
    public void setIsLogin(boolean isLogin){
        mIsLogin = isLogin;
    }
    public String getThirdPushToken() {
        return mThirdPushToken;
    }
    public void setThirdPushToken(String mThirdPushToken) {
        this.mThirdPushToken = mThirdPushToken;  // Here, the regId value is passed in. Describe it based on the aforementioned custom BroadcastReciever class documentation.
    }
    public void setPushTokenToTIM(){
        if(mIsTokenSet){
            QLog.i(TAG, "setPushTokenToTIM mIsTokenSet true, ignore");
            return;
        }
        String token = ThirdPushTokenMgr.getInstance().getThirdPushToken();
        if(TextUtils.isEmpty(token)){
            QLog.i(TAG, "setPushTokenToTIM third token is empty");
            mIsTokenSet = false;
            return;
        }
        if( !mIsLogin ){
            QLog.i(TAG, "setPushTokenToTIM not login, ignore");
            return;
        }
        TIMOfflinePushToken param = null;
        if(IMFunc.isBrandXiaoMi()){     // Identify the vendor brand and choose different push services for different vendors
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

### Step 5: Offline push

After the certificate ID and regId are successfully reported, the IM server sends messages through OPPO push notifications to the user when the app has been killed but the user has not logged out of IM.

>
>- If the IM user has logged out or was forced logout by the IM server (for example, due to login on another terminal), the device will not receive push messages.


## FAQs


### Can I customize the push notification sound?

Currently, OPPO push does not support custom notification sounds.

### How can I identify the cause of failures to receive push messages?
1. No push service guarantees 100% success in reaching target users and zero vendor push exceptions. Therefore, if one or two push messages fail to reach users during a fast and continuous push process, it is usually due to the restrictions of vendor push frequency control.
2. According to the push process, confirm whether the OPPO push certificate information is correctly configured in [IM Console](https://console.qcloud.com/avc).
3. Confirm that your project’s [OPPO push SDK integration](#step-3.3A-integrate-the-push-sdk) configuration is correct and that you have obtained the regId.
4. Confirm that you have [reported push information](#step-4.3A-report-the-push-information-to-the-im-server) to the IM server correctly.
5. Manually kill the app on your device, send several messages, and confirm whether you can receive notifications within one minute.
6. If you still cannot receive push messages after the preceding steps, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the specific `time`, `SDKAppID`, `certificate ID`, and `push receiving UserID` for processing.

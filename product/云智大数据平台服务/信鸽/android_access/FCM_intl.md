# Integration Guide for FCM Channel

FCM channel is a push channel launched by TPNS and Google, which allows Google Services Framework-enabled mobile phones outside mainland China to receive push messages without opening the app. In phone ROMs without FCM, the TPNS push channel will be used.

## Getting FCM Push Key
1. Register the app at [FireBase's official website](https://firebase.google.com/?hl=zh-cn). Configure the obtained FCM app push server key and SenderID to the TPNS console.
2. Download the google-services.json file.
See the figure below:

Get the json file:
![](/assets/获取fcmjson.jpeg)

Get the server key:
![](/assets/获取服务器密钥.jpeg)


## AS Development Integration Method

1. Configure the google-services.json file. See the figure below:

![](/assets/配置json.png)


2. Configure gradle to integrate the Google service.

a) Add the following code to the dependencies node in the project-level build.gradle file:
```xml
classpath 'com.google.gms:google-services:3.1.0'
```
Add dependencies to the app-level build.gradle file
```xml

compile 'com.tencent.xinge:fcm:4.3.0-beta'


compile 'com.google.firebase:firebase-messaging:17.3.1'


 // Add the following as the last line of code to the app-level gradle file and place google-services.json into the root path of your app's model

apply plugin: 'com.google.gms.google-services'

```
## Eclipse Development Integration Method

Add the following configuration on the basis of TPNS integration:

1. Configure the google-services.json file and place it in the assets directory.

2. Place Xg4FCM-v4.xxx.jar, firebase-common-12.0.1.jar, firebase-iid-12.0.1.jar, firebase-messaging-12.0.1.jar, play-services-base-12.0.1.jar, and play-services-basement-12.0.1.jar in the libs directory.

3. Add the following configuration to AndroidManifest.xml:

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
                             <!-- Change the following to the package name of the app -->
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
        <!-- 9080000 is the version of google-play-services.jar, and the Google Play service version on the phone must be higher than this value -->
        <meta-data android:name="com.google.android.gms.version" android:value="9080000" /> 
        <!-- [END instanceId_listener] -->

</application>

<!-- [START gcm_permission] -->
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    <!-- Declare and use a custom permission to ensure that only this program can receive your GCM messages. If the system is v4.1 or higher, this permission is not required. Change com.qq.xgdemo to the app package name -->
    <permission android:name="app package name.permission.C2D_MESSAGE"  android:protectionLevel="signature" />
    <uses-permission android:name="app package name.permission.C2D_MESSAGE" />
    <!-- [END gcm_permission] -->
```

## Enabling FCM Push


Add the following code setting before the TPNS registration calling code (XGPushManager.registerPush):

```java
XGPushConfig.enableFcmPush(this,true);
XGPushConfig.enableOtherPush(this, true);
```
The log of successful FCM registration is as follows:

```xml
12-02 09:16:31.874 17260-17423/lc.com.xinge.push E/XG_fcm: Fcm App has initialize 
12-02 09:16:31.874 17260-17423/lc.com.xinge.push D/XG_fcm: Firebase app initialization completed
12-02 09:16:31.875 17260-17423/lc.com.xinge.push I/XG_fcm: registerPush Token is: eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI
12-02 09:16:31.877 17260-17260/lc.com.xinge.push W/FA: Service connection failed: ConnectionResult{statusCode=SERVICE_VERSION_UPDATE_REQUIRED, resolution=null, message=null}
12-02 09:16:31.892 17260-17278/lc.com.xinge.push V/FA: Using measurement service
12-02 09:16:31.893 17260-17278/lc.com.xinge.push V/FA: Connecting to remote service
12-02 09:16:31.895 17260-17423/lc.com.xinge.push I/XINGE: [XGOtherPush] Reservert info: other push token is : eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI  other push type: fcm
```

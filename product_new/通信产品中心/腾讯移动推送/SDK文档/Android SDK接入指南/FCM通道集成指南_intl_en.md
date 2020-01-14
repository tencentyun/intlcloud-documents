# FCM channel integration guide

## Operation Scenario

FCM channels are system-level push channels provided by Google. If you use a mobile phone with the Google service framework overseas, you can receive push notifications without opening apps. If the mobile phone ROM has no FCM, TPNS push channel will be used.
## Steps

### 1. Getting the FCM push key
1. Register the app at [FireBase official website](https://firebase.google.com/?hl=en-us). Configure the FCM app push server key and SenderID to the TPNS console.
2. Download the google-services.json file.
As shown in the figure below:

Get the json file:
![](https://main.qcloudimg.com/raw/a3b3fbb86180fde824d7970f00418513.png)
Get the server key:
![](https://main.qcloudimg.com/raw/35e4dc46af79a52f4f200b1ef085f19f.png)

## Configuring Content

1. Configure the google-services.json file, as shown in the following figure:
![](https://main.qcloudimg.com/raw/60e855aaf46d86e8e32a057dc5a948f3.png)
2. Configure gradle to integrate the Google service.
a) Add the following code to the dependencies node in the project-level build.gradle file:
```xml
classpath 'com.google.gms:google-services:4.2.0'
```
**Note: If you use a version below 4.2.0, the following message will appear: FCM Register error! java.lang.IllegalStateException: Default FirebaseApp is not initialized in this process com.qq.xg4all. Make sure to call FirebaseApp.initializeApp(Context) first.  
Solution: You can add the following to string.xml under the res/values folder:
<string name="google_app_id">YOUR_GOOGLE_APP_ID</string>**

Add dependencies to the app-level build.gradle file
```xml

implementation 'com.tencent.tpns:fcm:[VERSION]-release'// [VERSION] is the current SDK version number.

implementation  'com.google.firebase:firebase-messaging:17.6.0'



 // In the app-level gradle file, add the following to the last line of the code and put google-services.json into the root path of your app model

apply plugin: 'com.google.gms.google-services'

```
**Note: Google configures google-play-services (TPNS only uses it to detect whether the device supports Google services. We recommend you use a version higher than 17.0.0, otherwise you may not be able to register for FCM). For more information, see documentation at: https://developers.google.com/android/guides/setup#add_google_play_services_to_your_project**


## Enabling FCM push


Add the following code setting before the TPNS calling registration code (XGPushManager.registerPush):

```java
XGPushConfig.enableOtherPush(this, true);
```
The log of a successful FCM registration is as follows:

```xml
 E/XG_fcm: Fcm App has initialized 
 D/XG_fcm: FirebaseAPP initialization complete
 I/XG_fcm: registerPush Token is: eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI
12-02 09:16:31.877 17260-17260/lc.com.xinge.push W/FA: Service connection failed: ConnectionResult{statusCode=SERVICE_VERSION_UPDATE_REQUIRED, resolution=null, message=null}
12-02 09:16:31.892 17260-17278/lc.com.xinge.push V/FA: Using measurement service
12-02 09:16:31.893 17260-17278/lc.com.xinge.push V/FA: Connecting to remote service
12-02 09:16:31.895 17260-17423/lc.com.xinge.push I/XINGE: [XGOtherPush] Reservert info: other push token is : eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI  other push type: fcm
```


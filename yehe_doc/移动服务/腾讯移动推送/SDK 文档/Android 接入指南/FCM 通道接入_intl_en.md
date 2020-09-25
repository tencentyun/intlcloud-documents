

## Overview
The FCM channel is a system-level push channel provided by Google. On mobile phones with the Google service framework, as the background processes are managed loosely, push notifications can be received if application processes are not force stopped.

## Directions
### Getting key
Register the application at FireBase official website and enter the FCM application push server key and `SenderID` in the TPNS Console.

### Configuration
1. Configure the `google-services.json` file as shown below:
![](https://main.qcloudimg.com/raw/568561b72a775058bf06750bfab38ed0.png)
2. Configure gradle to integrate the Google service.
  1. Add the following code to the `dependencies` node in the project-level `build.gradle` file:
```xml
classpath 'com.google.gms:google-services:4.2.0'
```
>!Note: if you use a version below 4.2.0, the following message will be displayed: `FCM Register error! java.lang.IllegalStateException: Default FirebaseApp is not initialized in this process com.qq.xg4all. Make sure to call FirebaseApp.initializeApp(Context) first.` We recommend you add `YOUR_GOOGLE_APP_ID` to `string.xml` in the `res/values` folder.

  2. Add dependencies to the application-level `build.gradle` file:
	```xml
	  implementation 'com.tencent.tpns:fcm:[VERSION]-release' // FCM push [VERSION] is the version number of the current SDK, which can be viewed on the SDK download page
      implementation  'com.google.firebase:firebase-messaging:17.6.0'

	 // In the application-level gradle file, add the following to the last line of the code and put `google-services.json` into the root path of your application model
	apply plugin: 'com.google.gms.google-services'
	```
>!
>- FCM push [VERSION] is the version number of the current SDK, which can be viewed on the [SDK download page](https://console.cloud.tencent.com/tpns/sdkdownload).
>- Google configures `google-play-services` (we recommend you use a version higher than 17.0.0; otherwise, you may not be able to register for FCM).

### Enabling FCM push
Add the following code setting before the TPNS calling registration code (XGPushManager.registerPush):

```java
XGPushConfig.enableOtherPush(this, true);
```
The log of a successful FCM registration is as follows:

```xml
 E/XG_fcm: Fcm App has initialize 
 D/XG_fcm: FirebaseAPP initialization completed
 I/XG_fcm: registerPush Token is: eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI
12-02 09:16:31.877 17260-17260/lc.com.xinge.push W/FA: Service connection failed: ConnectionResult{statusCode=SERVICE_VERSION_UPDATE_REQUIRED, resolution=null, message=null}
12-02 09:16:31.892 17260-17278/lc.com.xinge.push V/FA: Using measurement service
12-02 09:16:31.893 17260-17278/lc.com.xinge.push V/FA: Connecting to remote service
12-02 09:16:31.895 17260-17423/lc.com.xinge.push I/XINGE: [XGOtherPush] Reservert info: other push token is : eK0LLz43Z_U:APA91bHjyTCuX7fZ6Ye-fAojAo_l2nphA3rRtLZN98grADOZtULysxYd51pCaL5oiqyVs0Mtbfu2mBdjoeGsSq5sjbh5mCETgl2dURRy9-yNR_ZZrn6pWcvwt7CoWTY0_Q9_mreiryuI  other push type: fcm
```


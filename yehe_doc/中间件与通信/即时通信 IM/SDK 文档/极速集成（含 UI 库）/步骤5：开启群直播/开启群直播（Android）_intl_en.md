`TUIKit` `5.0.10` and later versions support group livestreaming and interconnection between the iOS and Android platforms. To implement group livestreaming, you need to [integrate the TUIKitLive component](#step2) as well.


If the Tencent Real-Time Communication (TRTC) service is not activated, enable group livestreaming as follows:

[](id:step1)

## Step 1: Activate the TRTC Service
1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the pop-up dialog box.
>? A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.

[](id:step2)
## Step 2: Integrate TUIKitLive 
You are advised to use the source code to integrate ``TUIKit`` and ``TUIKit-Live``. In this way, you can modify the source code to meet your business needs. To integrate ``TUIKit`` and ``TUIKit-Live``, add the following to the `build.gradle` file:

```groovy
implementation project(':tuikit')
implementation project(':tuikit-live')
```

[](id:step3)
## Step 3: Initialize TUIKit 
To initialize `TUIKit`, import the `SDKAppID` generated in [Step 1](#step1). (If your project is integrated with `TUIKit`, skip this step.)
```java
TUIKit.init(Context, SDKAppID, new ConfigHelper().getConfigs());
```

[](id:step4)
## Step 4: Log In to TUIKit
Call the `login` API provided by `TUIKit` to log in to IM. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). (If your product is integrated with `TUIKit`, skip this step.)

```java
TUIKit.login("userId", "userSig", new IUIKitCallBack() {
	@Override
	public void onError(String module, final int code, final String desc) {
		Log.i(TAG, "onError: login failed");
	}

	@Override
	public void onSuccess(Object data) {
		Log.i(TAG, "onSuccess: login successful");
	}
});
```

[](id:step5)
## Step 5: Enable/Disable Group Livestreaming
In `TUIKit-Live`, group livestreaming is enabled by default. If you do not need group livestreaming, disable it in the `TUIKitLiveChatController.java` file of the `TUIKit-Live` module. The code is as follows:

```java
// Values of `enableGroupLiveEntry`: true (enable); false (disable). Default value: true
private boolean enableGroupLiveEntry = false;
```

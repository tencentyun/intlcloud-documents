TUIKit 5.0.10 and later versions support group livestreaming and interconnection between the iOS and Android platforms. To implement group livestreaming, you need to [integrate the TUIKitLive component](#step2) as well.


If the Tencent Real-Time Communication (TRTC) service is not activated, enable group livestreaming as follows:

[](id:Step1)

## Step 1: Activate the TRTC Service

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target app card to go to the basic configuration page of the app.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the pop-up dialog box.
>?A TRTC app with the same SDKAppID as the IM app will be created in the [TRTC console](https://console.cloud.tencent.com/trtc). You can use the same account and authentication information for IM and TRTC.

[](id:step2)
## Step 2: Integrate TUIKitLive

1. Add the following content to the podfile file.
 ```
pod 'TXIMSDK_TUIKit_live_iOS'                // By default, the audio and video library of the TXLiteAVSDK_TRTC version is integrated.
// pod 'TXIMSDK_TUIKit_live_iOS_Professional' // By default, the audio and video library of the TXLiteAVSDK_Professional version is integrated.
 ```
Do not integrate different Tencent Cloud [audio and video libraries](https://intl.cloud.tencent.com/document/product/647/34615) at the same time to avoid symbol conflicts. If you use a library not of the [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) version, we recommend that you remove it and integrate the `TXIMSDK_TUIKit_iOS_Professional` version. The audio and video library of the [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) version contains all basic audio and video capabilities.

2. Run the following command to download the third-party library to the current project:
```
pod install
```
 If you cannot install the latest TUIKit version, run the following command to update the local CocoaPods repository list:
```
 pod repo update
```

[](id:step3)
## Step 3: Initialize TUIKit 
To initialize TUIKit, import the SDKAppID generated in [Step 1](#Step1). (If your project is integrated with TUIKit, skip this step.)
```
[[TUIKit sharedInstance] setupWithAppId:SDKAppID];
```

[](id:step4)
## Step 4: Log In to TUIKit
Call the `login` API provided by TUIKit to log in to IM. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). (If your project is integrated with TUIKit, skip this step.)

```
[[TUIKit sharedInstance] login:@"userID" userSig:@"userSig" succ:^{
     NSLog(@"-----> login succeeds");
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> login fails");
}];
```

[](id:step5)
## Step 5: Enable/Disable Group Livestreaming
In TUIKitLive, group livestreaming is enabled by default. If you do not need group livestreaming, use the ``enableGroupLiveEntry`` attribute in ``TUIKitLive.h`` to disable it. The code is as follows:

```
// Values of `enableGroupLiveEntry`: YES (enable); NO (disable). Default value: YES
[TUIKitLive shareInstance].enableGroupLiveEntry = YES;
```

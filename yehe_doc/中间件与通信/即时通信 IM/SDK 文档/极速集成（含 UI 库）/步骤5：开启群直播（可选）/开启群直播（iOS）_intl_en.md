Projects integrated with TUIKit provide a group livestreaming entry by default.
If the Tencent Real-Time Communication (TRTC) service is not activated, enable group livestreaming as follows:

<span id="Step1"></span>

## Step 1: Enable the TRTC Service

1. Log in to the [IM console](https://console.cloud.tencent.com/im) and click the target application card to go to the basic configuration page of the application.
2. Click **Activate** under **Activate Tencent Real-Time Communication (TRTC)**.
3. Click **Confirm** in the dialog box that appears.

>?A TRTC application with the same SDKAppID as the IM application is created in the [TRTC console](https://console.cloud.tencent.com/trtc/app). You can use the same account and authentication information for IM and TRTC.

<span id="step2"></span>
## Step 2: Initialize TUIKit 
To initialize TUIKit, import the SDKAppID generated in [Step 1](#step1). (If your project has already integrated with TUIKit, skip this step.)
```
[[TUIKit sharedInstance] setupWithAppId:SDKAppID];
```

<span id="step3"></span>
## Step 3: Log In to TUIKit
Call the `login` API provided by TUIKit to log in to IM. For more information on how to generate UserSig, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). (If your application is integrated with TUIKit, skip this step.)

```
[[TUIKit sharedInstance] login:@"userID" userSig:@"userSig" succ:^{
     NSLog(@"-----> login successful");
} fail:^(int code, NSString *msg) {
     NSLog(@"-----> login failed");
}];
```

<span id="step4"></span>
## Step 4: Enable/Disable Group Livestreaming
In TUIKitLive, group livestreaming is enabled by default. If you do not need group livestreaming, disable the group livestreaming entry through TUIKit configuration. The code is as follows:

```
// enableGroupLiveEntry true: enable; false: disable; default value: true
[TUIKit sharedInstance].config.enableGroupLiveEntry = YES;
```

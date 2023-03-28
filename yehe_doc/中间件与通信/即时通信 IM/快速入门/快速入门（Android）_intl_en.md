## Directions
[](id:step1)
### Step 1. Create an app
1. Log in to the [Chat console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 Chat apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
>
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. After creation, you can see the status, service version, SDKAppID, creation time, tag, and expiry time of the new app on the overview page of the console. Record the SDKAppID.
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)


[](id:step2)
### Step 2. Obtain key information
1. Click the target app card to go to the basic configuration page of the app.
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
2. In the **Basic Information** area, click **Display key**, and then copy and save the key information.
>! Store the key information properly to prevent disclosure.

[](id:step3)
### Step 3. Download and configure the demo source code

1. Download the Chat demo project. For more download information, see [SDK Download](https://intl.cloud.tencent.com/document/product/1047/33996).
>? To respect the copyright of emoji design, the downloaded demo project does not contain sliced images of major emoji elements. You can use your local emoji packs to configure code. Unauthorized use of the emoji pack in the Chat demo may infringe on the design copyright.
2. Open the project in the terminal directory and find the file `GenerateTestUserSig` in `Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java`.
3. Set relevant parameters in the `GenerateTestUserSig` file:

 - SDKAPPID: set it to the SDKAppID obtained in [Step 1](#step1).
 - SECRETKEY: enter the key obtained in [Step 2](#step2).
 ![](https://qcloudimg.tencent-cloud.cn/raw/928dd6de772f31c5328737050baf8c5a.png)


>! In this document, the method to obtain `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
> The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain a dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step4)
### Step 4. Compile and run the demo
Import the demo project with Android Studio, and then compile and run it.
For more information, see the file `README.md` in the corresponding directory of the demo project cloned in [Step 3](#step3).

**Environment requirements**
- Android Studio-Chipmunk 
- Gradle-6.7.1
- Android Gradle Plugin Version-4.2.0
- kotlin-gradle-plugin-1.5.31

>!The demo is integrated with the audio/video call feature by default. However, the TRTC SDK on which the audio/video call feature relies currently does not support simulators. Please use real devices for demo running or debugging.

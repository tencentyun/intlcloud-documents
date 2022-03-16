This document describes how to quickly run the IM demo for web.
                    

## Demo UI
![](https://qcloudimg.tencent-cloud.cn/raw/fe5b7406d6b6061918c393019aee2980.png)


## Directions
[](id:step1)
### Step 1. Create an app
1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>? If you already have an app, record its SDKAppID and [obtain key information](#step2).
>A Tencent Cloud account can create a maximum of 300 IM apps. If you want to create a new app, [disable and delete](https://intl.cloud.tencent.com/document/product/1047/34540) an unwanted app first. **Once an app (along with its SDKAppID) is deleted, the service it provides and all its data are lost. Proceed with caution**.
2. Click **Create Application**, enter your app name, and click **Confirm**.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. Go to the [overview page](https://console.cloud.tencent.com/im) to view the status, edition, `SDKAppID`, creation time, tag, and expiration time of the application created. Record the `SDKAppID`.
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)


[](id:step2)
### Step 2. Obtain key information
1. Click the target app card to go to the basic configuration page of the app.
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
2. In the **Basic Information** area, click **Display key**, and then copy and save the key information.
>! Please store the key information properly to prevent disclosure.

[](id:step3)
### Step 3. Download and configure the demo source code

1. Download the SDK and matching [demo source code](https://intl.cloud.tencent.com/document/product/1047/33996).
<dx-codeblock>
:::  js

# Run in CLI
git clone https://github.com/tencentyun/TIMSDK.git

# Go to the web project

cd TIMSDK/Web/Demo

# Install dependencies
npm install
:::
</dx-codeblock>
2. Open the project in the web directory, and find the file `GenerateTestUserSig` via the path /public/debug/GenerateTestUserSig.js.
3. Set relevant parameters in the `GenerateTestUserSig` file:
 - SDKAPPID: set it to the SDKAppID obtained in [Step 1](#step1).
 - SECRETKEY: enter the key obtained in [Step 2](#step2).


>! In this document, the method to obtain `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
> The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain a dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step4)
### Step 4. Compile and run the demo
Run the following command in the project terminal via the browser:
<dx-codeblock>
:::  js
# Run in CLI
npm run start
:::
</dx-codeblock>

## References

- [SDK API Documentation](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo Source Code](https://github.com/tencentyun/TIMSDK/tree/master/Web/Demo)

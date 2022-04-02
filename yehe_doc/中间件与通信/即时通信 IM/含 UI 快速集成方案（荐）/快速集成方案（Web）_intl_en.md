Web demo is a set of UI components based on the IM SDK. It provides features such as conversation, chat, search, relationship chain, group, and audio/video call. You can use these UI components to quickly build your own business logic.

## Feature Description 

| Feature | Description |
|---------|---------|
| Search | Searches for and displays conversations or messages |
| Conversation | Pulls and displays the conversation list |
| Chat | Receives, sends, and displays messages |
| Relationship Chain | Pulls and displays the friend list |
| Group | Pulls and displays group information |
| Audio/Video Call | Makes audio/video calls |


## Directions
[](id:step1)

### Step 1. Download the source code
Download the SDK and [demo source code](https://intl.cloud.tencent.com/document/product/1047/33996) that fit your needs.
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

### Step 2. Initialize the demo

1. Open the project in the web directory, and find the `GenerateTestUserSig` file via the path /public/debug/GenerateTestUserSig.js.
2. Set required parameters in the `GenerateTestUserSig` file, where `SDKAppID` and `Key` can be obtained in the [IM console](https://console.cloud.tencent.com/im). Click the card of the target app to go to its basic configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
3. In the **Basic Information** section, click **Display key**, and copy and save the key information to the `GenerateTestUserSig` file.

>! In this document, the method to obtain `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
> The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain a dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).


### Step 3. Integrate static resources
Integrate static resources (such as tools and images) into your project.
  <img src="https://qcloudimg.tencent-cloud.cn/raw/f0aff5e265cac1d7eefab7fa53bda545.png"   width = "200">

### Step 4. Integrate necessary modules
1. Copy all components to your project:
![](https://qcloudimg.tencent-cloud.cn/raw/18a5f940d61cb15c3979cf6944152bb2.png)
2. Alternatively, only integrate the modules you need. Take the conversation module as an example:
![](https://qcloudimg.tencent-cloud.cn/raw/8b9573f02146f3958af080bd07f716eb.png)

### Step 5. Update the route
Update the route based on the imported modules:
  <img src="https://qcloudimg.tencent-cloud.cn/raw/38733003ae12c255d615897102149097.png"   width = "200">

## References

- [SDK API Documentation](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK Update Log](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo Source Code](https://github.com/tencentyun/TIMSDK/tree/master/Web/Demo)


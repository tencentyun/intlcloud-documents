The web demo is implemented based on the IM TUIKit. TUIKit provides features such as management of conversations, chats, groups, and profiles. With TUIkit, you can quickly build your own business logic.

## Demo UI

### Conversation management

| Initiate a Conversation | Conversation List | Manage the Conversation List |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/562deec9715ae2c50f65e8d40c4d7cac.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/990204616a1c551c36ff5bdc57caa66c.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/695589f54d4ac0b9bb9bc24eb97c7e6d.png) |

### Chat management

| Message List | Send Messages | Manage Group Chats |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/8cb4fd0813a7ce0f3cab8468098dd896.png) |![](https://qcloudimg.tencent-cloud.cn/raw/f931993108c14ba3b2e628e4ed50a316.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/bb9b0449eb712f9e6fececfdb199418a.png) |



| Feature | Description |
| --- | --- |
| Conversation management | 1. Initiate a one-to-one or group chat <br/>2. Display the conversation list <br/>3. Manage the conversation list |
| Chat management | 1. Display the message list <br/>2. Send messages <br/>3. Manage group chats |


## Running the demo

### Step 1. Download the source code

Download the SDK and [demo source code](https://github.com/TencentCloud/TIMSDK) that fit your needs.

```shell
# Run the code in CLI
git clone https://github.com/TencentCloud/TIMSDK.git

# Go to the web project

cd TIMSDK/Web/Demo

# Install dependencies of the demo
npm install

cd TIMSDK/Web/Demo/src/TUIKit

# Install dependencies of the TUIKit
npm install
```

### Step 2. Initialize the demo
1. Open the project in the web directory, and find the `GenerateTestUserSig` file via the path `/debug/GenerateTestUserSig.js`.
2. Set required parameters in the `GenerateTestUserSig` file, where `SDKAppID` and `Key` can be obtained in the [IM console](https://console.cloud.tencent.com/im). Click the target app card to go to its basic configuration page. 
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
3. In the **Basic Information** area, click **Display key**, and copy and save the key information to the `GenerateTestUserSig` file. 


> ! In this document, the method to obtain `UserSig` is to configure a `SECRETKEY` in the client code. In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**. The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see the "Calculating UserSig on the Server" section of [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Step 3. Launch the project

```shell
# Launch the project
npm run serve
```

- [SDK APIs Documentation](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [Update Logs (Web)](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo Source Code](https://github.com/TencentCloud/TIMSDK/tree/master/Web/Demo)

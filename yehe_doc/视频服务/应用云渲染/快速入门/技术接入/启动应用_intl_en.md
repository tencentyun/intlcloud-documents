## Starting an Application
This section describes how to start a cloud application.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/dec8b73715e1a2e80f62a298fffba0e0.jpg)

Refer to the following, which appear in the diagram:

| Role | Description |
| ------ | ------ |
| CAR SDK | CAR client SDKs include the [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/1158/49627), [SDK for Android](https://intl.cloud.tencent.com/document/product/1158/49628), and [SDK for iOS](https://intl.cloud.tencent.com/document/product/1158/49629) <br>This document takes the SDK for JavaScript as an example. |
| Business client | A platform provided by your business for users. |
| Business backend | Your backend service. |
| CAR backend | [Tencent Cloud APIs](https://www.tencentcloud.com/document/product/1158/49958) provided by CAR. |
| Cloud application | The cloud service running the business application. |

### Directions
1. The business client calls the [TCGSDK.init()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.init(params)) API to perform initialization. After initialization, it calls the [TCGSDK.getClientSession()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.getClientSession()) API to get `ClientSession` of the client.
2. [](id:step2)The business client requests the business backend to start the application based on parameters passed in such as `UserId` and `ClientSession`. Here, `UserId` is the unique user identifier customized by the business and should remain unchanged during user queuing and application reconnection.
3. The business backend calls the [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) API through the TencentCloud API to apply to reserve a concurrency. If there are no available concurrencies or an error is returned, go back to **step 2** to send a request again.
4. The business backend calls the [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968) API to create a session and returns `ServerSession` to the business client.
5. The client calls the [TCGSDK.start()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.start(serverSession)) API to start the cloud application. After the application is connected, the SDK will trigger the `onConnectSuccess()` callback. We recommend you call the data channel creation API and APIs for other features after this callback.

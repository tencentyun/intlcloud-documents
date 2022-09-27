## CAR Description
CAR runs your application client (application with an engine such as UE or Unity) on a cloud computing resource with GPU and enables users to access the cloud application through a video stream. Before reading this document, make sure you understand the [basic technical concepts](https://intl.cloud.tencent.com/document/product/1158/49611) of CAR.

## CAR Integration
### Preparations for Access
![](https://qcloudimg.tencent-cloud.cn/raw/7c03a9fc66cfa851e742b6bdb79a738b.jpg)

[](id:step1)

### Step 1. Sign up for a Tencent Cloud account
If you don't have a Tencent Cloud account yet, [sign up for one](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) first.

[](id:step2)
### Step 2. Apply to activate CAR
After [applying to activate CAR](https://intl.cloud.tencent.com/apply/p/ombzi6237bn), you can start using the CAR console.

[](id:step3)
### Step 3. Perform operations in the console
In the console, we recommend you first [upload an application](https://intl.cloud.tencent.com/document/product/1158/49618), [create a project](https://intl.cloud.tencent.com/document/product/1158/49622), and [purchase a concurrency pack](https://intl.cloud.tencent.com/document/product/1158/49625). Eventually, you will associate the project with an application and allocate available concurrencies. The project ID is the unique ID for you to schedule CAR services.

[](id:step4)
### Step 4. Integrate CAR PaaS
CAR PaaS provides [TencentCloud APIs](https://intl.cloud.tencent.com/document/product/1158/49958) and SDKs for various client types, including the [JavaScript SDK](https://intl.cloud.tencent.com/document/product/1158/49627), [SDK for Android](https://intl.cloud.tencent.com/document/product/1158/49628), and [SDK for iOS](https://intl.cloud.tencent.com/document/product/1158/49629). You need to develop both the backend and the frontend.

[](id:step5)

### Step 5. Pull CAR for the first time

1. **The client initializes the CAR SDK**:
No matter which type of client you use, you can get `ClientSession` after the SDK is initialized successfully. `ClientSession` will be used by the business server to get `ServerSession` subsequently. The specific initialization and acquisition methods for each client type are as detailed below:
   - **JavaScript SDK**: The business client calls the [TCGSDK.init(params)](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.init(params)) API to perform initialization. After initialization, the client calls the [TCGSDK.getClientSession()](https://intl.cloud.tencent.com/document/product/1158/49627#tcgsdk.getclientsession()) function to get its `ClientSession`.
   - **SDK for Android**: The business client calls the `TcrSdk.getInstance().init(context, null, new AsyncCallback<Void>())` API to perform initialization. The client gets its `ClientSession` in the [TcrSession.init(AsyncCallback)](https://tencentyun.github.io/cloudgame-android-sdk/tcrsdk/com/tencent/tcr/sdk/api/TcrSession.html#init(com.tencent.tcr.sdk.api.AsyncCallback)) callback API.
2. **The backend service reserves a concurrency**:
Your backend service calls the CAR API [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) to reserve a concurrency and proceeds to the next step after receiving the success callback.
3. **The backend service gets `ServerSession`**:
Your backend service calls the CAR API [CreateSession(ClientSession)](https://intl.cloud.tencent.com/document/product/1158/49968) to get `ServerSession` in the success callback and return it to the client.
4. **Start CAR**:
The call method to start CAR after `ServerSession` is received varies slightly for SDKs for different client types. Read the following guides as needed:
   - **JavaScript SDK**: The client calls the [TCGSDK.start(ServerSession)](https://intl.cloud.tencent.com/document/product/1158/49627#tcgsdk.start(serversession)) function to start CAR.
   - **SDK for Android**: The client calls the [TcrSession.start(ServerSession, AsyncCallback)](https://tencentyun.github.io/cloudgame-android-sdk/tcrsdk/com/tencent/tcr/sdk/api/TcrSession.html#start(java.lang.String,com.tencent.tcr.sdk.api.AsyncCallback)) function to start CAR.


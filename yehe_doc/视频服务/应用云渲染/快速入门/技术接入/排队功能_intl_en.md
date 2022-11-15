## Queue Feature
This section describes how to integrate the user queue system. We recommend you integrate the user queue system to improve the user experience when the number of users requesting your application becomes greater than the max number of concurrencies.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/ef3d594d9fe81d0f98e856cbc289491c.jpg)

### Directions
1. The client calls the [TCGSDK.init()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.init(params)) API to perform initialization. After initialization, it calls the [TCGSDK.getClientSession()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.getClientSession()) API to get `ClientSession` of the client.
2. [](id:step2)The client requests the backend to start the application based on parameters passed in such as `UserId` and `ClientSession`. Here, `UserId` is the unique user identifier and should remain unchanged during user queuing and application reconnection. The business backend needs to perform the following operations based on the current queuing status: 
	- If the queue isn't empty, add the user to the queue and return the current queue ranking information. The client regularly initiates requests after receiving the queue information and repeats **step 2** until the application is started successfully.
	- If the queue is empty or the user ranks the first, proceed to **step 3**.
3. [](id:step3)The backend calls the [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) API to apply to reserve a CAR concurrency and perform the following steps based on the returned result:
	- If there are no idle concurrencies or an error is returned, add the user to the queue, return the current queue ranking information, and go back to **step 2** to initiate a request again.
	- If a concurrency is obtained successfully, proceed to **step 4**.
4. [](id:step4)The backend calls the [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968) API to create a session and returns `ServerSession` to the business client.

5. The client calls the [TCGSDK.start()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.start(serverSession)) API to start the cloud application. After the application is connected, the SDK will trigger the `onConnectSuccess()` callback. We recommend you call the data channel creation API and APIs for other features after this callback.
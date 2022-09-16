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


## Application Heartbeat Connection
This section describes how to maintain a heartbeat connection between the client and the backend. The heartbeat can be used to detect whether the user is still connected and used to collect and manage data such as user connection duration. In this way, if the user exits due to an error, the backend can more quickly repossess the concurrency the user was occupying, and make it available to other users.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/ff17676e26edbdda33036b615fe6d55a.jpg)

### Directions
1. The client regularly sends heartbeat messages to the backend. The backend maintains the user connectivity based on the heartbeat messages.
2. The backend regularly checks whether the user is still connected. If the user heartbeat times out, the backend will call the [DestroySession()](https://intl.cloud.tencent.com/document/product/1158/49967) API to terminate the session and close the application, and the client will disconnect from the application.

## Data Channel
This document describes how to use a data channel to establish communication between the client and a cloud application.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/d30a87c7f0069f555992b253ecf190e2.jpg)

### Directions
1. [](id:step4_1)Create a UDP service for the cloud application to listen on a local UDP port (recommended port range: 10000–20000 for `localhost 127.0.0.1`) and wait to receive UDP packets.
2. The client calls the [TCGSDK.start()](https://intl.cloud.tencent.com/document/product/1158/49627#TCGSDK.start(serverSession)) API to start the cloud application. After the application is connected, the SDK will trigger the `onConnectSuccess()` callback. We recommend the client create a data channel after this callback.
3. The client calls the [TCGSDK.createCustomDataChannel()](https://intl.cloud.tencent.com/document/product/1158/49627#tcgsdk.createcustomdatachannel(.7Bdestport.2Conmessage.7D)) API to create a passthrough channel. The target port parameter in the API must be the port listened on by the cloud application in **step 1**. If the data channel fails to be created, repeat this step until it is created successfully.
4. [](id:step4_4)After the data channel is created successfully, the client can call `sendMessage()` to send a customized data packet. The UDP service of the cloud application receives the request and parses the UDP source address.
5. The cloud application sends a custom data packet to the UDP source address obtained in **step 4**. The data packet will then be returned through the created data channel. The client can process the returned packet in the `onMessage()` callback API.

## Application Reconnection
This section describes how to reconnect to an application. If a user directly closes the client but doesn't actively call the application close feature, APIs for applying for a concurrency and creating a session can be called again to reconnect to the application.
### Sequence diagram
![](https://qcloudimg.tencent-cloud.cn/raw/01990988def83c87a9e35693ebcf857e.jpg)

### Directions
1. After the client is closed, it will disconnect from the cloud application. If the backend doesn't actively call the API to close the application, the concurrency will wait for 90 seconds by default, so that there is time to reconnect.
2. After the client is opened again, it will pass in the same `UserId` to request the backend to start the application. If the `UserId` values are different, it cannot reconnect the user to the application.
3. The backend calls the [ApplyConcurrent()](https://intl.cloud.tencent.com/document/product/1158/49969) API to apply to reserve the concurrent and perform the following steps based on the concurrency’s status:
	- If the user's last connected concurrency hasn't been repossessed, the last concurrency will be returned.
	- If the user's last connected concurrency has already been repossessed, a new concurrency will be returned.
4. The backend calls the [CreateSession()](https://intl.cloud.tencent.com/document/product/1158/49968) API to create a session and returns `ServerSession` to the client to restart the application.

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
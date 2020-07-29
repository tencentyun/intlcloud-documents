## Operation Scenarios

This document describes how to use the "demo" to experience the GSE core process and get started with the game server hosting service.


## Prerequisites

You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## Directions

1. Upload a demo package
 1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Demo** on the left sidebar.
 2. Select the service region in the top-left corner and click **Quick Upload of Demo Package** to upload a demo package. After the message indicating that the package has been uploaded successfully is displayed, click **Next**.
 ![](https://main.qcloudimg.com/raw/aba9f81e1e145dd9233c962a71f9938e.png)
>?
>- The demo package provided by GSE has already integrated the gRPC framework, and the game process communicates with GSE through gRPC.
>- If you want to create on your own, please see [Creating Asset Package](https://intl.cloud.tencent.com/document/product/1055/36674).

2. Create a server fleet
Click **Quick Creation of Server Fleet**. After the message indicating that the fleet has been created successfully is displayed, click **Next**.
 ![](https://main.qcloudimg.com/raw/a951885502b0175481566008cf53fabb.png)
 >?
 > - Create a server fleet and deploy the demo package on it.
 > - A server fleet consists of a group of servers and is capable of auto scaling, so the demo package can be deployed globally with ease.
 > - If you want to create on your own, please see [Creating Server Fleet](https://intl.cloud.tencent.com/document/product/1055/36675).

3. Create a game server session and a player session
  - Click **Create Game Server Session**, and a message will be displayed indicating that a game server session has been created successfully. 
 ![](https://main.qcloudimg.com/raw/62bfaaea48a794c5971038b96e6ce42c.png)

>?
>- This operation will call the `CreateGameServerSession` TencentCloud API, so GSE will create a game server session and assign it a service process.
>- If you want to create on your own, please see the API document for `CreateGameServerSession`. 

 - Click **Create Player Session**, and a message indicating that a player session has been created successfully will be displayed.
 ![](https://main.qcloudimg.com/raw/bf467a231680025f40bfddbc07888567.png)

 >?
 >- This operation will call the `JoinGameServerSession` TencentCloud API, so GSE will create a player session and join the player in the game server session.
 >- If you want to create on your own, please see the API document for [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132).

4. Connect the client to the game server
Click **Redirect to client webpage** to access the page for connecting the client to the game server. Click **Connect**, and a message indicating that the server has been connected successfully will be displayed. 
>?
>- After creating the player session, the player (client) needs to connect to the server within 1 minute; otherwise, the session will expire.
>- This demo package is a chat service. When multiple players connect to the server, they can chat with each other.

 The above four steps simulate the entire GSE integration process. For more information, please see [Development Guide](https://intl.cloud.tencent.com/document/product/1055/36683).

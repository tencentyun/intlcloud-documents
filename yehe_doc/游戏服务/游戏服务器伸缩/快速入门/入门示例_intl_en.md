
## Overview

This document describes how to use the "Demo" to get started with GSE, a game server hosting service.

## Directions

### Step 1: uploading demo package
 1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Demo** in the left sidebar.
 2. Select the service region in the top-left corner and click **Quick Upload of Demo Package**. After the message indicating that the package has been uploaded successfully is displayed, click **Next**.
    ![](https://main.qcloudimg.com/raw/aba9f81e1e145dd9233c962a71f9938e.png)
 >?
    - The demo package provided by GSE has already integrated the gRPC framework through which the game process communicates with GSE.
    - If you want to create on your own, please see [Creating Code Packages](https://intl.cloud.tencent.com/document/product/1055/36674).

### Step 2: creating a server fleet
Click **Quick Creation of Server Fleet**, and you will see how the creation status changes, such as “Create (In progress)” and “Downloading (In progress)”. When “Created successfully” is displayed, click **Next**.
 - To create a server fleet needs a “Completed” status for all 6 steps, namely, Create (Completed), Downloading (Completed), Verifying (Completed), Generating (Completed), Activating (Completed), and Active (Completed).
 - **Status**: creating, or server fleet XXX created successfully.
![](https://main.qcloudimg.com/raw/8854d79ca8ce4f1edbb4f93529766bdb.png)
![](https://main.qcloudimg.com/raw/013f88008a3833369c8ab2ca1ae8a0a9.png)
![](https://main.qcloudimg.com/raw/d395303b0afa601cd1e7bd29713816e2.png)
 >?
   - Your demo package is deployed onto the server fleet as it is being created.
   - A server fleet consists of a group of servers capable of auto-scaling, so the demo package can be deployed globally with ease.
   - If you want to create on your own, please see [Creating Server Fleets](https://intl.cloud.tencent.com/document/product/1055/36675).

### Step 3: creating a game server session and a player session
- Click **Create Game Server Session**, and a message will be displayed indicating that a game server session has been created successfully. 
![](https://main.qcloudimg.com/raw/00e1ad7d8190f60cf021f5a1ec82d437.png)
 >?
    - This operation calls the `CreateGameServerSession` TencentCloud API so that GSE will create a game server session and assign it a service process.
    - If you want to create on your own, please see the API document [CreateGameServerSession](https://intl.cloud.tencent.com/zh/document/product/1055/37139). 
- Click **Create Player Session**, and a message indicating that a player session has been created successfully will be displayed.
![](https://main.qcloudimg.com/raw/3ac88d02e60888dafce042625927cba4.png)
>?
    - This operation calls the `JoinGameServerSession` TencentCloud API, so that GSE will create a player session and add the player to a game server session.
    - If you want to create on your own, please see the API document [JoinGameServerSession](https://intl.cloud.tencent.com/zh/document/product/1055/39130).

### Step 4: connecting client to the game server
   Click **Redirect to client webpage** to access the page for connecting the client to the game server. Click **Connect**, and a message indicating that the server has been connected successfully will be displayed. 

>?
>
>- After creating the player session, the player (client) needs to connect to the server within 1 minute; otherwise, the connection will expire.
>- This demo package is a chat service. When multiple players connect to the server, they can chat with each other.

 The above four steps simulate the entire GSE integration process. For more information, please see [Development Guide](https://intl.cloud.tencent.com/zh/document/product/1055/36683).

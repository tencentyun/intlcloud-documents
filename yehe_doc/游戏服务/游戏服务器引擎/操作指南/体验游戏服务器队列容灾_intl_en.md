## Overview
This document describes how to perform disaster recovery for a game server queue.


## Preparations 
- You have integrated the [ServerSDK code package](https://intl.cloud.tencent.com/document/product/1055/36674). You can also [use the demo package](https://intl.cloud.tencent.com/document/product/1055/36678).
- You have created server fleet 1 (in the Shanghai region).
- You have created server fleet 2 (in the US region).
![](https://main.qcloudimg.com/raw/7726bf7876142b7b1e7ed626e2cd2f46.png)
![](https://main.qcloudimg.com/raw/5881c69ab304675cf86c741364a5502b.png)


## Directions
### Creating a game server queue
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Game Server Queue** on the left sidebar.
2. Select and add the created server fleets "Shanghai - server fleet 1" and "US - server fleet 2" to the queue.
3. Access the server fleet details page and modify the delay policy to limit the delay to below 150 ms.
![](https://main.qcloudimg.com/raw/1bbaed4ecdf6946d4b8d89490a18e5fb.png)

### Requesting a server address
Place a game server session. In addition to integrating the SDK into the code to call a TencentCloud API, you can also use [TencentCloud API debugging](https://console.cloud.tencent.com/api/explorer?Product=gse) to quickly create a session.

**Input parameters**:
- The delay for player 1 is 100 ms to Shanghai and 50 ms to Silicon Valley.
- The delay for player 2 is 60 ms to Shanghai and 80 ms to Silicon Valley.
![](https://main.qcloudimg.com/raw/fa0aa1e00bab6cfa89c1cd211b1af562.png)
![](https://main.qcloudimg.com/raw/29baaa97fb0e6a3e20a2f9b53f0a5bdd.png)
![](https://main.qcloudimg.com/raw/0327f3c13ce77d07af24e6fc5a417f59.png)


Since the delay policy specifies that only servers in regions where the delay for all players is below 150 ms will be matched and since both the Silicon Valley and Shanghai regions meet this requirement, a game server session will be automatically created in "Shanghai - server fleet 1", which has a higher priority.

![](https://main.qcloudimg.com/raw/7a1a2d5bbb156d6dd99e29abd3cb8821.png)

### Automatic disaster recovery

Suppose the Shanghai region fails and its speed cannot be tested.

**Input parameters**:  
![](https://main.qcloudimg.com/raw/a143ffef65105d4a785e11803946ac3d.png)
![](https://main.qcloudimg.com/raw/e6b46c5b84adb4dea5e8da0613eb8bc2.png)
![](https://main.qcloudimg.com/raw/482798618d6366bd186a726364d7a831.png)

A game server session will be automatically created in "Silicon Valley - server fleet 2", which has a higher priority.

![](https://main.qcloudimg.com/raw/d10d4b8c38a10b8a8bfb89ca9b292406.png)


### Manual disaster recovery
If a region fails, fleets in it will be removed from the target list in the game server session queue.
![](https://main.qcloudimg.com/raw/94c558e6fa2df116135e8d0017bb19b2.png)

## Overview
This document describes how to implement nearby resource scheduling through a game server queue.
## Prerequisites 
- Create two server fleets in Shanghai and Silicon Valley regions as instructed below:
  - Complete the first three steps in the [Demo](https://intl.cloud.tencent.com/document/product/1055/37401): click **Quick Upload of Demo Package**, **Quick Creation of Server Fleet**, and **Create Game Server Session** and then click **Complete**.
- You have created server fleet 1 (Shanghai region).
![](https://main.qcloudimg.com/raw/e9240bad9dc778191158a37dba941908.png)
- You have created server fleet 2 (US region).
![](https://main.qcloudimg.com/raw/a22c7cb934124b91728523e56d42f3fc.png)

## Directions

### Creating game server queue

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Queue** on the left sidebar to enter the game server queue page.
2. Select the service region in the top-left corner and click **Create**.
3. In the game server queue creation page, enter the basic information:
  - Identifier: enter a valid identifier, which can contain letters only and is "dispatchingnearby" in this example.
  - Timeout Allocation: enter the max time that a game server session request can be retained in a multi-region deployment. It can be up to 600 seconds and is 30 seconds in this example.
4. Enter the latency policies: 
 - In the first 10s, server fleets whose latency for any players is up to 80 ms are matched and waited for first.  
 - In the subsequent 10s (i.e., in the first 20 seconds), server fleets whose latency for any players is up to 100 ms are matched and waited for first.
 - In the last 10s (= 30s - 10s - 10s) of the timeout period, server fleets whose latency for any players is up to 150 ms are matched and waited for. 
5. Select the created server fleet 1 (Shanghai region) and server fleet 2 (US region) as the target.
6. Click **OK** to complete creating the game server queue.
![](https://main.qcloudimg.com/raw/24e976209f4592336cc4cbb4255e8cbc.png)

### Starting placing game server session with queue
Call the `StartGameServerSessionPlacement` TencentCloud API in the code to place the game server session in the server fleet process. This example uses [TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=StartGameServerSessionPlacement&SignVersion=) for quick creation.

>?Input parameter description
- `Region` indicates the region, which is “ap-shanghai” (East China (Shanghai)) in this example;
- `PlacementId` indicates the unique ID of the game server session placement, which is 1 in this example;
- `GameServerSessionQueueName` indicates the game server session queue name, which is "dispatchingnearby" in this example;
- `MaximumPlayerSessionCount` indicates the maximum number of concurrent players allowed by the game server to connect to the game session, which is 2 in this example;
- `DesiredPlayerSessions.N` indicates the player game session information, where `PlayerId` is the unique player ID associated with the player session. In this example, two values of 1 and 2 are entered respectively;
- `PlayerLatencies.N` indicates the player latency, where `PlayerId` is the player ID, `RegionIdentifier` is the name of the region where the latency occurs, and `LatencyInMilliseconds` is the latency in milliseconds. In this example, four value sets are entered, i.e., [1, ap-shanghai, 100], [1, na-siliconvalley, 50], [2, ap-shanghai, 60], and [2, na-siliconvalley, 80].

![](https://main.qcloudimg.com/raw/d0ef6f4ac7bcee9f340eecd53ae690cc.png)
![](https://main.qcloudimg.com/raw/e22e0c148d52885be3ceea010c13ce19.png)
![](https://main.qcloudimg.com/raw/6d3d71aa4c6173ae78112727ac12abec.png)

#### Scheduling result evaluation of latency policy

Latency in two players' arrival at the target address: 
- The latency for player 1 is 100 ms to Shanghai and 50 ms to Silicon Valley.
- The latency for player 2 is 60 ms to Shanghai and 80 ms to Silicon Valley.

Since the latency policy specifies that in the first 10 seconds, servers in regions where the latency for any players is up to 80 ms will be matched first, the game server session will be scheduled to the Silicon Valley region.

**Test result returned after API call:**
The game server session is scheduled to server fleet 2 (US region).
![](https://main.qcloudimg.com/raw/ee9c2397d8159b1fa4a8cb4964a0a8e6.png)




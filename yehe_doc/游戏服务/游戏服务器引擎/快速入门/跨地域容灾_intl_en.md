## Operation Scenarios

This document describes how to implement cross-region disaster recovery through a game server queue.


## Prerequisites 

- Create two server fleets in Shanghai and Silicon Valley as instructed below:
  - Complete the first three steps in the [demo](https://intl.cloud.tencent.com/document/product/1055/37401): click **Quick Upload of Demo Package**, **Quick Creation of Server Fleet**, and **Create Game Server Session** and then click **Complete**.
- You have created server fleet 1 (in the Shanghai region).
![](https://main.qcloudimg.com/raw/7726bf7876142b7b1e7ed626e2cd2f46.png)
- You have created server fleet 2 (in the US region).
![](https://main.qcloudimg.com/raw/5881c69ab304675cf86c741364a5502b.png)

## Directions

### Creating game server queue

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Game Server Queue** on the left sidebar to enter the game server queue page.
2. Select the service region in the top-left corner and click **Create**.
3. Go to the game server queue creation page and enter the basic information:
   - Identifier: enter a valid identifier, which can contain letters only and is "disasterrecovery" in this example.
   - Timeout Allocation: enter the longest period for waiting for a game server session request in multiple regions, which can be up to 600 seconds and is 30 seconds in this example.
4. Enter the delay policy: 
  - In the remainder of the timeout period (30s), server fleets whose delay for all players is below 150 ms can be matched.
5. Select the created server fleet 1 (Shanghai region) and server fleet 2 (US region) as the target.
6. Click **OK** to complete creating the game server queue.
![](https://main.qcloudimg.com/raw/5499f546232f016127e201c6ce40f871.png)


### Requesting server address if no failure

Call the `StartGameServerSessionPlacement` TencentCloud API in the code to place the game server session in the server fleet process. This example uses [TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=StartGameServerSessionPlacement&SignVersion=) for quick creation.
>?Input parameter description:
>- `Region` indicates the region, which is "East China (Shanghai)" in this example;
>- `PlacementId` indicates the unique ID of the game server session placement, which is 1 in this example;
>- `GameServerSessionQueueName` indicates the game server session queue name, which is "disasterrecovery" in this example;
>- `MaximumPlayerSessionCount` indicates the maximum number of concurrent players allowed by the game server to connect to the game session, which is 2 in this example;
>- `DesiredPlayerSessions.N` indicates the player game session information, where `PlayerId` is the unique player ID associated with the player session. In this example, two values of 1 and 2 respectively are entered;
>- `PlayerLatencies.N` indicates the player delay, where `PlayerId` is the player ID, `RegionIdentifier` is the name of the region corresponding to the delay, and `LatencyInMilliseconds` is the delay in milliseconds. In this example, four values are entered, i.e., [1,ap-shanghai,100], [1,na-siliconvalley,50], [2,ap-shanghai,60], and [2,na-siliconvalley,80].

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/29baaa97fb0e6a3e20a2f9b53f0a5bdd.png)
![](https://main.qcloudimg.com/raw/0327f3c13ce77d07af24e6fc5a417f59.png)
**Scheduling result evaluation of delay policy:**
Delays in two players' arrival at the target address:

- The delay for player 1 is 100 ms to Shanghai and 50 ms to Silicon Valley.
- The delay for player 2 is 60 ms to Shanghai and 80 ms to Silicon Valley.
As the delay policy specifies that only servers whose delay for all players is below 150 ms can be matched and both the Silicon Valley and Shanghai regions meet the requirement, a game server session will be automatically created in server fleet 1 (Shanghai region) with a higher priority.
![](https://main.qcloudimg.com/raw/7a1a2d5bbb156d6dd99e29abd3cb8821.png)

### Automatic disaster recovery in case of failure

Suppose the Shanghai region fails and its speed cannot be tested.
>?Input parameter description: 
  - `PlayerLatencies.N` indicates the player delay, where `PlayerId` is the player ID, `RegionIdentifier` is the name of the region corresponding to the delay, and `LatencyInMilliseconds` is the delay in milliseconds. In this example, four values are entered, i.e., [1,ap-shanghai,0], [1,na-siliconvalley,50], [2,ap-shanghai,0], and [2,na-siliconvalley,80]. To set a condition where the speed cannot be measured, enter 0 or infinity for the delay or leave it empty. In this example, the delay to Shanghai is entered as 0.
  - Keep the rest parameters the same as the ones above.

![](https://main.qcloudimg.com/raw/bf528fd7700938e035cbe7ccd201954c.png)
![](https://main.qcloudimg.com/raw/e6b46c5b84adb4dea5e8da0613eb8bc2.png)
![](https://main.qcloudimg.com/raw/482798618d6366bd186a726364d7a831.png)


**Scheduling result evaluation of delay policy:**
Delays in two players' arrival at the target address:
- The delay for player 1 is 0 ms to Shanghai and 50 ms to Silicon Valley.
- The delay for player 2 is 0 ms to Shanghai and 80 ms to Silicon Valley.

A delay of 0 ms to the Shanghai region indicates that the delay cannot be measured due to a failure in Shanghai; therefore, a game server session will be automatically created in server fleet 2 in the US region.
![](https://main.qcloudimg.com/raw/eccba22674c685285bb94220bd9b407c.png)

### Manual disaster recovery in case of failure

If a region fails, you need to manually remove server fleets in it from the target list in the game server session queue, and GSE will schedule game server sessions to the remaining server fleets in the target list.
![](https://main.qcloudimg.com/raw/94c558e6fa2df116135e8d0017bb19b2.png)


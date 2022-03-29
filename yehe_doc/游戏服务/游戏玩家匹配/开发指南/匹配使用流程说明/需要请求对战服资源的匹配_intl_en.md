>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.

This document describes how to use GSE in combination with GPM to enhance your game development experience.

## Prerequisites

- You have [created a server fleet](https://intl.cloud.tencent.com/document/product/1055/36681) on the GSE console.
- You have [created a match](https://intl.cloud.tencent.com/document/product/1072/39203) and selected **Request GSE Resources**.

## Process Architecture
The process architecture of GSE+GPM is as follows:
![](https://main.qcloudimg.com/raw/aa2bb73826a1f8dd1319cb3a3fa8861a.png)

## Matchmaking Status
To request GSE resources for the GPM matchmaking result, your MatchTicket will have the following statuses:
>?For more information about MatchTicket, see [MatchTicket Parameters](https://intl.cloud.tencent.com/document/product/1072/39214).
>
![](https://main.qcloudimg.com/raw/6110d973c2fe926279824242d52149e0.png)

## Directions

### Step 1: initiate a matchmaking request on the client

You need a server to process matchmaking requests from your players, and call the [`StartMatching`](https://intl.cloud.tencent.com/document/product/1072/39904) API to initiate matchmaking requests to GPM. A successful call of the [`StartMatching`](https://intl.cloud.tencent.com/document/product/1072/39904) API generates a unique MatchTicket. You need to track the MatchTicket status to complete your matchmaking process.

You can call the [`CancelMatching`](https://intl.cloud.tencent.com/document/product/1072/39908) API to cancel the matching MatchTicket.

### Step 2: track the matchmaking status through event notifications

After a matchmaking request is initiated, you can configure a notification address to receive GPM event notifications. Meanwhile, you can set a timer to periodically process event notifications. For more information about event notification, see [Event Notifications](https://intl.cloud.tencent.com/document/product/1072/39219).

### Step 3: process completed MatchTicket

- For a completed MatchTicket, GPM has already started a game server session on the game server queue, and filled in the relevant MatchTicket fields with game connections.
- You need to parse MatchTicket based on the [protocol](https://intl.cloud.tencent.com/document/product/1072/39219) and obtain game connections as well as player ID and player session ID in the same battle.
- Players can access the active GSE game server session after receiving the game connections and player session ID. For more information about how to connect to a game server session, see [Connecting Client to gRPC Server of GSE](https://intl.cloud.tencent.com/document/product/1055/37408).
- For **cancelled/timeout/failed** ticket, you can notify players according to the actual business logic, or initiate a matchmaking request again for players.


### (Recommended) Step 4: use the DescribeMatchingProgress API to complement event notifications
If you failed to configure a notification address or receive event notifications, you can call the [`DescribeMatchingProgress`](https://intl.cloud.tencent.com/document/product/1072/39907) API to track the MatchTicket status. For more information about the statuses, see [MatchTicket Status](https://intl.cloud.tencent.com/document/product/1072/39214).


## FAQs

### 1. How does the region latency of players affect GPM and GSE?

- **For GPM**
  - If there is no latency rule in the GPM rule script, the region latency of players will not be used.
  - If there is a latency rule in the GPM rule script, the region latency of all players matched to a battle should be satisfied in at least one region.
  

For more information about region latency in GPM, see [Latency Rule](https://intl.cloud.tencent.com/document/product/1072/39870).

- **For GSE**
  - If the region latency is not passed in when a matchmaking request is initiated, GSE will choose a fleet to place the game server session according to fleet priority in the queue.
  - If the region latency is passed in when a matchmaking request is initiated, GSE will use the region latency based on whether the queue is configured a latency policy.
    - No latency policy: GSE will place the game server session in the common region according to fleet priority.
    - Latency policy configured: GSE will place the game server session in the common region according to latency policy. If there are multiple eligible regions, GSE will choose the region according to fleet priority.

For more information about region latency in GSE, see [Nearby Resource Scheduling](https://intl.cloud.tencent.com/document/product/1055/37404).


### 2. What is the difference between timeouts in GPM and GSE?

- **GPM timeout**
![](https://main.qcloudimg.com/raw/523f3f40471f8888f2dc2c6eaac9c6f5.png)
This timeout is the longest period during which GPM will search for a MatchTicket, and the MatchTicket is in `SEARCHING` status. If no other matched players are found during the period, the `MatchTicket` status will change to `TimedOut`.
- **GSE timeout**
![](https://main.qcloudimg.com/raw/dc9d48972e8de15d2bf1f57be02728ad.png)
This timeout is the longest period for retaining a game session request during which GSE will search for eligible fleet in the queue after a placement request is received. If no matched fleet is found during the period, the status of all `MatchTickets` involved in this placement change to `Failed`.

>? The time consumed for a matchmaking service mainly includes the GPM searching and GSE placing.


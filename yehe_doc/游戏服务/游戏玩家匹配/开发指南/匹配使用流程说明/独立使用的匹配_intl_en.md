>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.

This document describes how to use GPM service alone.

## Prerequisites
You have [created a match](https://intl.cloud.tencent.com/document/product/1072/39203) without selecting **Request GSE Resources**.

## Process Architecture
The GPM service can be independently used as follows:
![](https://main.qcloudimg.com/raw/575fe64bddcdf7155c4e7c5685304d6f.png)

## Matchmaking Status

The MatchTicket statuses will be as follows when you use the GPM service alone.
>? For more information about MatchTicket, please see [MatchTicket Parameters](https://intl.cloud.tencent.com/document/product/1072/39214).
>
![](https://main.qcloudimg.com/raw/ef69b3a6f56174deae5c6bdead0ec644.png)


## Directions

### Step 1: initiate a matchmaking request on the client

You need a server to process matchmaking requests from your players, and call the [`StartMatching`](https://intl.cloud.tencent.com/document/product/1072/39904) API to initiate matchmaking requests to GPM. A successful call of the [StartMatching](https://intl.cloud.tencent.com/document/product/1072/39904) API generates a unique MatchTicket. You need to track the MatchTicket status to complete your matchmaking process.

You can call the [`CancelMatching`](https://intl.cloud.tencent.com/document/product/1072/39908) API to cancel the matching MatchTicket.

### Step 2: track the matchmaking status through event notifications

After a matchmaking request is initiated, you can configure a notification address to receive GPM event notifications. Meanwhile, you can set a timer to periodically process event notifications. For more information about event notification, see [Event Notifications](https://intl.cloud.tencent.com/document/product/1072/39219).

### Step 3: process completed MatchTicket

- After the potential battle ticket is found, you need to parse MatchTicket based on the [protocol](https://intl.cloud.tencent.com/document/product/1072/39219) and obtain the player IDs matched to the same battle.
- For eligible battle tickets, you need a server to process matchmaking requests from players and connect these players to the same battle. Then, you need to process the player connection and battle logic in GPM.
- For **cancelled/timeout/failed** ticket, you can notify players according to the actual business logic, or initiate a matchmaking request again for players.


### (Optional) Step 4: use the DescribeMatchingProgress API to complement event notifications

If you failed to configure a notification address or receive event notifications, you can call the [`DescribeMatchingProgress`](https://intl.cloud.tencent.com/document/product/1072/39907) API to track the MatchTicket status. For more information about the statuses, see [MatchTicket Status](https://intl.cloud.tencent.com/document/product/1072/39214).


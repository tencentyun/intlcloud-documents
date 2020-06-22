## Overview
This document describes how to perform disaster recovery for a game server queue.


## Preparations 
- You have integrated the [ServerSDK code package](https://intl.cloud.tencent.com/document/product/1055/36674). You can also [use the demo package](https://intl.cloud.tencent.com/document/product/1055/36678).
- You have created server fleet 1 (in the Shanghai region).
- You have created server fleet 2 (in the US region).



## Directions
### Creating a game server queue
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Game Server Queue** on the left sidebar.
2. Select and add the created server fleets "Shanghai - server fleet 1" and "US - server fleet 2" to the queue.
3. Access the server fleet details page and modify the delay policy to limit the delay to below 150 ms.


### Requesting a server address
Place a game server session. In addition to integrating the SDK into the code to call a TencentCloud API, you can also use [TencentCloud API debugging](https://console.cloud.tencent.com/api/explorer?Product=gse) to quickly create a session.

**Input parameters**:
- The delay for player 1 is 100 ms to Shanghai and 50 ms to Silicon Valley.
- The delay for player 2 is 60 ms to Shanghai and 80 ms to Silicon Valley.



Since the delay policy specifies that only servers in regions where the delay for all players is below 150 ms will be matched and since both the Silicon Valley and Shanghai regions meet this requirement, a game server session will be automatically created in "Shanghai - server fleet 1", which has a higher priority.

### Automatic disaster recovery

Suppose the Shanghai region fails and its speed cannot be tested.

**Input parameters**:  


A game server session will be automatically created in "Silicon Valley - server fleet 2", which has a higher priority.

### Manual disaster recovery
If a region fails, fleets in it will be removed from the target list in the game server session queue.

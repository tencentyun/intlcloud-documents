## Overview

This document describes how to perform auto scaling through a server fleet.



## Prerequisites
You have completed the steps in the [Demo](https://intl.cloud.tencent.com/document/product/1055/37401).

## Directions

### Modifying the scaling configuration and the number of processes 

1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Fleet** on the left sidebar.
2. Click the ID of the server fleet created in the "Demo" to enter the fleet details page. Click the **Expand/Reduce** tab to view scaling details.
![](https://main.qcloudimg.com/raw/36b0bb5d3fd052bb79d87247555e637e.png)
3. Click **Modify** in the top-right corner to modify the scaling configuration as follows:
 1. Select "Automatic adjustment" as the adjustment mode.
 2. Set "Instance Range" to 0–3 so that there will be room for expansion.
 3. Set the game server session buffer to 30%, i.e., when the number of game battles (sessions) loaded on the server exceeds 70% of the limit, expansion will be performed. 
 4. After making the modifications, click **OK**.
![](https://main.qcloudimg.com/raw/e4805f7c77db319c80a46fade73b4170.png)
 >? 
 >-  Game server session buffer = number of available game server sessions / maximum number of game server sessions
  = (maximum number of game server sessions - number of active game server sessions) / maximum number of game server sessions.
 >- If the game server session buffer is configured as 30%, expansion will be performed when the available game server sessions are below 30%; otherwise, reduction will be performed.

### Creating game server session and observing expansion result
1. In the console, click **Demo** on the left sidebar, complete the first three steps in the [Demo](https://intl.cloud.tencent.com/document/product/1055/37401), and click **Create Game Server Session** for seven times to create eight game server sessions and trigger expansion.
![](https://main.qcloudimg.com/raw/9c3a7488abacb89bf8c31a254f294220.png)

>?
>- In GSE Console > Demo, one server can sustain up to 10 game server sessions by default. Therefore, when the server sustains 7 game server sessions, the game server session buffer will be number of available game server sessions / maximum number of game server sessions = (maximum number of game server sessions - number of active game server sessions) / maximum number of game server sessions = (10 - 7) / 10 = 30%.
>- Therefore, you need to create eight game server sessions at least to trigger expansion.

2. Click **[Fleet](https://console.cloud.tencent.com/gse/fleet)** on the left sidebar, select the ID of the created server fleet to enter the fleet details page, and click the **Instance List** tab to observe. After two minutes, you will see that the number of instances is increased to two.
![](https://main.qcloudimg.com/raw/120fadd9401cdfb751bf6dcc469b2344.png)
>?After the creation, **do not** click **Complete** for next trial. Instead, you still need the above configuration for reduction.

### Ending game server session and observing reduction result

1. In the console, click **Demo** on the left sidebar and proceed with the subsequent steps after the above expansion. After selecting each game server session, click **Create Player Session** once to create a player session.
![](https://main.qcloudimg.com/raw/2bc7069636a21972a9ca18ebb6264b92.png)
2. Click **Redirect to client webpage** to enter the client page. Click **Connect** to successfully connect to the server. Click **End Game Session** to end the game server session. Repeat steps 1 and 2 once to end 2 game server sessions and trigger reduction.

>? 
>- Game server session buffer = number of available game server sessions / maximum number of game server sessions = (maximum number of game server sessions - number of active game server sessions) / maximum number of game server sessions = (20 - 6) / 20 = 70%.
>- As there are only 6 active game server sessions left, which is above 30%, so reduction will be triggered.
>- On the current version, after you close the client webpage, previously created player sessions will not be able to reconnect to the client, and only new player sessions can be connected again to close the game server session.

3. Click **[Server Fleet](https://console.cloud.tencent.com/gse/fleet)** on the left sidebar, select the ID of the created server fleet to enter the fleet details page, and click the **Instance List** tab. Observe the instance quantity. After 2 minutes, you will see that the number of servers is decreased to 1.
![](https://main.qcloudimg.com/raw/08b123eb22e7bf84f6ebf812bc23e924.png)





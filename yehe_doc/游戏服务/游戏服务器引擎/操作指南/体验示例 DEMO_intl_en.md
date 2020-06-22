## Overview
This document describes how to use the "quick trial" tool to experience the GSE core process and get started with the game server hosting service.


## Prerequisites
You have completed the [GSE Application Form](https://intl.cloud.tencent.com/apply/p/k0b6pvbhs6) and your application has been approved.

## The Overall Process
![](https://main.qcloudimg.com/raw/497d075c6e3b78d11fba77cbccb95cd6.jpg)

You can call GSE by the following the four steps below:
1. Integrate ServerSDK.
2. Publish the program integrated with ServerSDK.
3. Call a TencentCloud API (to create a game server session and a player session) and request the service address.
4. Access the service.

## Directions
### Using quick trial



1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Quick Trial** > **Demo** on the left sidebar.
2. Select the service region in the top-left corner and click **Quick Upload of Demo Package**. After the message indicating that the package has been uploaded successfully is displayed, click **Next**.
![](https://main.qcloudimg.com/raw/fcf724549b9d7d9467609d84d41846a7.png)
>This step integrates ServerSDK into your code. Please upload the code and the dependencies. GSE provides a demo package and allows you to quickly upload it.
3. Click **Quick Creation of Server Fleet**. After "Created successfully" is displayed, click **Next**.
![](https://main.qcloudimg.com/raw/809653901b3c464fe9495f7badd35a4a.png)
4. Click **Create Game Server Session**, and a message will be displayed indicating that a game server session has been created successfully.
![](https://main.qcloudimg.com/raw/7f8419e0c0d87f3748aea206e501cd27.png)
>This step is performed by calling a TencentCloud API. The Console page is used for quick creation.
5. Click **Create Player Session**, and a message indicating that a player session has been created successfully will be displayed. Click **Create Player Session** to open a client webpage.
![](https://main.qcloudimg.com/raw/16697108484f9a0fe516d3c7f2fc9062.png)
6. Click **Redirect to client webpage** to access the page for connecting the client to the game server. Click **Connect**, and a message indicating that the server has been connected successfully will be displayed.
>This step connects the game service process through the IP and port returned by the TencentCloud API called in the last step. This step simulates the whole connection process. 




### Trying out auto scaling

#### Modifying the scaling configuration
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse) and click **Server Fleet** on the left sidebar.
2. Select the ID of the created server fleet to access the fleet details page and select **Expand/Reduce**.
![](https://main.qcloudimg.com/raw/14763840a0a668fefb00561635117d8a.png)
3. Click **Modify** in the top-right corner to modify the scaling configuration items as follows:
 - Set the game server session buffer to 50%, i.e., when the number of game battles (sessions) loaded on the server exceeds 50% of the limit, expansion will be performed.
 - Set "Instance Range" to 0–3 so that there will be room for expansion.
 ![](https://main.qcloudimg.com/raw/c536b489618bdb31ea365f3f878d970c.png)
4. After making the modifications, click **OK**.


#### Creating multiple game server sessions to trigger expansion

>
>- In the demo, one server is configured to sustain up to 10 game server sessions by default. When 5 game server sessions are loaded, the buffer utilization will be 50%.
>- Expansion will be required when there are more than 5 game server sessions. Therefore, you need to create 6 game server sessions to trigger expansion.

1. Select **Quick Trial** > **Deploy Demo Package** and click **Create Game Server Session** 5 consecutive times to create 6 game server sessions.
![](https://main.qcloudimg.com/raw/08657b4e432b7b7b9c1c3e76abe6d8b3.png)
2. Click **[Server Fleet](https://console.cloud.tencent.com/gse/fleet)** on the left sidebar, select the ID of the created server fleet to access the fleet details page, and select **Instance List**. Observe the instance quantity. After 2 minutes, you will see the number of servers increase to 2.
![](https://main.qcloudimg.com/raw/fff0c7e124e3e234c6cb5b33e3629e51.png)


#### Ending game server sessions to trigger reduction
1. Select **Quick Trial** > **Deploy Demo Package** and create a player session for each game server session. Access the client page and click **End Game Session** to end a session. Repeat this operation 5 consecutive times to end 5 game server sessions.
2. Click **[Server Fleet](https://console.cloud.tencent.com/gse/fleet)** on the left sidebar, select the ID of the created server fleet to access the fleet details page, and select **Instance List**. Observe the instance quantity. After 2 minutes, you will see the number of servers decrease to 1.
![](https://main.qcloudimg.com/raw/926551c0ddd00088ed5be6f556ceb485.png)

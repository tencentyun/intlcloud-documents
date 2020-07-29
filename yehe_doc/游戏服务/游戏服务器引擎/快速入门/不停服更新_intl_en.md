## Operation Scenarios

This document describes how to implement zero downtime update through an alias.

## Prerequisites

- Create two server fleets in Shanghai and Silicon Valley as instructed below:
  - Complete the first three steps in the [demo](https://intl.cloud.tencent.com/document/product/1055/37401): click **Quick Upload of Demo Package**, **Quick Creation of Server Fleet**, and **Create Game Server Session** and then click **Complete**.
- You have created server fleet 1 (in the Shanghai region).
![](https://main.qcloudimg.com/raw/57e329af56b34ad437d8f1a28e6fde76.png)
- You have created server fleet 2 (in the US region).
![](https://main.qcloudimg.com/raw/a09178360cc2d92637c0c166135355be.png)

## Directions
### Creating alias 
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Alias** on the left sidebar.
2. Select the service region in the top-left corner and click **Create**.
3. Go to the alias creation page, enter the name and description, select the alias type and associated server fleet in the corresponding drop-down list, and click **OK**.
 - Name: enter the name of the alias for easy identification in the directory, which is "zero downtime update test" in this example.
 - Type: select common alias or termination alias, which is "common alias" in this example.
    - Common alias: it points to a fleet, under which the system automatically finds servers and assigns them to clients. If you select common alias, you need to associate an available server fleet.
    - Termination alias: it doesn't point to a fleet. You can describe the reason why the alias cannot be used in the termination information, which will be sent to clients.
 - Associate Server Fleet: after selecting common alias, select "server fleet 1".
 - Description: enter a short description of the alias for easy identification, which is "test" in this example.
4. After completing the settings, click **OK** to create the alias.
![](https://main.qcloudimg.com/raw/ef04ad328a96e3b26031bf79577f335d.png)


### Creating game server session

Call the TencentCloud API in the code. This example uses [TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=CreateGameServerSession&SignVersion=) for quick creation.

>?Input parameter description:
>- `Region` indicates the region, which is "East China (Shanghai)" in this example;
>- `MaximumPlayerSessionCount` indicates the maximum number of players, which is 10 in this example;
>- `AliasId` indicates the alias ID, which is the ID of the just created alias in this example.

![](https://main.qcloudimg.com/raw/676fc6ade84a0e5284f474af2cd92d3d.png)

If a game server session is successfully created through [TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=CreateGameServerSession&SignVersion=), you can see that it is generated in server fleet 1.
![](https://main.qcloudimg.com/raw/5e0f14322ec92296e63947dfa88482de.png)


### Modifying alias configuration

1. In the console, click **Alias** on the left sidebar to enter the alias list page.
2. Select the just created alias and click **Modify** to enter the alias editing page, modify the alias configuration, and set "Associate Server Fleet" to "Server fleet 2".
![](https://main.qcloudimg.com/raw/dd5a258098c49aaa00cb7d7048507bd1.png)

### Creating another game server session

>?Create another game server session with the same alias.

Create another game server session through [TencentCloud API Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=CreateGameServerSession&SignVersion=), and you can see that a game server session is generated in server fleet 2. As can be seen, the new session is assigned to server fleet 2.
![](https://main.qcloudimg.com/raw/14a5feb8995eb22c4d1f3c26b6c2fcf3.png)

## Notes on Zero Downtime Update
When the version needs to be updated, you can create a new server fleet and point the alias to it.
- Automatic reduction will be performed on the original server fleet as the game server sessions decrease.
- Automatic expansion will be performed on the new server fleet as the game server sessions increase, thus implementing zero downtime update.


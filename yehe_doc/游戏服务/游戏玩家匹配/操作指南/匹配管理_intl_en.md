>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31, , 2022.
This document describes how to manage a match through the console.

## Prerequisites

- You have [created a rule](https://intl.cloud.tencent.com/document/product/1072/39202).
- If you need to create a match that needs to **request GSE resources**, you need to [create a game server queue](https://intl.cloud.tencent.com/document/product/1055/36681).

## Directions

### Creating a match

1. Log in to the [GPM console](https://console.cloud.tencent.com/gpm) and click **Matches** on the left sidebar.
2. On the **Matches** page, click **Create**.
   ![](https://main.qcloudimg.com/raw/17a5bded65a06d5d8bdbd8e7df47461d.jpg)
3. Set the related information, such as match name, description, the associated rule.
   GPM classifies matchmakings into two types based on whether to automatically request resources from your game server based on matchmaking results to start battles. The creation parameters of the two matchmaking types are as follows:

<span id="test2"></span>

 - #### Matchmaking without automatically requesting GSE resources

   In this type, GPM will use the MatchTicket for matching, that is, searching for the eligible MatchTicket according to the configured rules to complete matchmaking. User needs to handle the matchmaking results and the battle connection after the matchmaking is completed. For detailed matchmaking process of this type, please see [Independent Match](https://intl.cloud.tencent.com/document/product/1072/39218).

   ![](https://main.qcloudimg.com/raw/3d82e1b0d9634c019d1282abf46f8720.jpg)

   - Name (required): enter a match name. It can contain up to 128 bytes.
   - Description (optional): the description of the match. It can contain up to 1024 bytes.
   - Associate Rule (required): the rule associated with the match.
   - Timeout (required): the time that GPM performs a matching search for a MatchTicket. Value range: 1 - 600 seconds
   - Notification Address (optional): only HTTP and HTTPS protocols are supported. When the matchmaking is completed based on the currently MatchTicket or the matchmaking status changes, GPM will push the event notification to the address you configured. We strongly recommend that you use GPM's event notification feature and configure the receiving notification address to obtain the matchmaking results.
   - Request GSE Resources (required): select **No**.



<span id="test2"></span>

- #### Request resources from the game server to start battles

  GMP can automatically request [GSE](https://intl.cloud.tencent.com/document/product/1055) resources based on matchmaking results to start a game server session. Players who are successfully matched can connect to the resources allocated by GSE for game battles. To create this type of matchmaking, you need to create a queue in GSE first. For details, please see [Creating Game Server Queues](https://intl.cloud.tencent.com/document/product/1055/36681). For details on this type of matchmaking process, please see [Battle Match](https://intl.cloud.tencent.com/document/product/1072/39217) and enter the following information.
  ![](https://main.qcloudimg.com/raw/a692ca9c613e9bcc836ed41ae5af10c8.jpg)

   - Request GSE Resources (required): select **Request GSE Resources**.
   - Game Server Queue Region (required): select the region of the GSE server queue.
   - Game Server Queue (required): the GSE server queue name.
   - Custom Push Data (optional): it can contain up to 1024 bytes. This parameter will be passed through to GSE and will be used to create a GSE game server session.
   - Game Server Session Data (Optional): it can contain up to 1024 bytes. This parameter will be passed through to GSE and will be used to create a GSE game server session.
   - Game Attributes (Optional): this parameter will be passed through to GSE and will be used to create a GSE game server session.
     - Key: attribute name. Up to 32 ASCII characters are allowed.
     - Value: attribute value. Up to 96 ASCII characters are allowed.

4. Click **OK**. After the matchmaking is created, the corresponding MatchCode will be generated on the **Matches** page.
   ![](https://main.qcloudimg.com/raw/2f752494bf04ef42d3854683979e94e4.jpg)

### Viewing a match

On the **Matches** page, click a MatchCode in the list to view its details.

>?If the current match needs to request GSE resources, you can click the game server queue name and go to the [GSE console](https://console.cloud.tencent.com/gpm) to view the game server queue associated with the current match.
>
![](https://main.qcloudimg.com/raw/a03b3651923d91c992281546d551fed9.jpg)

### Editing a match

On the **Matches** page, select a match in the list and click **Edit** in the **Operation** column. After the match is edited, the new configuration will take effect immediately.
![](https://main.qcloudimg.com/raw/aea14ba5dbeaf6ebd7a9218a838ab670.jpg)

### Deleting a match

On the **Matches** page, select a match to delete in the list and click **Delete** in the **Operation** column.

>!After the match is deleted, its MatchCode configuration will be invalidated, its matching configuration will be terminated, and the log topic and log data corresponding to the current MatchCode will be deleted.
>
![](https://main.qcloudimg.com/raw/7089849258c16318dbc00806c257a6f9.jpg)




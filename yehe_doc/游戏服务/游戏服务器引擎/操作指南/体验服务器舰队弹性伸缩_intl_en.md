## Overview
This document describes how to perform auto scaling for a server fleet.



## Preparations 
- You have integrated the [ServerSDK code package](https://intl.cloud.tencent.com/document/product/1055/36674). You can also [use the demo package](https://intl.cloud.tencent.com/document/product/1055/36678).
- You have [created a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675).



## Directions
### Modifying the scaling configuration and the number of processes 
1. Log in to the [GSE Console](https://console.cloud.tencent.com/gse/asset) and click **Server Fleet** on the left sidebar.
2. Click the ID of the created server fleet to access the fleet details page.
3. Click **Expand/Reduce** to access the scaling details page and click **Modify** in the top-right corner to modify the scaling configuration items:
 - Set the game server session buffer to 50%, i.e., when the number of game battles (sessions) loaded on the server exceeds 50% of the limit, expansion will be performed.
 - Set "Instance Range" to 0–3 so that there will be room for expansion.  
 ![](https://main.qcloudimg.com/raw/8c5756b270c965498e19a5954ce53905.png)  

### Creating a game server session and observing the expansion result
In addition to integrating the SDK into the code to call a TencentCloud API, you can also use [TencentCloud API debugging](https://console.cloud.tencent.com/api/explorer?Product=gse) to quickly create a session.
 ![](https://main.qcloudimg.com/raw/7a51ee63925890bd0ff336b0d684214b.png)  
 
After the game server session is successfully created through TencentCloud API debugging, you will see that it is generated in the server fleet.
 ![](https://main.qcloudimg.com/raw/9eaf67be7b686426f0d026d5afb7aa69.png)


In this step, one process is configured for one CVM instance by default. Therefore, after a game server session is created, the session utilization will be 100%. As the game server session buffer was set to 50% in the previous step, the number of instances will be automatically increased to 2.  



### Ending a game server session and observing the reduction result
After ending a game server session, the number of instances will be automatically decreased to 1.









## The Overall Process
![](https://main.qcloudimg.com/raw/b629cd5edf3be72e21678aa9afd1a500.jpg)


## Integration Steps

### 1. Complete the integration on the server 
The server program needs to integrate with ServerSDK. For detailed directions, please see [ServerSDK Integration Process](https://intl.cloud.tencent.com/document/product/1055/36687).


### 2. Publish the server program

#### Upload the program package and the dependencies 
Compress the server program integrated with ServerSDK and the dependent package into a ZIP package and publish it as an asset package. For detailed directions, please see [Creating an Asset Package](https://intl.cloud.tencent.com/document/product/1055/36674).


#### Create a server fleet 
Publish the uploaded ZIP package to the server fleet and configure information such as the startup process and the scaling parameters of the program. For detailed directions, please see [Creating a Server Fleet](https://intl.cloud.tencent.com/document/product/1055/36675).   


### 3. Call TencentCloud APIs

#### Create a game server session 
Call the `CreateGameServerSession` TencentCloud API to create a game server session. This operation can be understood as creating a server or assigning a service process. 


#### Create a game player session
Call the `JoinGameServerSession` TencentCloud API to reserve a place in a game server session (specified by `GameServerSession`) for a player, i.e., allowing the player to access the server or process. 



### 4. Access the server
The client can connect to the target server through the `IP` and `PORT` returned in step 3.



## Workflow
![](https://main.qcloudimg.com/raw/e1aaa90a6e11e422c187dfdeb5bc8adf.png)

Tencent Cloud Game Server Engine (GSE) provides dedicated game server hosting services for the deployment and scaling of stateful games. It supports service discovery, flexible server scaling, and optimal resource scheduling. GSE helps developers quickly build a stable and low-latency deployment environment for multiplayer games while reducing OPS costs. It can be used to deploy and run Unreal and Unity game engines, as well as server frameworks written in C#, C++ or any language that supports gRPC. It is ideal for stateful games that need to remember data such as battle servers and push notifications in FPS, MOBA, turn-based games, MMORPG, chess and card games, and more.



## Product Architecture 
GSE provides a runtime environment for game code packages where you can perform service discovery, scaling, cross-region deployment, and nearby scheduling. You can integrate the GSE ServerSDK into your server framework so that clients can request access to game servers through APIs and GSE will return the optimal game server for client access.

![](https://main.qcloudimg.com/raw/363390d57a27cac0a9b8adc3d4935a2f.png)


## Features 

### Program deployment and update 

#### Program deployment
You can upload code packages and dependencies through GSE, which will deploy your code to the server fleet and launch it according to the configuration.

#### Zero downtime update
Generally, servers need to be suspended when games are updated, but GSE implements updates with zero downtime by providing an alias mechanism.

#### A/B Test
You can easily conduct or end an A/B test with GSE.



### Server instance management 

### Auto scaling 
- Auto scaling is performed once every day: games have peak and off-peak hours. Surges generally happen at noon and in the evenings, and demand falls after midnight. With GSE, you can set a selected instance type and a scaling scope, and GSE will auto-scale game servers according to player traffic within the specified scope throughout the day. 
- Stateful reduction: GSE will not remove instances with running processes. When the server load drops and reduction is triggered, GSE will inform the game processes that the server is being removed and prevent new game server sessions from being assigned to the server. However, it will not forcibly terminate the instance, so clients cab still be connected. The instance will be removed only after the game processes initiate an end command.


#### Cross-region deployment
GSE supports cross-region deployment, and server fleets built in multiple regions make up a queue. When the queue is requested, the system will automatically select a server fleet in a region for player access. You can also manually adjust the fleet priority. When a region fails, the service will be quickly switched to another region.

#### Global release 
GSE is available in regions such as Shanghai and North America and will soon be available in more regions.


### Process management 
#### Process launch  
GSE launches a process based on the launch path, launch parameters, and the allowed concurrent processes you specify.

#### Process preparation  
After a process is launched, an API will be called to inform GSE that the process is ready to accept access requests.

#### Process health check  
GSE regularly performs health checks on processes. If a process is found to be unhealthy, it will be blocked and will not be assigned to any caller.

#### Process end  
- If GSE needs to reduce its capacity or if health check fails, it will ask related processes to end. The processes can choose whether to end. If they do not immediately end, GSE will handle them based on the protection policy configured on the console.
- Processes can proactively call an API to inform GSE that they have ended.

### Game server session management
GSE manages and assigns game server sessions. From a service perspective, one game server session represents one gaming round (a battle) or a single service. From a backend program perspective, one game server session corresponds to one process, which will be launched by GSE in advance as configured. Generally, one process matches one session. When a client requests a game server session through TencentCloud API, GSE will assign this session to an idle process.

#### When the game server session starts    
When a caller requests a game server session, GSE will assign an idle and healthy process to start the session.

#### When the game server session ends  
When there are no players on a game server session or the session is unhealthy, the session will end itself or be ended. Logs will be saved before the session ends to facilitate troubleshooting.

#### Nearby assignment of game server session  
GSE can select the nearest region to a player based on the network latency.

#### Server scaling based on the ratio of available game server sessions  
You can configure a game server session buffer as an auto scaling condition for a game server fleet. A game server session buffer is the proportion of available game server sessions.


### Monitoring and logging 
The system provides CVM instance monitoring, game server session monitoring, and operation logs.


### Associated feature

For information on the game player matchmaking feature, see [Game Player Matchmaking (GPM)](https://intl.cloud.tencent.com/document/product/1072/38344). GPM provides flexible and powerful matchmaking logic algorithms. You can customize matchmaking rules, and the matched game battles will be automatically put in the GSE game server queue.

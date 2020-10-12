GPM is suitable for a variety of use cases. Here we list some examples.

### Use Case 1: Player Matchmaking

GPM can be used independently to generate player matches via custom matchmaking rules. Generated matchmaking results will be delivered to your server address. 
![](https://main.qcloudimg.com/raw/1798f70b2cc870b58f0d28abd5e8ba97.png)

### Use Case 2: Hosted Game Solutions

GPM can be used together with Tencent Cloud Game Server Engine (GSE) to form a streamlined gaming solution, where matchmaking results can be used to request resources from the game servers hosted with GSE to automatically start new game sessions for matched players. 
![](https://main.qcloudimg.com/raw/9cc184add5d43b899d2f53cb105d725f.png)

### Use Case 3: Matching Teams

GPM supports multiple matchmaking configurations within the same game. Developers can create sequential matchmaking rules to build teams and match battles. Players are first slotted into teams and then the teams are matched against each other.  
![](https://main.qcloudimg.com/raw/f9a83daee21184e72f7b57936f9d1b04.png)

### Use Case 4: Match Backfill

GPM offers a match backfill feature for existing game sessions. It can be difficult to fill all player slots for large matches. GPM supports starting a game session once the minimal number of players are matched to reduce wait time. GPM will then initiate match backfill requests for the empty player slots to continue searching for potential matches. This feature can also be used when players drop out of a session. 
![](https://main.qcloudimg.com/raw/7473734517ee61fb3d215730c41f459d.png)

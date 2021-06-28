## GSE Local

GSE Local is a command line tool that can independently launch the game server hosting service GSE. This tool also provides runtime logs including the server initialization, health check, and API calls and responses.

GSE Local is limited to launch GSE hosting services and test your game integration on a local device, which will shorten the debugging time and improve efficiency at the iterative development of games. Otherwise, you have to upload each new game package to GSE and configure the server fleet to host games.

With GSE Local, you can test that:
* Your game server correctly integrates the GSE server development kit, properly communicates with GSE service, and is able to launch new game sessions, accept new players and report the running status.
* Your game client correctly integrates the GSE-related TencentCloud APIs to retrieve existing game sessions, launch new game sessions, and allow players to join and connect to the game session.




## Setting Up GSE Local


GSE Local can run on Windows, Linux and Mac in any GSE-supported languages. You can download the installation package according to the operating system:
- [GSE Local for Windows](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-windows-amd64.exe)
- [GSE Local for Linux](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-linux-amd64)
- [GSE Local for Mac](https://gselocal-1301007756.cos.ap-nanjing.myqcloud.com/gse-local/gselocal-master-darwin-amd64)


>?The following sample code is applicable to Linux and MacOS. For Windows, we recommend to use the gitbash command line tool to run `curl` command.
>

<span id="test"></span>
## Testing Game Server

If you only need to test your game server, directly use `curl` to simulate the game client calls to GSE Local and verify that your game server can complete the following operations as expected:
1. During launch, the game server will call the `ProcessReady` API to inform GSE that the server is ready to host a game server session.
2. During runtime, the game server will use the `onHealthCheck` callback to send its running status to GSE every minute.
3. The game server will respond to requests and trigger the `onStartGameServerSession` callback (call the `activateGameServerSession` API in this process) to launch a new game session.

### Step 1: launch GSE Local

Open the command prompt window, navigate to the directory of `gselocal_windows`, `gselocal_linux` or `gselocal_mac`, and run the program. This document uses the Mac program `./gselocal_mac` as an example. After the program is launched, it will automatically connect to GSE Local.
Enter the following command in a terminal window:
```
./gselocal_mac
```
If the following information appears in the command prompt window, the launch is successful:
```
{"level":"info","ts":"2020-10-20T09:16:09.364+0800","msg":"start grpc v3 server success"}
```



### Step 2: launch the game server

Launch the game process in a programming tool or command line tool. The game process then will call the `ProcessReady` API to prepare for hosting a session and print the following logs:
```
Getting process ready, LogPath: System.String[], ClientPort: 3237, GrpcPort: 6224
Process ready succeed, resp: { }
Server Start On Locolhost:6224
```
After receiving the ProcessReady request, GSE Local will also print logs and start the health check:
```
{"level":"info","ts":"2020-10-20T09:27:03.172+0800","msg":"ProcessReady Info is","pid":"41688","requestId":"3b38495b38bc4ef8a59ae8****a8256d","info":"clientPort:3237 grpcPort:6224 "}
{"level":"info","ts":"2020-10-20T09:27:03.172+0800","msg":"set runner success","pid":"41688","processUUID":"527bf89b-d128-4b5d-bfea-****3d22ede7"}
{"level":"info","ts":"2020-10-20T09:28:03.276+0800","msg":"onHealthCheck received","pid":"41688","health":true}
{"level":"info","ts":"2020-10-20T09:29:03.256+0800","msg":"onHealthCheck received","pid":"41688","health":true}
{"level":"info","ts":"2020-10-20T09:30:03.261+0800","msg":"onHealthCheck received","pid":"41688","health":true}
```




### Step 3: use curl to create a game server session and a player session

Use `curl` to simulate the client calls. For specific parameters, see [APIs](https://intl.cloud.tencent.com/document/product/1055/37120).

<span id="test1"></span>
#### Create a game server session

Run the following command to configure the `FleetId` parameter. You can set it to any valid strings `(^fleet-\S+)` in GSE Local.
```
curl -d '{"Action":"CreateGameServerSession", "FleetId":"fleet-1235", "MaximumPlayerSessionCount":5}' http://127.0.0.1:8080/capi
```

The following log message displayed in the command prompt window indicates that GSE Local has sent the `onStartGameServerSession` callback to your game server. If a game server session is successfully created, your game server will call the `ActivateGameServerSession` API to respond to the callback. The logs are as follows:
```
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"API to use: GSE.CreateGameServerSession, with input","req":"FleetId:<value:\"fleet-1235\" > MaximumPlayerSessionCount:<value:5 > "}
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"Reserved process: 41688 for GameServerSession: qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T09:37:08.580+0800","msg":"start to call StartGameSessionByGrpc to game server","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T09:37:08.597+0800","msg":"onGameSessionActivate received","pid":"4****","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe","requestId":"de1a678dea364db4b487ff84ad****31"}
{"level":"info","ts":"2020-10-20T09:37:08.598+0800","msg":"call StartGameSessionByGrpc to game server success","gameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
```

#### Querying a game server session

GSE Local uses `curl` to pass the game server session ID and object. Please note that the status of a new server session will change from “Activating” to “Active” after the game server calls the `ActivateGameServerSession` API. To view the status, run the following curl command to call the `DescribeGameServerSessions` API:
```
curl -d '{"Action":"DescribeGameServerSessions", "FleetId":"fleet-1235"}' http://127.0.0.1:8080/capi
```
The output is as shown below:
```
{"Response":{"GameServerSessions":[{"AvailabilityStatus":"Enable","CreationTime":"2020-10-20T01:37:08Z","CreatorId":"","CurrentCustomCount":0,"CurrentPlayerSessionCount":0,"DnsName":"","FleetId":"fleet-1235","GameProperties":[],"GameServerSessionData":"","GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-2fa56a09bffe","InstanceType":"localhost","IpAddress":"127.0.0.1","MatchmakerData":"","MaxCustomCount":0,"MaximumPlayerSessionCount":5,"Name":"","PlayerSessionCreationPolicy":"ACCEPT_ALL","Port":3237,"Status":"ACTIVE","StatusReason":"","TerminationTime":null,"Weight":0}],"NextToken":"","RequestId":"s1603158295201357000"}}
```

<span id="test4"></span>
## Testing Game Server and Client

#### Prerequisites
You have completed the [game server tests](#test).

### Step 1: add players
Run the following command to add players. The `GameServerSessionId` parameter is obtained in the response of the API used in [creating a game server session](#test1)
```
curl -d '{"Action":"JoinGameServerSession", "GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe", "PlayerId":"k****111"}' http://127.0.0.1:8080/capi
```

The GSE Local Command Prompt displays the following logs, indicating that the game server has sent the AcceptPlayerSession request to verify a new player connection.
```
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"API to use: GSE.JoinGameServerSession, with input","req":"GameServerSessionId:\"qcs::gse:local::gameserversession/fleet-****/gssess-c648654a-293b-4f1f-b71f-****6a09bffe\" PlayerId:\"ka****11\" "}
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"Creating player session with id: kadin111 for gameServersessionId: qcs::gse:local::gameserversession/fleet-****/gssess-c648654a-293b-4f1f-b71f-****6a09bffe"}
{"level":"info","ts":"2020-10-20T10:03:43.096+0800","msg":"Created player session with PlayerId: kadin111 and PlayerSessionId: psess-56dd6f48-08d4-4a11-9330-****09784977"}
```

### Step 2: query a player session

Call the `DescribePlayerSessions` to query a player session. The initial status of the player session is “Reserved”:
- If the client successfully connects to the game server within 1 minute, the player session status will become “Active”.
- If the client fails to connect to the game server within 1 minute, the player session status will become “TIMEDOUT”.

```
curl -d '{"Action":"DescribePlayerSessions", "GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-2fa56a09bffe", "PlayerId":"kadin111"}' http://127.0.0.1:8080/capi
```
The output is as shown below:
```
{"Response":{"NextToken":"","PlayerSessions":[{"CreationTime":"2020-10-20T02:03:43Z","DnsName":"","FleetId":"fleet-****","GameServerSessionId":"qcs::gse:local::gameserversession/fleet-1235/gssess-c648654a-293b-4f1f-b71f-****6a09bffe","IpAddress":"127.*.*.1","PlayerData":"","PlayerId":"ka****11","PlayerSessionId":"psess-56dd6f48-08d4-4a11-9330-****09784977","Port":3237,"Status":"TIMEDOUT","TerminationTime":"1970-01-01T00:00:00Z"}],"RequestId":"s16031596094****2000"}}% 
```

### Step 3: connect the client player to the server

After creating a game session and player session, you can directly use `localhost：port` to join a client player to the game session.

The GSE Local Command Prompt will display logs, indicating that the game server has sent the AcceptPlayerSession request to verify the new player connection. If you use `curl` to call the `DescribePlayerSessions` API, the player session status should be changed from “Reserved” to “Active”.


### Step 4: send the test report to GSE
To verify that your game server sends the game and player statuses to GSE, ensure your game server always send these statuses to GSE Local to help GSE Local manage player needs and correctly report metrics. GSE Local will record the following actions. You may also need `curl` to track the status change.
* **A player disconnects from the game session**
The GSE Local logs should display that the game server called the `RemovePlayerSession` API. The status in the response of the `DescribePlayerSessions()` API changed from “Active” to “Completed”. You can also call the `DescribeGameServerSessions` API to check that the current number of players in the game session has decreased by one.
* **The game session ends**
The GSL Local logs should display that the game server called the `TerminateGameServerSession` API. The status in the response of the `DescribeGameServerSessions` API changed from “Active” to “Terminated” or “Terminating”.
* **The server process stops**
The GSE Local logs should display that the game server called the `ProcessEnding` API.

## Testing Game Client Calls to GSE

All game session and player session APIs used in [game server tests](#test) and [game server and client tests](#test4) use `curl` to call GSE Local. You can use codes to call the following APIs in the game service to verify whether your game server is running properly. For the local debugging, you need to call `http://127.0.0.1:8080/capi`.
- [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)
- [DescribeGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37136)
- [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)
- [JoinGameServerSessionBatch](https://intl.cloud.tencent.com/document/product/1055/39130)
- [DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37135)

The GSE Local Command Prompt only displays the logs of the `CreateGameServerSession` API calls. As shown in the log message, GSE Local prompts the time when your game server launches a game session (using the `onStartGameServerSession` callback). After your game server uses the callback, GSE Local will obtain the ActivateGameServerSession response. You can `use` curl to view the calling of other APIs.

## Notes

Take notice of the following points when using GSE Local:
1. Different from the GSE Web service, GSE Local does not track the running status or the `onProcessTerminate` callback triggering of the server. GSE Local only records the runtime report of the game server.
2. The FleetId will not be verified during the calling of Tencent Cloud development kid, because this parameter can be set to any valid strings `(^fleet-\S+)`.
3. The game session created using GSE Local has a distinct ID structure, which contains `local` as shown below:
```
arn:gse:local::gamesession/fleet-****/gsess-56961f8e-db9c-4173-97e7-****82f0daa6
```





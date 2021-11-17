
## Installing gRPC
1. To use gRPC C#, you need to install .Net Core 3.1 SDK first. Taking CentOS as an example, the version must be v7, v8 or above.
  - Add the signature key
```
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm```
 - Install .NET Core SDK
```
 sudo yum install dotnet-sdk-3.1```
2. In addition, you can also use gRPC C# in the following runtime environments/IDEs:
 - Windows: .NET Framework 4.5 or higher, Visual Studio 2013 or higher, Visual Studio Code.
 - Linux: Mono 4 or higher, Visual Studio Code.
 - macOS X: Mono 4 or higher, Visual Studio Code, Visual Studio for Mac.


<dx-alert infotype="explain" title="">
 For more information on the installation process, please see [Installing gRPC C#](https://github.com/grpc/grpc/blob/v1.30.0/src/csharp/README.md#prerequisites).
</dx-alert>




## Defining Service
 gRPC uses Protocol Buffers to define a service: an RPC service specifies methods that can be called remotely by using parameters and return types.

>?We provide the .proto files for service definition. You can [click here](https://intl.cloud.tencent.com/document/product/1055/37419) to directly download them with no need to generate them by yourself.

## Generating gRPC Code
1. After defining the service, you can use protoc (protocol buffer compiler) to generate the client and server code (in any language supported by gRPC). 
2. The generated code includes the client stub and the abstract APIs to be implemented by the server.
3. Steps for generating gRPC code:
     - Download the code. In the `csharp-demo` directory, run
       ```
       dotnet run
       ```
         to automatically compile and run the service.
     - After the program is compiled and run correctly, the project's dependent libraries and binary files, and the .cs files created by compiling the `proto` file will be generated in the `csharp-demo/obj/Debug/netcoreapp3.1` folder.
     - The `proto` file is imported in `csharp-demo/csharpdemo.csproj`:
       ```
<Protobuf Include="..\proto\csharp-demo\GameServerGrpcSdkService.proto" Link="GameServerGrpcSdkService.proto"/>
<Protobuf Include="..\proto\csharp-demo\GseGrpcSdkService.proto" Link="GseGrpcSdkService.proto" />
       ```
       The project relies on the two `proto` files `GameServerGrpcSdkService.proto` and `GseGrpcSdkService.proto` in the `proto/csharp-demo` folder.

## Game Process Integration Process
![](https://main.qcloudimg.com/raw/96018551bc88c71a02333b1f197b3111.png)

#### Game server callback API list

| API Name | API Description |
|-----|----|
[OnHealthCheck](https://intl.cloud.tencent.com/document/product/1055/37422)| Runs health check |
|[OnStartGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37423)| Receives game server session |
|[OnProcessTerminate](https://intl.cloud.tencent.com/document/product/1055/37424)| Ends game process |

#### Game server active API list

| API Name | API Description |
|-----|----|
|[ProcessReady](https://intl.cloud.tencent.com/document/product/1055/37426)| Gets process ready |
|[ActivateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37427)| Activates game server session |
|[AcceptPlayerSession](https://intl.cloud.tencent.com/document/product/1055/37428)| Receives player session |
|[RemovePlayerSession](https://intl.cloud.tencent.com/document/product/1055/37429)| Removes player session |
|[DescribePlayerSessions](https://intl.cloud.tencent.com/document/product/1055/37430)| Gets player session list |
|[UpdatePlayerSessionCreationPolicy](https://intl.cloud.tencent.com/document/product/1055/37431)| Updates player session creation policy |
|[TerminateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37432)| Ends game server session |
|[ProcessEnding](https://intl.cloud.tencent.com/document/product/1055/37434)| Ends process |
|[ReportCustomData](https://intl.cloud.tencent.com/document/product/1055/37435)| Reports custom data |

#### Others

 When the game process uses gRPC to call a game server active API, you need to add two fields to `meta` of the gRPC request.

| Field      | Description                                      | Type   |
| --------- | ----------------------------------------- | ------ |
| pid       | `pid` of the current game process                         | string |
| requestId | `requestId` of the current request, which is used to uniquely identify a request | string |

1. Generally, after the server is initialized, the process will check itself to see whether it can provide services, and the game server will call the `ProcessReady` API to notify GSE that the process is ready to host a game server session. After receiving the notification, GSE will change the status of the server instance to "Active".
```
public static GseResponse ProcessReady(string[] logPath, int clientPort, int grpcPort)
{
	logger.Println($"Getting process ready, LogPath: {logPath}, ClientPort: {clientPort}, GrpcPort: {grpcPort}");
	// Set the ports
	var req = new ProcessReadyRequest{
		ClientPort = clientPort,
		GrpcPort = grpcPort,
	};
	// Log path
	req.LogPathsToUpload.Add(logPath);         // After being parsed by `pb`, the `repeated` type is read-only and needs to be added by running `Add`           
	// Ready to provide services
	return GrpcClient.GseClient.ProcessReady(req, meta);
}
```
2. After the process is ready, GSE will call the `OnHealthCheck` API to perform a health check on the game server every minute. If the health check fails three consecutive times, the process will be considered to be unhealthy, and no game server sessions will be assigned to it.
```
public override Task<HealthCheckResponse> OnHealthCheck(HealthCheckRequest request, ServerCallContext context)
{
	logger.Println($"OnHealthCheck, HealthStatus: {GseManager.HealthStatus}");
	return Task.FromResult(new HealthCheckResponse{
			HealthStatus = GseManager.HealthStatus
	});
}
```
3. Because the client calls the [CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139) API to create a game server session and assigns it to a process, GSE will be triggered to call the `onStartGameServerSession` API for the process and change the status of `GameServerSession` to "Activating".
```java
public override Task<GseResponse> OnStartGameServerSession(StartGameServerSessionRequest request, ServerCallContext context)
{
	logger.Println($"OnStartGameServerSession, request: {request}");
	GseManager.SetGameServerSession(request.GameServerSession);
	var resp = GseManager.ActivateGameServerSession(request.GameServerSession.GameServerSessionId, request.GameServerSession.MaxPlayers);
	return Task.FromResult(resp);
}
```
4. After the game server receives `onStartGameServerSession`, you need to handle the logic or resource allocation by yourself. After everything is ready, the game server will call the `ActivateGameServerSession` API to notify GSE that the game server session has been assigned to a process and is ready to receive player requests and will change the server status to "Active".
<dx-codeblock>
:::  Java
public static GseResponse ActivateGameServerSession(string gameServerSessionId, int maxPlayers)
{
	logger.Println($"Activating game server session, GameServerSessionId: {gameServerSessionId}, MaxPlayers: {maxPlayers}");
	var req = new ActivateGameServerSessionRequest{
			GameServerSessionId = gameServerSessionId,
			MaxPlayers = maxPlayers,
	};  
	return GrpcClient.GseClient.ActivateGameServerSession(req, meta);
}
:::
</dx-codeblock>
5. After the client calls the [JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/39130) API for the player to join, the game server will call the `AcceptPlayerSession` API to verify the validity of the player. If the connection is accepted, the status of `PlayerSession` will be set to "Active". If the client receives no response within 60 seconds after calling the `JoinGameServerSession` API, it will change the status of `PlayerSession` to "Timeout" and then call `JoinGameServerSession` again.
<dx-codeblock>
:::  Java
public static GseResponse AcceptPlayerSession(string playerSessionId)
{
	logger.Println($"Accepting player session, PlayerSessionId: {playerSessionId}");
	var req = new AcceptPlayerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			PlayerSessionId = playerSessionId,
	};            
	return GrpcClient.GseClient.AcceptPlayerSession(req, meta);
}
:::
</dx-codeblock>
6. After the game ends or the player exits, the game server will call the `RemovePlayerSession` API to remove the player, change the status of `playersession` to "Completed", and reserve the player slot in the game server session.
<dx-codeblock>
:::  java 
public static GseResponse RemovePlayerSession(string playerSessionId)
{
	logger.Println($"Removing player session, PlayerSessionId: {playerSessionId}");
	var req = new RemovePlayerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			PlayerSessionId = playerSessionId,
	};            
	return GrpcClient.GseClient.RemovePlayerSession(req, meta);
}
:::
</dx-codeblock>
7. After a game server session (a game battle or a service) ends, the game server will call the `TerminateGameServerSession` API to end the `GameServerSession` and change its status to `Terminated`.
<dx-codeblock>
:::  java 
public static GseResponse TerminateGameServerSession()
{
	logger.Println($"Terminating game server session, GameServerSessionId: {gameServerSession.GameServerSessionId}");
	var req = new TerminateGameServerSessionRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId
	};            
	return GrpcClient.GseClient.TerminateGameServerSession(req, meta);
}
:::
</dx-codeblock>
8. In case of health check failure or reduction, GSE will call the `OnProcessTerminate` API to end the game process. The reduction will be triggered according to the [protection policy](https://intl.cloud.tencent.com/document/product/1055/36675) configured in the GSE console.
<dx-codeblock>
:::  java 
 public override Task<GseResponse> OnProcessTerminate(ProcessTerminateRequest request, ServerCallContext context)
{
		logger.Println($"OnProcessTerminate, request: {request}");
		// Set the process termination time
		GseManager.SetTerminationTime(request.TerminationTime);
		// If the following two APIs are called, the game server session will be ended immediately. We recommend you call `ProcessEnding` to end the process only when there are no players or game server sessions
		// If the following two APIs are not called, `ProcessEnding` will be called to end the process according to the protection policy. We recommend you configure time-period protection

		// Terminate game server sessions
		GseManager.TerminateGameServerSession();
		// Exit the process
		GseManager.ProcessEnding();
		return Task.FromResult(new GseResponse{
				Status = GseResponse.Types.Status.Ok,
				ResponseData = "SUCCESS",
		});
}
:::
</dx-codeblock>
9. The game server calls the `ProcessEnding` API to end the process immediately, change the server process status to "Terminated", and repossess the resources.
<dx-codeblock>
:::  java 
// Active call: a game battle corresponds to a process. The `ProcessEnding` API will be actively called after the game battle ends
// Passive call: in case of reduction, process exception, or health check failure, the `ProcessEnding` API will be called passively according to the protection policy. If a full protection or time-period protection policy is configured, it is required to determine whether there are any players in the game server session before the passive call can be made
public static GseResponse ProcessEnding()
{
	logger.Println($"Process ending, pid: {pid}");
	var req = new ProcessEndingRequest();            
	return GrpcClient.GseClient.ProcessEnding(req, meta);
}
:::
</dx-codeblock>
10. The game server calls the `DescribePlayerSessions` API to get the information of the player in the game server session (which is optional based on your actual business needs).
<dx-codeblock>
:::  java 
public static DescribePlayerSessionsResponse DescribePlayerSessions(string gameServerSessionId, string playerId, string playerSessionId, string playerSessionStatusFilter, string nextToken, int limit)
{
	logger.Println($"Describing player session, GameServerSessionId: {gameServerSessionId}, PlayerId: {playerId}, PlayerSessionId: {playerSessionId}, PlayerSessionStatusFilter: {playerSessionStatusFilter}, NextToken: {nextToken}, Limit: {limit}");
	var req = new DescribePlayerSessionsRequest{
			GameServerSessionId = gameServerSessionId,
			PlayerId = playerId,
			PlayerSessionId = playerSessionId,
			PlayerSessionStatusFilter = playerSessionStatusFilter,
			NextToken = nextToken,
			Limit = limit,
	};            
	return GrpcClient.GseClient.DescribePlayerSessions(req, meta);
}
:::
</dx-codeblock>
11. The game server calls the `UpdatePlayerSessionCreationPolicy` API to update the player session creation policy and set whether to accept new players, i.e., whether to allow new players to join a game session (which is optional based on your actual business needs).
<dx-codeblock>
:::  java
public static GseResponse UpdatePlayerSessionCreationPolicy(string newPolicy)
{
	logger.Println($"Updating player session creation policy, newPolicy: {newPolicy}");
	var req = new UpdatePlayerSessionCreationPolicyRequest{
			GameServerSessionId = gameServerSession.GameServerSessionId,
			NewPlayerSessionCreationPolicy = newPolicy,
	};            
	return GrpcClient.GseClient.UpdatePlayerSessionCreationPolicy(req, meta);
}
:::
</dx-codeblock>
12. The game server calls the `ReportCustomData` API to notify GSE of the custom data (which is optional based on your actual business needs).
<dx-codeblock>
:::  java
public static GseResponse ReportCustomData(int currentCustomCount, int maxCustomCount)
{
	logger.Println($"Reporting custom data, CurrentCustomCount: {currentCustomCount}, MaxCustomCount: {maxCustomCount}");
	var req = new ReportCustomDataRequest{
			CurrentCustomCount = currentCustomCount,
			MaxCustomCount = maxCustomCount,
	};            
	return GrpcClient.GseClient.ReportCustomData(req, meta);
}
:::
</dx-codeblock>

## Launching Server for GSE to Call

Server running: launch `GrpcServer`.
<dx-codeblock>
:::  java
public class Program
{
public static int ClientPort = PortServer.GenerateRandomPort(2000, 6000);
public static int GrpcPort = PortServer.GenerateRandomPort(6001, 10000);

public static void Main(string[] args)
{
	CreateHostBuilder(args).Build().Run();
}
public static IHostBuilder CreateHostBuilder(string[] args) =>
Host.CreateDefaultBuilder(args)
	.ConfigureWebHostDefaults(webBuilder =>
	{
		webBuilder.ConfigureKestrel(options =>
		{
			 // gRPC port (set the HTTP/2 endpoint without TLS certificate)
			options.ListenAnyIP(GrpcPort, o => o.Protocols = 
					HttpProtocols.Http2);

			// HTTP port
			options.ListenAnyIP(ClientPort);
		});
	
		webBuilder.UseStartup<Startup>();
	});
}
:::
</dx-codeblock>

## Connecting Client to gRPC Server of GSE
Server connecting: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
<dx-codeblock>
:::  java
public class GrpcClient
{
	private static string agentAdress = "127.0.0.1:5758";
	public static GameServerGrpcSdkService.GameServerGrpcSdkServiceClient GameServerClient
	{
		get
		{
			Channel channel = new Channel(agentAdress, ChannelCredentials.Insecure);
			return new GameServerGrpcSdkService.GameServerGrpcSdkServiceClient(channel);
		}
	 }
	public static GseGrpcSdkService.GseGrpcSdkServiceClient GseClient
	{
		get
		{
			Channel channel = new Channel(agentAdress, ChannelCredentials.Insecure);
			return new GseGrpcSdkService.GseGrpcSdkServiceClient(channel);
		}
	}
}
:::
</dx-codeblock>


## Demo for C#
1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/csharp-demo.zip) to download the code of the Demo for C#.
2. Generate the gRPC code.
As the gRPC code has already been generated in the `proto/csharp-demo` directory of the Demo for C#, you do not need to generate it again.
3. Launch the server for GSE to call.
 - Implement the server.
`gameserversdk.cs` in the `csharp-demo/api` directory implements three server APIs.
 - Run the server.
`Program.cs` in the `csharp-demo` directory launches `GrpcServer`.
4. Connect the client to the gRPC server of GSE.
 - Implement the client.
`GseManager.cs` in the `csharp-demo/Models` directory implements nine client APIs.
 - Connect to the server.
Create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
5. Compile and run the program.
 1. Generate the executable file and dependencies
  ```
  dotnet publish -c Release -r linux-x64 --self-contained true 
  ```
 The above operation will generate all the dependent files needed to generate and package the asset package in the `csharp-demo/bin/Release/netcoreapp3.1/linux-x64` directory, which contains the executable file `csharpdemo` used to run the service.
 - Copy the pre-request script `install.sh`
 ```
 chmod u+x install.sh
cp install.sh bin/Release/netcoreapp3.1/linux-x64
 ```
 - Package the GSE asset package
 ```
 cd csharp-demo/bin/Release/netcoreapp3.1/linux-x64
zip -r csharpdemo.zip * 
 ```
The packaged `csharpdemo.zip` is the [asset package](https://intl.cloud.tencent.com/document/product/1055/36674) needed by GSE. Configure the launch path as `csharpdemo` with no launch parameter needed.
 - [Create a server fleet](https://intl.cloud.tencent.com/document/product/1055/36675) and deploy the asset package on it. After that, you can perform various operations such as [scaling](https://intl.cloud.tencent.com/document/product/1055/37445).

 

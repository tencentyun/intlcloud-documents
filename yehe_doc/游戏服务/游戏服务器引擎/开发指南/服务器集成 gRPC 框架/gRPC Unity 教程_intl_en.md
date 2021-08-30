This document describes how to integrate Unity with GSE SDK. The overall process mainly consists of two tasks:
1. Integrating Unity with gRPC
2. Integrating Unity with GSE SDK

## Prerequisites
You have already installed Unity Hub and Unity IDE.
>!This document uses 2018.3.5f1 or 2019.4.9f1 Unity engine and MacOS as an example.

## Integrating Unity with gRPC

gRPC has experimental support for Unity. For more information, see [README](https://github.com/grpc/grpc/tree/master/src/csharp/experimental). Perform the following steps to integrate Unity with gRPC:

### Step 1: create a Unity project 

Because gRPC APIs are only available for `.NET 4.5+`, it is necessary to create a Unity project equivalent to `.NET 4.x` at **Edit** > **Project Setting** > **Player** > **Configuration** > **Scripting Runtime Version**.
![](https://main.qcloudimg.com/raw/c28d0dc10bded3be2e98358a95a374fa.jpg)

<span id="test"></span>
### Step 2: download grpc_unity_package

Download the latest development version of `grpc_unity_package.VERSION.zip` [here](https://packages.grpc.io/). Click `Buidld ID` to redirect to the download page.
![](https://main.qcloudimg.com/raw/9ac9fa93e7de83042e1771cf0c4e6379.jpg)
Click to download `grpc_unity_package.VERSION.zip` under the `c#` directory.
![](https://main.qcloudimg.com/raw/8aa7bbbb7ab6076f28e711bc3bd92907.jpg)

### Step 3: decompress the package

Decompress the downloaded ` .zip` package to the `Assets` directory of the Unity project, as shown below:
![](https://main.qcloudimg.com/raw/3d319f3b4acbf2dea17f09e704e083fe.png)

### Step 4: test the package 

Unity Editor will fetch files and automatically add them to the project for your use of gRPC and Protobuf in codes. If Unity Editor prompts an error, see [FAQs](https://intl.cloud.tencent.com/document/product/1055/39059) for troubleshooting.

## Integrating Unity with GSE SDK

Complete the following steps to integrate Unity with GSE SDK:

### Step 1: obtain the GSE SDK Protobuf files

Obtain the `GameServerGrpcSdkService.proto` and `GseGrpcSdkService.proto` files of GSE SDK Protobuf. For more information, see [proto File](https://intl.cloud.tencent.com/document/product/1055/37419)
<span id="test2"></span>
### Step 2: generate C# codes based on Protobuf
1. Access the [grpc_unity_package.VERSION.zip](#test) page again to download the gRPC protoc Plugin package compatible with your operating system.
![](https://main.qcloudimg.com/raw/0ae70c8558f0a07a04d72554004faa76.png)
2. Decompress the package to obtain the `protoc` and `grpc_csharp_plugin` executable programs.
![](https://main.qcloudimg.com/raw/3e78515f814018e653fe85809da36800.png)
<span id="test3"></span>
3. Copy `protoc` and `grpc_csharp_plugin` executable programs to the same directory as the Protobuf file. Run the following two commands according to the operating system to generate `C#` codes:
 -  **For MAC and Linux OS:**
    - `protoc -I ./ --csharp_out=. GseGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin`
    - ` protoc -I ./ --csharp_out=. GameServerGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin`
 - **For Windows OS:**
    - ` ./protoc -I ./ --csharp_out=. GseGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin.exe `
    - ` ./protoc -I ./ --csharp_out=. GameServerGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin.exe`

 Four `.cs` code files are generated as shown in the following figure.
  ![](https://main.qcloudimg.com/raw/0ce56e0ea9abae1197b96587621d84f9.png)

### Step 3: develop and use GSE SDK on the Unity server

Copy the four `.cs` files generated in the [Step 2](#test2) to the Unity project (to a separate folder under the `Assets/Scripts/` directory) and use GSE SDK for the development. For more information, see [Unity DEMO](#test5).
1. Implement the `OnHealthCheck`, `OnStartGameServerSession` and ` OnProcessTerminate` APIs defined by `gameserver_grpcsdk_service.proto`.
``` JavaScript
 public class GrpcServer : GameServerGrpcSdkService.GameServerGrpcSdkServiceBase
    {
        private static Logs logger
        {
            get
            {
                return new Logs();
            }
        }
        // Health checks
        public override Task<HealthCheckResponse> OnHealthCheck(HealthCheckRequest request, ServerCallContext context)
        {
            logger.Println($"OnHealthCheck, HealthStatus: {GseManager.HealthStatus}");
            logger.Println($"OnHealthCheck, GameServerSession: {GseManager.GetGameServerSession()}");
            return Task.FromResult(new HealthCheckResponse
            {
                HealthStatus = GseManager.HealthStatus
            });
        }
        // Receive game sessions
        public override Task<GseResponse> OnStartGameServerSession(StartGameServerSessionRequest request, ServerCallContext context)
        {
            logger.Println($"OnStartGameServerSession, request: {request}");
            GseManager.SetGameServerSession(request.GameServerSession);
            var resp = GseManager.ActivateGameServerSession(request.GameServerSession.GameServerSessionId, request.GameServerSession.MaxPlayers);
            logger.Println($"OnStartGameServerSession, resp: {resp}");
            return Task.FromResult(resp);
        }    
        // End the game process
        public override Task<GseResponse> OnProcessTerminate(ProcessTerminateRequest request, ServerCallContext context)
        {
            logger.Println($"OnProcessTerminate, request: {request}");
            // Set the process termination time
            GseManager.SetTerminationTime(request.TerminationTime);
            // Terminate game server sessions
            GseManager.TerminateGameServerSession();
            // Exit the process
            GseManager.ProcessEnding();
            return Task.FromResult(new GseResponse());
        }
    }
```
2. Develop Unity server programs (taking ChatServer as an example). 
``` JavaScript
public static void StartChatServer(int clientPort)
    {
        RegisterHandlers();
        logger.Println("ChatServer Listen at " + clientPort);
        NetworkServer.Listen(clientPort);
    }
```
3. Develop the gRPC server.
``` JavaScript
public static void StartGrpcServer(int clientPort, int grpcPort, string logPath)
    {
        try
        {
           Server server = new Server
           {
              Services = { GameServerGrpcSdkService.BindService(new GrpcServer()) },
              Ports = { new ServerPort("127.0.0.1", grpcPort, ServerCredentials.Insecure) },
            };
            server.Start();
            logger.Println("GrpcServer Start On localhost:" + grpcPort);
            GseManager.ProcessReady(new string[] { logPath }, clientPort, grpcPort);
        }
        catch (System.Exception e)
        {
           logger.Println("error: " + e.Message);
        }
    }
```
4. Launch the implemented server and the gRPC server.
``` JavaScript
public class StartServers : MonoBehaviour
{
		private int grpcPort = PortServer.GenerateRandomPort(2000, 6000);
		private int chatPort = PortServer.GenerateRandomPort(6001, 10000);
		private const string logPath = "./log/log.txt";
		// Start is called before the first frame update
		[Obsolete]
		void Start()
		{
			 // Start ChatServer By UNet's NetWorkServer, Listen on UDP protocol
			 MyChatServer.StartChatServer(chatPort);
			 // Start GrpcServer By Grpc, Listen on TCP protocol
			 MyGrpcServer.StartGrpcServer(chatPort, grpcPort, logPath);
		}
		[Obsolete]
		void OnGUI()
		{
		}
}
```

<span id="test5"></span>

## Unity DEMO

1. [Click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/unity-demo.zip) to download the code of the Demo for Unity.
2. Import grpc unity package.
   Decompress grpc_unity_package in the [Step 2](#test2) to the `unity-demo/Assets` directory of the Demo project.
3. Generate C# codes based on the [Protobuf](#test3) file.
4. Launch the server for GSE to call.
 - Implement the server: implement the three server APIs in the `GrpcServer.cs` file under the `unity-demo/Assets/Scripts/Api` directory.
 - Run the server: create `gRPC Server` and `StartServers.cs` in the `MyGrpcServer.cs` file under the `unity-demo/Assets/Scripts` directory to launch `gRPC Server`.
5. Connect the client to the gRPC server of GSE.
 - Implement the client: implement the nine client APIs in the `Gsemanager.cs` file under the `unity-demo/Assets/Scripts/Gsemanager` directory.
 - Connect to the server: create a gRPC channel, specify the host name and server port to connect to, and use this channel to create a stub instance.
6. Compile and run the program
   Use Unity Editor to encapsulate the executable program of the target system into an asset package, and configure the actual name of the executable program at the launch path.

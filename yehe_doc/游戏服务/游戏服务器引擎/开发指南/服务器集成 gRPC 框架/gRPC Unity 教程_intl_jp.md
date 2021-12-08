ここでは、GSE SDKとUnityを統合するプロセスについて説明します。このプロセスには主に次の2つの作業が含まれます。
1.UnityにgRPCを統合。
2.UnityにGSE SDKを統合。

## 前提条件
Unity Hub、Unity IDEがインストール済みであること。
>!このドキュメンテーションは、Unity エンジン：2018.3.5f1、2019.4.9f1，OS：MacOSをベースとしています。

## UnityにgRPCを統合

gRPCのUnityに対するサポートはまだ実験段階にあり、詳細な情報については[README](https://github.com/grpc/grpc/tree/master/src/csharp/experimental)をご参照ください。具体的な操作手順は次のとおりです。

### 手順1：Unityプロジェクトの作成 

`.NET 4.x` に対応する同等バージョンのUnityプロジェクトを作成する必要があります。gRPC APIは `.NET 4.5+` のみ使用可能であるため、この手順が必要です。**Edit**>**Project Setting**>**Player**>**Configuration**>**Scripting Runtime Version**にて設定を行います。
![](https://main.qcloudimg.com/raw/c28d0dc10bded3be2e98358a95a374fa.jpg)

<span id="test"></span>
### 手順2：grpc_unity_packageをダウンロード

`grpc_unity_package.VERSION.zip` の [最新開発バージョン](https://packages.grpc.io/)をダウンロードします。 `Buidld ID` をクリックすると、ダウンロードページにリダイレクトされます。
![](https://main.qcloudimg.com/raw/9ac9fa93e7de83042e1771cf0c4e6379.jpg)
`c#` ディレクトリの `grpc_unity_package.VERSION.zip` をクリックして、ダウンロードします。
![](https://main.qcloudimg.com/raw/8aa7bbbb7ab6076f28e711bc3bd92907.jpg)

### 手順3： 解凍

下図に示すとおり、ダウンロードした**.zip**ファイルをUnity プロジェクトの**Assets** ディレクトリに解凍します。
![](https://main.qcloudimg.com/raw/3d319f3b4acbf2dea17f09e704e083fe.png)

### 手順4：テスト 

Unity Editorがファイルを取り出し、プロジェクトに自動的に追加されるので、コードでgRPCとProtobufが使用できます。UnityEditorがエラーを表示する場合は、[よくあるご質問](https://intl.cloud.tencent.com/document/product/1055/39059)をご参照ください。

## UnityとGSE SDKの統合

UnityとGSE SDKの統合は、次の手順を踏みます。

### 手順1： GSE SDK Protobufファイルを取得

GSE SDK Protobufファイル `GameServerGrpcSdkService.proto` および `GseGrpcSdkService.proto`を取得します。詳細は [protoファイル](https://intl.cloud.tencent.com/document/product/1055/37419)をご参照ください。
<span id="test2"></span>
### 手順2： Protobufに基づきC#コードを生成
1. gRPC protoc Pluginをダウンロードするために、再度 [grpc_unity_package.VERSION.zip](#test) ダウンロードページにアクセスし、OSに対応するprotoc 圧縮パッケージをダウンロードします。
![](https://main.qcloudimg.com/raw/0ae70c8558f0a07a04d72554004faa76.png)
2. 圧縮パッケージを解凍し、 `protoc` および `grpc_csharp_plugin` を取得すれば、プログラムを実行できます。
![](https://main.qcloudimg.com/raw/3e78515f814018e653fe85809da36800.png)
<span id="test3"></span>
3. `protoc`と` grpc_csharp_plugin`の実行可能プログラムをProtobufファイルと同一のディレクトリにコピーした後、このディレクトリで次の2つのコマンドを実行し、 `C＃`コードを生成します。
 -  **MACおよびLinux 環境でのコマンドは次のとおりです**
    - `protoc -I ./ --csharp_out=. GseGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin`
    - ` protoc -I ./ --csharp_out=. GameServerGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin`
 - **Windows環境でのコマンドは次のとおりです**
    - ` ./protoc -I ./ --csharp_out=. GseGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin.exe `
    - ` ./protoc -I ./ --csharp_out=. GameServerGrpcSdkService.proto --grpc_out=. --plugin=protoc-gen-grpc=grpc_csharp_plugin.exe`

 下図に示すとおり、4つの `.cs` コードファイルが生成されます。
  ![](https://main.qcloudimg.com/raw/0ce56e0ea9abae1197b96587621d84f9.png)

### 手順3：UnityサーバーでのGSE SDKの開発と使用

[手順2](#test2) で生成された4つの `.cs` ファイルをUnityプロジェクトにコピーして（Assets/Scripts/ディレクトリの個別のフォルダにコピー）、GSE SDKを開発に使用できます。詳細は [Unity DEMO](#test5)をご参照ください。
1. `gameserver_grpcsdk_service.proto`で定義された3つのインターフェース `OnHealthCheck`、`OnStartGameServerSession` および ` OnProcessTerminate`を実装します。
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
        // ヘルスチェック
        public override Task<HealthCheckResponse> OnHealthCheck(HealthCheckRequest request, ServerCallContext context)
        {
            logger.Println($"OnHealthCheck, HealthStatus: {GseManager.HealthStatus}");
            logger.Println($"OnHealthCheck, GameServerSession: {GseManager.GetGameServerSession()}");
            return Task.FromResult(new HealthCheckResponse
            {
                HealthStatus = GseManager.HealthStatus
            });
        }
        // ゲームセッションの受信
        public override Task<GseResponse> OnStartGameServerSession(StartGameServerSessionRequest request, ServerCallContext context)
        {
            logger.Println($"OnStartGameServerSession, request: {request}");
            GseManager.SetGameServerSession(request.GameServerSession);
            var resp = GseManager.ActivateGameServerSession(request.GameServerSession.GameServerSessionId, request.GameServerSession.MaxPlayers);
            logger.Println($"OnStartGameServerSession, resp: {resp}");
            return Task.FromResult(resp);
        }    
        // ゲームプロセスの終了
        public override Task<GseResponse> OnProcessTerminate(ProcessTerminateRequest request, ServerCallContext context)
        {
            logger.Println($"OnProcessTerminate, request: {request}");
            // プロセス終了時間の設定
            GseManager.SetTerminationTime(request.TerminationTime);
            // ゲームサーバーセッションの終了
            GseManager.TerminateGameServerSession();
            // プロセスの終了
            GseManager.ProcessEnding();
            return Task.FromResult(new GseResponse());
        }
    }
```
2. Unityサーバープログラムを開発します（ChatServerを例示します）。 
``` JavaScript
public static void StartChatServer(int clientPort)
    {
        RegisterHandlers();
        logger.Println("ChatServer Listen at " + clientPort);
        NetworkServer.Listen(clientPort);
    }
```
3. gRPCサーバーを開発します。
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
4. 開発したサーバーとgRPCサーバーを起動します。
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
1.[ここをクリック]( https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/unity-demo.zip)して、Unity DEMOコードをダウンロードします。
2.grpc unity packageをインポートします。
   [手順2](#test2) の grpc_unity_packageをDemoプロジェクトのunity-demo/Assetsディレクトリに解凍します。
3.[Protobuf](#test3) ファイルに基づきC#コードを生成します。
4.GSEをコールするためにサーバーを起動します。
 - サーバーの実装は、`unity-demo/Assets/Scripts/Api` ディレクトリの `GrpcServer.cs` ファイルに、3つのサーバーインターフェースを実装します。
 - サーバーの実行は、`unity-demo/Assets/Scripts` ディレクトリの `MyGrpcServer.cs` ファイルに、`gRPC Server` と `StartServers.cs` を作成し、`gRPC Server` を起動します。
5.クライアントをGSEのgRPCサーバーに接続します。
 - クライアントの実装は、`unity-demo/Assets/Scripts/Gsemanager` ディレクトリの `Gsemanager.cs` ファイルに9個のクライアントインターフェースを実装します。
 - サーバーへの接続は、1つのgRPC channelを作成し、接続するホスト名とサーバーポートを指定した後、このchannelを使用してスタブインスタンスを作成します。
6.コンパイルして実行します。
   Unity Editorを使用してターゲットシステムの実行可能プログラムをアセットとしてパッケージ化し、起動パスで実行可能プログラム名を（実際の実行可能プログラム名に基づいて）設定します。

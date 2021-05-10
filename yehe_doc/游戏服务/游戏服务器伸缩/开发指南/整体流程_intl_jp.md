## 全体のフローチャート
![](https://main.qcloudimg.com/raw/70af47a2520180f93b202547acaadac8.png)
## 統合の手順
### 手順1：サーバーのgRPCフレームワークとの統合
ゲームサーバーとGSEはgRPCを介して通信し、ゲームサーバープログラムはgRPCフレームワークと統合することで多くの言語によるプログラミングが実現し、ゲームサーバーの実行可能ファイルが生成されます。各言語のサーバーでGSEを統合するための具体的なチュートリアルについては、Tencent Cloud [gRPC-C++ チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37408)、[gRPC-C# チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37409)、[gRPC-Go チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37410)、[gRPC-Java チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37411)、[gRPC-Lua チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37412)、[gRPC-Nodejs チュートリアル](https://intl.cloud.tencent.com/document/product/1055/37413) ドキュメントをご参照ください。その他言語については、 [gRPC公式ドキュメント](http://doc.oschina.net/grpc)をご参照ください。

### 手順2：プログラムのリリース

1. アセットのアップロード 
アセットにはゲームサーバーの実行可能ファイル、依存パッケージおよびインストールスクリプトが含まれ、これらはzipパッケージにパッケージ化してからアップロードする必要があります。詳細については、 [アセットの作成](https://intl.cloud.tencent.com/document/product/1055/36674)をご参照ください。
2. サーバーフリートの作成 
アップロードされたアセットを作成したサーバーフリートにデプロイし、プロセス管理、デプロイ設定、スケーリング設定などを完了します。詳細については、[サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)をご参照ください。   

### 手順3：TencentCloud APIを呼び出し、サーバーアドレス（IP:port）を取得

ゲームサーバーセッションを作成するか、ゲームサーバーセッションを配置することによって、サーバーアドレス（IP:port）を取得できます。

#### 方法一：ゲームサーバーセッションの作成
TencentCloud APIの呼び出し：
各種ゲームサーバーセッションのサポート方式に応じて、多様なクライアントクラウドAPI呼び出しプロセスがあります。
-  1つのゲームサーバーセッションが1つのゲームのみをサポートする場合：
   - ゲームサーバーセッションを作成します（[CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)）。
   - ゲームサーバーセッションに参加します（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）。
-  1つのゲームサーバーセッションが複数のゲームまたは1つのサービス（ゲームサーバーへのログインなど）をサポートする場合。
   - ゲームサーバーセッションリストを確認するか（[DescribeGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37136)）、またはゲームサーバーセッションリストを検索します（[SearchGameServerSessions](https://intl.cloud.tencent.com/document/product/1055/37131)）。
   - ゲームサーバーセッションがすでに存在する場合は、ゲームサーバーセッションに参加します（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）。
   - ゲームサーバーセッションが存在しない場合は、まずゲームサーバーセッションを作成し（[CreateGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37139)）、その後、ゲームサーバーセッションに参加します（[JoinGameServerSession](https://intl.cloud.tencent.com/document/product/1055/37132)）。

TencentCloud API呼び出しの具体的な操作については、 [ゲームサーバーセッションの作成](https://intl.cloud.tencent.com/document/product/1055/37416) のドキュメントをご参照ください。

#### 方法二：ゲームサーバーセッションの配置
TencentCloud APIの呼び出し：
 - ゲームサーバーセッションの配置を開始します（[StartGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37130)）。
 - ゲームサーバーセッションの配置を確認します（[DescribeGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37137)）。
 - ゲームサーバーセッションの配置を停止します（[StopGameServerSessionPlacement](https://intl.cloud.tencent.com/document/product/1055/37129)）。

TencentCloud API呼び出しの具体的な操作については、[ゲームサーバーセッションの配置](https://intl.cloud.tencent.com/document/product/1055/37417) のドキュメントをご参照ください。

### 手順4：クライアントがIP:portを介してサーバーに接続
手順3でサーバーのIP:portがすでに返されている場合、クライアントは、そのIP:portを介してターゲットサーバーにアクセスできます。

## ワークフローチャート
![](https://main.qcloudimg.com/raw/02ec2067c8e06f5e1d1f3130aee7b81d.png)

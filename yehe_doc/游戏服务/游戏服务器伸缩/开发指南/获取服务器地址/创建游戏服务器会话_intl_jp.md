
## 概要
- ゲーム開発者はクライアントTencentCloud APIを使用してゲームサーバーセッションを作成できます。セッションを作成するには、次の2つの方法があります。
  - サーバーフリートを作成することによって、自動スケーリングとヘルスチェックの機能を実装できます。
  - エイリアスを作成することによって、ダウンタイムゼロでアップデートを実装できます。
- 1つのサーバープロセスに1つのゲームサーバーセッションが配置されますが、ゲームサーバーセッションのサポートに応じて、クライアントAPI呼び出しプロセスは異なります。

## クライアントAPI呼び出しプロセス
### 1つのゲームサーバーセッションが1つのゲームをサポートする場合
1つのゲームサーバーセッションが1つのゲームのみをサポートする場合、クライアントAPIの呼び出しプロセスは次のとおりです。
<span id="CreateGameServerSession"></span>
1. まず、サーバーフリートまたはエイリアスを介してゲームサーバーセッションを作成します。具体的な操作については、[ゲームサーバーセッションの作成](https://intl.cloud.tencent.com/document/product/1055/37139) のAPIドキュメントをご参照ください。
>?次の例はすべてJavaをベースとしています。

  ```
  public class CreateGameServerSession
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}";
                CreateGameServerSessionRequest req = CreateGameServerSessionRequest.fromJsonString(params, CreateGameServerSessionRequest.class);

                CreateGameServerSessionResponse resp = client.CreateGameServerSession(req);
 
                System.out.println(CreateGameServerSessionRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

<span id="JoinGameServerSession"></span>
2. 次に、作成したゲームサーバーセッションに参加します。具体的な操作については、[ゲームサーバーセッションに参加](https://intl.cloud.tencent.com/document/product/1055/37132) のAPIドキュメントをご参照ください。

 ```
public class JoinGameServerSession
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}";
                JoinGameServerSessionRequest req = JoinGameServerSessionRequest.fromJsonString(params, JoinGameServerSessionRequest.class);

                JoinGameServerSessionResponse resp = client.JoinGameServerSession(req);

                System.out.println(JoinGameServerSessionRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                    System.out.println(e.toString());
            }
        }
    }
```

### 1つのゲームサーバーセッションが複数のゲームまたは1つのサービスをサポートする場合
1つのゲームサーバーセッションが複数のゲームまたは1つのサービスをサポートする場合、クライアント APIの呼び出しプロセスは次のとおりです。
1. まず、ゲームサーバーセッションリストを確認して、ゲームサーバーセッションが存在するかどうかを判断します。具体的な操作については、[ゲームサーバーセッションリストの確認](https://intl.cloud.tencent.com/document/product/1055/37136) のAPIドキュメントをご参照ください。

 ```
public class DescribeGameServerSessions
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}"; 
                DescribeGameServerSessionsRequest req = DescribeGameServerSessionsRequest.fromJsonString(params, DescribeGameServerSessionsRequest.class);

                DescribeGameServerSessionsResponse resp = client.DescribeGameServerSessions(req);

                System.out.println(DescribeGameServerSessionsRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
    }
```

  ゲームサーバーセッションリストを検索して、ゲームサーバーセッションが存在するかどうかを判断することもできます。具体的な操作については、[ゲームサーバーセッションリストの検索](https://intl.cloud.tencent.com/document/product/1055/37131) のAPIドキュメントをご参照ください。

 ```
public class SearchGameServerSessions
{
        public static void main(String [] args) {
            try{

                Credential cred = new Credential("", "");

                HttpProfile httpProfile = new HttpProfile();
                httpProfile.setEndpoint("gse.tencentcloudapi.com");

                ClientProfile clientProfile = new ClientProfile();
                clientProfile.setHttpProfile(httpProfile);

                GseClient client = new GseClient(cred, "", clientProfile);

                String params = "{}";
                SearchGameServerSessionsRequest req = SearchGameServerSessionsRequest.fromJsonString(params, SearchGameServerSessionsRequest.class);

                SearchGameServerSessionsResponse resp = client.SearchGameServerSessions(req);

                System.out.println(SearchGameServerSessionsRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

2. ゲームサーバーセッションがすでに存在する場合は、ゲームサーバーセッションに直接参加できます。具体的な操作については、[ゲームサーバーセッションに参加](https://intl.cloud.tencent.com/document/product/1055/37132) のAPIドキュメントか、このテキストの [サンプルコード](#JoinGameServerSession)をご参照ください。
3. ゲームサーバーセッションが存在しない場合は、まずゲームサーバーセッションを作成する必要があります。具体的な操作については、[ゲームサーバーセッションの作成](https://intl.cloud.tencent.com/document/product/1055/37139) のAPIドキュメントか、このテキストの [サンプルコード](#CreateGameServerSession)をご参照ください。その後、ゲームサーバーセッションに参加します。具体的な操作については、 [ゲームサーバーセッションに参加](https://intl.cloud.tencent.com/document/product/1055/37132) のAPIドキュメントか、このテキストの [サンプルコード](#JoinGameServerSession)をご参照ください。

>?[API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=CreateGameServerSession&SignVersion=) を使用してオンラインデバッグを実行できます。左側の「Game Server Engine」/「サービス管理関連インターフェース」内の対応するTencentCloud APIを選択すれば、「コード生成」、「オンラインコール」などの操作を実行できます。


## 概要
ゲーム開発者は、クライアントクラウドAPIを使用してゲームサーバーセッションを配置できます。言い換えれば、ゲームサーバーキューを介して、近隣のスケジューリング、クロスリージョン災害復旧の機能を実装できます。

## クライアントAPI呼び出しプロセス
1. まず、ゲームサーバーセッションの配置をクエリーし、ゲームサーバーセッションがプロセスに配置されているかどうかを確認します。具体的な操作については、[ゲームサーバーセッションの配置の確認](https://intl.cloud.tencent.com/document/product/1055/37137) のAPIドキュメントをご参照ください。
  >?次の例はすべてJavaをベースとしています。

 ```
public class DescribeGameServerSessionPlacement
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
                DescribeGameServerSessionPlacementRequest req = DescribeGameServerSessionPlacementRequest.fromJsonString(params, DescribeGameServerSessionPlacementRequest.class);
 
                DescribeGameServerSessionPlacementResponse resp = client.DescribeGameServerSessionPlacement(req);

                System.out.println(DescribeGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
 }
 ```
  
2. 次に、ゲームサーバーセッションの配置を開始できます。具体的な操作については、[ゲームサーバーセッションの配置開始](https://intl.cloud.tencent.com/document/product/1055/37130) のAPIドキュメントをご参照ください。

 ```
public class StartGameServerSessionPlacement
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
                StartGameServerSessionPlacementRequest req = StartGameServerSessionPlacementRequest.fromJsonString(params, StartGameServerSessionPlacementRequest.class);
 
                StartGameServerSessionPlacementResponse resp = client.StartGameServerSessionPlacement(req);

                System.out.println(StartGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```

3. 最後に、ゲームサーバーセッションの配置を停止します。具体的な操作については、[ゲームサーバーセッションの配置停止](https://intl.cloud.tencent.com/document/product/1055/37129) のAPIドキュメントをご参照ください。

 ```
public class StopGameServerSessionPlacement
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
                StopGameServerSessionPlacementRequest req = StopGameServerSessionPlacementRequest.fromJsonString(params, StopGameServerSessionPlacementRequest.class);

                StopGameServerSessionPlacementResponse resp = client.StopGameServerSessionPlacement(req);

                System.out.println(StopGameServerSessionPlacementRequest.toJsonString(resp));
            } catch (TencentCloudSDKException e) {
                System.out.println(e.toString());
            }
        }
}
```
>? [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gse&Version=2019-11-12&Action=DescribeGameServerSessionPlacement&SignVersion=) を使用してオンラインデバッグを実行できます。左側の「Game Server Engine」/「サービス管理関連インターフェース」の対応するTencentCloud APIを選択すれば、「コード生成」、「オンラインコール」などの操作を実行できます。

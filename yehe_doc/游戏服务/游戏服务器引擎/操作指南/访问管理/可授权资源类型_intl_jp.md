
Game Server Elastic-scaling（GSE）は、リソースレベルの権限をサポートします。つまり、特定のGSE操作について、ユーザーが操作を実行できるタイミングやユーザーが使用できる特定のリソースを制御できます。次の表はGSEが許可を与えることができるリソースの種類について説明するものです。

>? リソースレベルの権限とは、ユーザーが操作を実行できるのはどのリソースか指定することをいいます。

Cloud Access Management（CAM）で、操作を許可できるリソースの種類は以下のとおりです：

| リソースのタイプ                              | 承認ポリシーにおけるリソースの記述メソッド  
| :------------------------------------ | :---------------------------------------------------- |
| [GSEアセット関連](#test1)         | `qcs::gse:$region:$account:asset/* `                  |
| [GSEエイリアス関連](#test1)         | `qcs::gse:$region:$account:alias/* `                  |
| [GSEフリート関連](#test1)         | `qcs::gse:$region:$account:fleet/* `                 |
| [GSEゲームサーバーキュー関連](#test4) | `qcs::gse:$region:$account:gameServerSessionQueue/* ` |

[GSEアセット関連](#test1)、[GSEエイリアス関連](#test2) および [GSEフリート関連](#test3)は、それぞれ現在リソースレベルの権限をサポートするGSE API操作および各操作でサポートされるリソースについて説明します。リソースパスを設定すると、$region、$account などの変数パラメータを実際のパラメータに変更する必要があります。またパスに `*` ワイルドカードを使用することもできます。関連の操作デモについては、 [アクセス制御デモ](https://intl.cloud.tencent.com/document/product/1055/37779)を参照してください。

>? リストに載っていないGES API操作は、リソースレベル権限をサポートしていないことを示します。リソースレベル権限をサポートしていないGES API操作に対しても、この操作を利用する権限を許可できますが、ポリシーステートメントのリソース要素を `*` に指定する必要があります。

<span id="test1"></span>
### GSEアセット関連

| API 操作      | リソースパス                                                     | 説明             |
| :------------ | :----------------------------------------------------------- | :--------------- |
| DeleteAsset   | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId` |アセットの削除       |
| DescribeAsset | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId ` | アセットの属性を検索       |
| UpdateAsset   | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId ` | アセットの属性を更新       |

<span id="test2"></span>
### GSEエイリアス関連

| API 操作      | リソースパス                                                     | 説明                    |
| :------------ | :----------------------------------------------------------- | :---------------------- |
| DeleteAlias   | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | エイリアス削除                |
| DescribeAlias | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | エイリアスの属性を検索          |
| ResolveAlias  | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId` | エイリアスに関連付けられたフリートIDを検索 |
| UpdateAlias   | `qcs::gse:$region:$account:alias/*`<br>`qcs::gse:$region:$account:alias/$AliasId ` | エイリアスの属性を更新          |

<span id="test3"></span>
### GSEフリート関連

| API 操作                     | リソースパス                                                     | 説明                             |
| :--------------------------- | :----------------------------------------------------------- | :------------------------------- |
| AttachCcnInstances           | `qcs::gse:$region:$account:asset/*`<br>`qcs::gse:$region:$account:asset/$AssetId` |　CCNインスタンスの関連付け                   |
| CreateFleetDemo              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートデモの作成                    |
| DeleteFleet                  | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | ブランクのフリートの削除                       |
 DeleteScalingPolicy          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | スケーリングポリシーの削除               |
| DescribeFleetEvents          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートのイベントログからエントリーを検索       |
| DescribeFleetPortSettings    | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートのインバウンドアクセス権限を検索           |
| DescribeInstances            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートインスタンス情報を検索              |
| DescribeInstancesExtend      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートインスタンスの拡張情報を検索           |
| DescribeRuntimeConfiguration | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートのランタイム設定を検索             |
| DescribeScalingPolicies      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId ` | フリートのすべてのスケーリングポリシーを検索         |
| DetachCcnInstances           | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | CCNインスタンスの関連付けを解除                |
| GetInstanceAccess            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | 指定のフリートインスタンスへのリモートアクセス権限をリクエスト |
| PutScalingPolicy             | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | スケーリングポリシーの作成または更新             |
| SetServerWeight              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | サーバーの加重値の設定                   |
| StartFleetActions            | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリート上の自動スケーリングアクティビティを開始       |
| StopFleetActions             | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリート上の自動スケーリングアクティビティを一時停止       |
| UpdateDemoResource           | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | サービスデプロイデモのソース属性を修正           |
| UpdateFleetAttributes        | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートの通常属性を更新               |
| UpdateFleetCapacity          | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートの容量を更新                   |
| UpdateFleetName              | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` |サーバーフリート名を更新 |
| UpdateFleetPortSettings      | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | フリートのポート設定を更新              |
| UpdateFleetVpc               | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` | ゲームサーバーフリート VPCを更新             |
| UpdateRuntimeConfiguration   | `qcs::gse:$region:$account:fleet/*`<br>`qcs::gse:$region:$account:fleet/$FleetId` |フリートランタイムの通常設定を更新         |

<span id="test4"></span>
### GSEキュー関連

| API 操作                        | リソースパス                                                   | 説明                                                |
| :------------------------------ | :----------------------------------------------------------- | :--------------------------------------------------- |
| DeleteGameServerSessionQueue    | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$Name` | ゲームサーバーセッションキューを削除                               |
| StartGameServerSessionPlacement | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$GameServer`<br>`SessionQueueName` | ゲームサーバーセッション配置リクエストの<br>ゲームサーバーセッションキューへの送信を開始 |
| UpdateGameServerSessionQueue    | `qcs::gse:$region:$account:game`<br>`ServerSessionQueue/*`<br>`qcs::gse:$region:$account:game`<br>`ServerSessionQueue/$Name` | ゲームサーバーセッションキューの属性を更新                         |

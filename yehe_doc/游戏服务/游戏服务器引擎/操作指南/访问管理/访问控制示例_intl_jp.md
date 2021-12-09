
## シナリオ

Cloud Access Management（CAM）ポリシーを使用してGSEコンソールにおいて特定のリソースを表示して使用する権限をユーザーに付与できます。この例ではユーザーにコンソールの特定部分の使用を許可するポリシーとなっています。

## 操作手順

### GSE 全読み取り書き込みポリシー

ユーザーにGSEゲームを作成し管理する権限を持たせたい場合、そのユーザーに対してQcloudGSEFullAccess というポリシーを使用することができます。
具体的な操作手順は次のとおりです：
1.  [ポリシー管理インターフェース](https://console.cloud.tencent.com/cam/policy)に移動し、**サービスのタイプ**をクリックします。
2. ドロップダウンリストオプションで**Game Server Elastic-scaling**を選択します。また右上コーナーの検索機能を使用し、このポリシーを検索することもできます。

![](https://main.qcloudimg.com/raw/fe654b37e2fd44deac52743c77ecc477.png)

ポリシー構文は次のとおりです。

```
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "gse:*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

上記のポリシーによってユーザーは、サービスのアクティブ化、統計データの表示、アセット、エイリアス、フリート、ゲームサーバーセッションキュー、その他すべてのリソースに対する操作権限を持つことができます。

### GSEに対する読み取り専用ポリシー

ユーザーにすべてのGSEリソースをクエリーする権限のみを付与し、作成、削除および変更しないようにする場合は、ユーザーにQcloudGSEReadOnlyAccess というポリシーを使用できます。
具体的な操作手順は次のとおりです：
1.  [ポリシー管理インターフェース](https://console.cloud.tencent.com/cam/policy)に移動し、**サービスのタイプ**をクリックします。
2. ドロップダウンリストオプションで**Game Server Elastic-scaling**を選択します。また右上コーナーの検索機能を使用し、このポリシーを検索することもできます。

![](https://main.qcloudimg.com/raw/2368902dfcb590dd60e51b1720c0c07f.png)

ポリシー構文は次のとおりです。

```
{
  "version": "2.0",
  "statement": [
    {
      "action": [
        "gse:Get*",
        "gse:Describe*",
        "gse:List*",
        "gse:Resolve*",
        "gse:Search*",
        "gse:Check*"
      ],
      "resource": "*",
      "effect": "allow"
    }
  ]
}
```

### GSEサービスのステータスをクエリーするポリシー

ユーザーにGSE サービスアクティブ化ステータスをクエリーする権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称            | 説明             |
| --------------- | ---------------- |
| CheckOpenStatus | サービスのステータスのクエリー |

具体的な操作手順は次のとおりです：
1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、GSEサービスをアクティブ化できるカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:CheckOpenStatus"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

>!すべてのAPIリクエストはCheckOpenStatusをリクエストする必要があるため、すべてのカスタムポリシーにはCheckOpenStatus API の操作権限が含まれている必要があります。このAPIをカスタムポリシー に追加することも、上記例のカスタムポリシーをサブユーザーに個別に作成することもできます。

### GSEサービスのアクティブ化ポリシー

ユーザーにGSE サービスをアクティブ化する権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称          | 説明             |
| ------------- | ---------------- |
| SetOpenStatus | サービスアクティブ化ステータスの設定 |

具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、GSEサービスをアクティブ化できるカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:SetOpenStatus"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

### GSE 統計データを表示するポリシー

ユーザーにGSE サービス統計データをクエリーする権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                          | 説明                 |
| ----------------------------- | -------------------- |
| DescribeFleetStatisticDetails | フリートの統計詳細のクエリー     |
| DescribeFleetStatisticFlows   | フリートの統計用量のクエリー     |
| DescribeFleetStatisticSummary | フリートの統計概要のクエリー |
| ListFleets                    | フリートリストの検索         |

具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、GSEサービスの統計データを表示するためのカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:ListFleets",
                "gse:DescribeFleetStatisticDetails",
                "gse:DescribeFleetStatisticFlows",
                "gse:DescribeFleetStatisticSummary"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

### GSEマッチングポリシー

ユーザーにマッチング権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                | 説明                       |
| ------------------- | -------------------------- |
| StartMatchPlacement | マッチプレースメントゲームサーバーセッションの開始 |


具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、マッチングのためのカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "gse:StartMatchPlacement",
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

### GSEリストポリシー

ユーザーにGSE リストを検索する権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                            | 説明                           |
| ------------------------------- | ------------------------------ |
| DescribeAssets                  | アセットリストの検索                 |
| DescribeGameServerSessionQueues | ゲームサーバーセッションキューのクエリー       |
| DescribeFleetAttributes         | フリートの通常属性（ステータスを含む）の検索 |
| DescribeFleetCapacity           | 現在のフリートの容量設定の検索        |
| DescribeFleetUtilization        | フリートの利用率統計データの検索       |
| DescribeInstanceTypes           | サーバーインスタンスタイプリストの検索         |
| DescribeUserQuotas              | ユーザーの複数コンポーネント割当数の検索         |
| ListAliases                     | エイリアスリストの検索                   |
| ListFleets                      | フリートリストの検索                   |

具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、GSEサービスをアクティブ化できるカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DescribeFleetUtilization",
                "gse:DescribeInstanceTypes",
                "gse:DescribeFleetAttributes",
                "gse:DescribeFleetCapacity",
                "gse:DescribeUserQuotas",
                "gse:DescribeAssets",
                "gse:DescribeGameServerSessionQueues"
                "gse:ListAliases",
                "gse:ListFleets"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

### GSE 全読み取り書き込みポリシー、ただしサービスのアクティブ化とデータ統計は含まない

ユーザーに全読み取り書き込み権限を持たせたいが、そのサービスのアクティブ化とデータ統計の権限を承認したくない場合は、カスタマイズポリシーを追加し、そのポリシーをユーザーに関連付けることができます。ポリシーの内容は、次のポリシー構文を参考に設定してください：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "gse:SetOpenStatus",
                "gse:DescribeFleetStatisticDetails",
                "gse:DescribeFleetStatisticFlows",
                "gse:DescribeFleetStatisticSummary"
            ],
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```

### GSE アセットリソースポリシー

ユーザーにアカウント番号110702656のすべてのアセットの操作権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称          | 説明             |
| ------------- | ---------------- |
| DeleteAsset   | アセットの削除       |
| DescribeAsset | アセットの属性を検索 |
| UpdateAsset   | アセットのプロパティの更新 |


具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、アカウント番号110702656のすべてのアセットの操作権限を持つカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteAsset",
                "gse:DescribeAsset",
                "gse:UpdateAsset"
            ],
            "resource": "qcs::gse::uin/110702656:asset/*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

ユーザーに、例えばアカウント番号110702656の特定のアセット（AssetId=asset-eiu39dki-3o0dk2dk）の操作権限を持たせたい場合は、ポリシーの resource を次のとおり修正することができます：

```
qcs::gse::uin/110702656:asset/asset-eiu39dki-3o0dk2dk

```

### GSE エイリアスリソースポリシー

ユーザーに例えばアカウント番号110702656のすべてのエイリアスの操作権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称          | 説明                    |
| ------------- | ----------------------- |
| DeleteAlias   | エイリアスの削除                |
| DescribeAlias | エイリアスの属性を検索          |
| ResolveAlias  | エイリアスに関連付けられたフリートIDの検索 |
| UpdateAlias   | エイリアスの属性の更新          |


具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、アカウント番号110702656の全エイリアスの操作権限を持つカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteAlias",
                "gse:DescribeAlias",
                "gse:ResolveAlias",
                "gse:UpdateAlias"
            ],
            "resource": "qcs::gse::uin/110702656:alias/*",
            "effect": "allow"
        }
    ]
}

```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

ユーザーに例えばアカウント番号110702656の特定のエイリアス（AliasId=alias-wk30dke9-ovr93dk3）の操作権限を持たせたい場合は、ポリシーの resource を次のとおり修正することができます：

```
qcs::gse::uin/110702656:asset/alias-wk30dke9-ovr93dk3

```

### GSE フリートリソースポリシー

ユーザーに例えばアカウント番号110702656のすべてのフリートの操作権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                         | 説明                             |
| ---------------------------- | -------------------------------- |
| AttachCcnInstances           | CCNインスタンスの関連付け                  |
| CreateFleetDemo              | フリートデモの作成                     |
| DeleteFleet                  | ブランクのフリートの削除                       |
| DeleteScalingPolicy          | スケーリングポリシーの削除               |
| DescribeFleetEvents          | フリートのイベントログからエントリーを検索       |
| DescribeFleetPortSettings    | フリートのインバウンドアクセス権限を検索           |
| DescribeInstances            | フリートのインスタンス情報の検索               |
| DescribeInstancesExtend      | フリートインスタンスの拡張情報の検索          |
| DescribeRuntimeConfiguration | フリートのランタイム設定の検索             |
| DescribeScalingPolicies      | フリートのすべてのスケーリングポリシーの検索         |
| DetachCcnInstances           | CCNインスタンスの関連付けの解除                |
| GetInstanceAccess            | 指定のフリートインスタンスへのリモートアクセス権限のリクエスト |
| PutScalingPolicy             | スケーリングポリシーの作成または更新             |
| SetServerWeight              | サーバーの加重値の設定                   |
| StartFleetActions            | フリート上の自動スケーリングアクティビティの開始       |
| StopFleetActions            | フリート上の自動スケーリングアクティビティの一時停止       |
| UpdateDemoResource           | サービスデプロイデモのソース属性の変更           |
| UpdateFleetAttributes        | フリートの通常属性の更新               |
| UpdateFleetCapacity          | フリート容量の更新                   |
| UpdateFleetName | サーバーフリート名の更新 |
| UpdateFleetPortSettings      | フリートのポート設定の更新               |
| UpdateFleetVpc               | ゲームサービスフリート VPCの更新             |
| UpdateRuntimeConfiguration   | フリートランタイムの通常設定の更新         |


具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、アカウント番号110702656のすべてのフリート操作権限を持つカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
				"gse:AttachCcnInstances",
				"gse:CreateFleetDemo",
				"gse:DeleteFleet",
				"gse:DeleteScalingPolicy",
				"gse:DescribeFleetEvents",
				"gse:DescribeFleetPortSettings",
				"gse:DescribeInstances",
				"gse:DescribeInstancesExtend",
				"gse:DescribeRuntimeConfiguration",
				"gse:DescribeScalingPolicies",
				"gse:DetachCcnInstances",
				"gse:GetInstanceAccess",
				"gse:PutScalingPolicy",
				"gse:SetServerWeight",
				"gse:StartFleetActions",
				"gse:UpdateDemoResource",
				"gse:UpdateFleetAttributes",
				"gse:UpdateFleetCapacity",
				"gse:UpdateFleetName",
				"gse:UpdateFleetPortSettings",
				"gse:UpdateFleetVpc",
				"gse:UpdateRuntimeConfiguration"
            ],
            "resource": "qcs::gse::uin/110702656:fleet/*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

ユーザーに例えばアカウント番号110702656の特定フリート（FleetId=fleet-28a9refi-ur5pe34j）の操作権限を持たせたい場合は、ポリシーの resource を次のとおり修正することができます：

```
qcs::gse::uin/110702656:fleet/fleet-28a9refi-ur5pe34j
```

### GSEゲームサーバーセッションキューリソースポリシー

ユーザーにアカウント番号110702656のすべてのゲームサーバーセッションキューの操作権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                            | 説明                                                 |
| ------------------------------- | ---------------------------------------------------- |
| DeleteGameServerSessionQueue    | ゲームサーバーセッションキューを新たに削除                             |
| StartGameServerSessionPlacement | ゲームサーバーセッション配置リクエストのゲームサーバーセッションキューへの送信を開始 |
| UpdateGameServerSessionQueue    | ゲームサーバーセッションキューの属性の更新                         |


具体的な操作手順は次のとおりです：

1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、アカウント番号110702656のすべてのゲームサーバーセッションキューの操作権限を持つカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:DeleteGameServerSessionQueue",
                "gse:StartGameServerSessionPlacement",
                "gse:UpdateGameServerSessionQueue"
            ],
            "resource": "qcs::gse::uin/110702656:gameServerSessionQueue/*",
            "effect": "allow"
        }
    ]
}
```

2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

ユーザーにアカウント番号110702656の特定のゲームサーバーセッションキュー（StartGameServerSessionPlacementエントリーでは、GameServerSessionQueueName=queue-ciu3c0de-c09dk3do；またはDeleteGameServerSessionQueue/UpdateGameServerSessionQueueエントリーでは、Name=queue-ciu3c0de-c09dk3do）の操作権限を持たせたい場合は、ポリシーの resource を次のとおり修正することができます：

```
qcs::gse::uin/110702656:gameServerSessionQueue/queue-ciu3c0de-c09dk3do
```

### デモ権限ポリシー

ユーザーにデモの操作権限を持たせたい場合は、ポリシーに次の操作を追加してから、そのポリシーをユーザーに関連付けることができます。

| 名称                       | 説明                           |
| -------------------------- | ------------------------------ |
| CreateAssetAuto            | アセットの自動作成                 |
| CreateFleetDemo            | フリートデモの作成                   |
| CreateGameServerSession    | ゲームサーバーセッションの作成             |
| DescribeFleetAttributes    | フリートの通常属性（ステータスを含む）の検索 |
| DescribeGameServerSessions | ゲームセッションリストのクエリー              |
| DescribeDemoResource       | サービスデプロイのデモリソース属性の検索         |
| JoinGameServerSession      | ゲームサーバーセッションへの参加             |
| UpdateDemoResource           | サービスデプロイデモのソース属性の変更           |

具体的な操作手順は次のとおりです：
1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づき、デモを操作するためのカスタムポリシーを作成します。次のポリシー構文を参考に設定することができます：

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "gse:CreateAssetAuto",
                "gse:UpdateDemoResource",
                "gse:CreateFleetDemo",
                "gse:DescribeDemoResource",
                "gse:DescribeFleetAttributes",
                "gse:DescribeGameServerSessions",
                "gse:CreateGameServerSession",
                "gse:JoinGameServerSession"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列の**ユーザー/グループの関連付け**をクリックします。
3. ポップアップした「ユーザー/ユーザーグループの関連付け」ウィンドウにおいて、承認する必要があるユーザー/グループを選択し、**OK**をクリックします。

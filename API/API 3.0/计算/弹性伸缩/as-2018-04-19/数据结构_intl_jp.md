## Activity

条件を満たすスケーリングイベントの関連情報。

以下のAPIによって参照されます：DescribeAutoScalingActivities。

| 名称 | タイプ |  説明 |
|------|------|-------|
| AutoScalingGroupId | string | スケーリンググループID。 |
| ActivityId | String | スケーリングイベントID。 |
| ActivityType | String | スケーリングイベントタイプ。値は以下のとおりです：<br><br/><li>SCALE_OUT：拡張イベント<li>SCALE_IN：圧縮イベント<li>ATTACH_INSTANCES：インスタンス追加<li>REMOVE_INSTANCES：インスタンス終了<li>DETACH_INSTANCES：インスタンス除去<li>TERMINATE_INSTANCES_UNEXPECTEDLY：インスタンスがCVMコンソールで終了されました<li>REPLACE_UNHEALTHY_INSTANCE：非正常性インスタンスの置き換え） |
| StatusCode | String | スケーリングイベントのステータス。値は以下のとおりです：<br><br/><li>INIT：初期化中<br/><li>RUNNING：実行中<br/><li>SUCCESSFUL：イベント成功<br/><li>PARTIALLY_SUCCESSFUL：一部のイベント成功<br/><li>FAILED：イベント失敗<br/><li>CANCELLED：イベントキャンセル |
| StatusMessage | String | スケーリングイベントのステータス説明。 |
| Cause | String | スケーリングイベントの原因。 |
| Description | String | スケーリングイベントの説明。 |
| StartTime | Timestamp | スケーリングイベントの開始時間。 |
| EndTime | Timestamp | スケーリングイベントの終了時間。 |
| CreatedTime | Timestamp | スケーリングイベントの作成時間。 |
| ActivityRelatedInstanceSet | Array of [ActivtyRelatedInstance](#ActivtyRelatedInstance) | スケーリングイベントの関連インスタンス情報セット。 |
| StatusMessageSimplified | String | スケーリングイベントのステータス概要。 |

## ActivtyRelatedInstance

今回のスケーリングイベントの関連インスタンス情報。

以下のAPIによって参照されます：DescribeAutoScalingActivities。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | インスタンスID。 |
| InstanceStatus | String | スケーリングイベントでのインスタンスのステータス。値は以下のとおりです：<br/><li>SUCCESSFUL：イベント成功<br/><li>FAILED：イベント失敗 |

## AutoScalingGroup

スケーリンググループ

以下のAPIによって参照されます：DescribeAutoScalingGroups。

| 名称 | タイプ |  説明 |
|------|------|-------|
| AutoScalingGroupId | string | スケーリンググループID |
| AutoScalingGroupName | string | スケーリンググループ名称 |
| AutoScalingGroupStatus | string | スケーリンググループのステータス |
| CreatedTime | Timestamp | 作成時間、UTC標準時間を使用します |
| DefaultCooldown | Integer | デフォルトクールダウン、単位が秒です |
| DesiredCapacity | Integer | 希望インスタンス数 |
| EnabledStatus | String | 有効状態、値には`ENABLED`と`DISABLED`を含みます |
| ForwardLoadBalancerSet | Array of [ForwardLoadBalancer](#ForwardLoadBalancer) | アプリケーション型CLB装置リスト |
| InstanceCount | Integer | インスタンス数量 |
| InServiceInstanceCount | Integer | 状態は`IN_SERVICE`インスタンス数量 |
| LaunchConfigurationId | String | 起動構成ID |
| LaunchConfigurationName | String | 起動構成名称 |
| LoadBalancerIdSet | Array of String | 従来型CLB装置IDリスト |
| MaxSize | Integer | 最大インスタンス数 |
| MinSize | Integer | 最小インスタンス数 |
| ProjectId | Integer | プロジェクトID |
| SubnetIdSet | Array of String | サブネットIDリスト |
| TerminationPolicySet | Array of String | 終了ポリシー |
| VpcId | String | VPCタグ |
| ZoneSet | Array of String | Availability Zoneリスト |
| RetryPolicy | String | 再試行ポリシー |

## AutoScalingGroupAbstract

スケーリンググループの概要。

以下のAPIによって参照されます：DescribeLaunchConfigurations。

| 名称 | タイプ |  説明 |
|------|------|-------|
| AutoScalingGroupId | string | スケーリンググループID。 |
| AutoScalingGroupName | string | スケーリンググループ名称。 |

## DataDisk

構成されたデータディスク構成情報を起動します。このパラメータを指定しないと、デフォルトでデータディスクを購入しません。現時点では、購入するとき1つのみのデータディスクを指定することをサポートします。

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| DiskType | String | いいえ | データディスクタイプ。データディスクタイプの制限については、[CVMインスタンス構成](https://cloud.tencent.com/document/product/213/2177)を参照してください。値範囲：<br><li>LOCAL_BASIC：ローカルディスク<br><li>LOCAL_SSD：ローカルSSDディスク<br><li>CLOUD_BASIC：HDD Cloud Storage<br><li>CLOUD_PREMIUM：Premium Cloud Storage<br><li>CLOUD_SSD：SSD Cloud Storage<br><br>デフォルト値：LOCAL_BASIC。 |
| DiskSize | Integer | いいえ | データディストサイズ、单位：GB。最小調整ステップサイズは10Gです。データディストのタイプによって値範囲が異なります。具体的には、[CVMインスタンス構成](https://cloud.tencent.com/document/product/213/2177)を参照してください。デフォルト値は0で、データディスを購入しないと示します。更なる制限については、製品ドキュメントを参照てください。 |
| SnapshotId | String | いいえ | データディスクのスナップショットID、`snap-l8psqwnt`と似ています。 |

## EnhancedService

クラウドセキュリティ、CMなどのインスタンスAgentのような設定、およびインスタンス拡張サービス起動状況について説明します。

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | いいえ | クラウドセキュリティサービスを起動します。このパラメータを指定しないと、デフォルトでクラウドセキュリティサービスを起動します。 |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | いいえ | CMサービスを起動します。このパラメータを指定しないと、デフォルトでCMサービスを起動します。 |

## Filter

>条件付きフィルタリング照合用のキー値ペアのフィルタについて説明します。例えば、フィルタリングID、名称、ステータスなど
> * 複数の`Filter`が存在する場合、`Filter`間の関係は論理積（`AND`）関係です。
> * 同一`Filter`には複数の`Values`が存在する場合、同一`Filter`下の`Values`間の関係は論理和（`OR`）関係です。
>
> [DescribeInstances](https://cloud.tencent.com/document/api/213/9388) APIの`Filter`を例として、照合するAvailability Zone（`zone`）が広州1区 ***且つ*** インスタンス課金モード（`instance-charge-type`）は年額/月額 ***または*** 従量制課金のインスタンスの場合、以下のように実現することができます：
```
Filters.1.Name=zone
&Filters.1.Values.1=ap-guangzhou-1
&Filters.2.Name=instance-charge-type
&Filters.2.Values.1=PREPAID
&Filters.3.Values.2=POSTPAID_BY_HOUR
```

以下のAPIによって参照されます：DescribeAutoScalingActivities、DescribeAutoScalingGroups、DescribeAutoScalingInstances、DescribeLaunchConfigurations、DescribeScheduledActions。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Name | String | はい | フィルタリングが必要なフィールド。 |
| Values | Array of String | はい | フィールドのフィルタリング値。 |

## ForwardLoadBalancer

アプリケーション型CLB装置

以下のAPIによって参照されます：CreateAutoScalingGroup、DescribeAutoScalingGroups、ModifyLoadBalancers。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| LoadBalancerId | String | はい | CLB装置ID |
| ListenerId | String | はい | アプリケーション型CLBリスナーID |
| TargetAttributes | Array of [TargetAttribute](#TargetAttribute) | はい | 目標規則属性リスト |
| LocationId | String | いいえ | 転送規則ID |

## Instance

インスタンス情報

以下のAPIによって参照されます：DescribeAutoScalingInstances。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | インスタンスID |
| AutoScalingGroupId | string | スケーリンググループID |
| LaunchConfigurationId | String | 起動構成ID |
| LaunchConfigurationName | String | 起動構成名称 |
| LifeCycleState | String | ライフサイクルのステータス、値にはIN_SERVICE、CREATING、TERMINATING、ATTACHING、DETACHING、ATTACHING_LB、DETACHING_LBなどが含まれます |
| HealthStatus | String | 正常性ステータス、値にはHEALTHYとUNHEALTHYが含まれます |
| ProtectedFromScaleIn | Boolean | 圧縮保護の有効化状態 |
| Zone | String | Availability Zone |
| CreationType | String | 作成タイプ、値にはAUTO_CREATION、MANUAL_ATTACHINGが含まれます。 |
| AddTime | Timestamp | インスタンス追加時間 |
| InstanceType | String | インスタンスタイプ |

## InstanceMarketOptionsRequest

CVM入札リクエスト関連オプション

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| SpotOptions | [SpotMarketOptions](#SpotMarketOptions) | はい | 入札関連オプション |
| MarketType | String | いいえ | マーケットオプションタイプ、現時点でサポートする値はspotのみです |

## InternetAccessible

起動構成で作成するインスタンスのパブリックネットワークのアクセス可能性について説明し、インスタンスのパブリックネットワーク使用課金モード、最大帯域幅などを宣言します

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| InternetChargeType | String | いいえ | ネットワーク課金タイプ。値範囲：<br><li>BANDWIDTH_PREPAID：前払いは帯域幅により課金<br><li>TRAFFIC_POSTPAID_BY_HOUR：トラフィックは時間制後払い<br><li>BANDWIDTH_POSTPAID_BY_HOUR：帯域幅は時間制後払い<br><li>BANDWIDTH_PACKAGE：帯域幅パッケージユーザー<br>デフォルト値：TRAFFIC_POSTPAID_BY_HOUR。 |
| InternetMaxBandwidthOut | Integer | いいえ | パブリックネットワークのアウトバウンド帯域幅上限、单位：Mbps。デフォルト値：0Mbps。モデルによって帯域幅の上限範囲が違います。具体的な制限については[ネットワーク帯域幅の購入](https://cloud.tencent.com/document/product/213/509)を参照してください。 |
| PublicIpAssigned | Boolean | いいえ | パブリックネットワークIPを割り当てるかどうか。値範囲：<br><li>TRUE：パブリックネットワークIPの割り当てを示します<br><li>FALSE：パブリックネットワークIPを割り当てらないと示します<br><br>パブリックネットワーク帯域幅が0Mbpsより大きい場合、有効にするかどうか自由に選択できます。パブリックネットワークIPをデフォルトで有効にします。パブリックネットワーク帯域幅が0である場合、パブリックネットワークIPを割り当てはいけません。 |

## LaunchConfiguration

条件を満たす起動構成情報のセット。

以下のAPIによって参照されます：DescribeLaunchConfigurations。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ProjectId | Integer | インスタンス所属プロジェクトID |
| LaunchConfigurationId | String | 起動構成ID。 |
| LaunchConfigurationName | String | 起動構成名称。 |
| InstanceType | String | インスタンスモデル。 |
| SystemDisk | [SystemDisk](#SystemDisk) | インスタンスシステムディスク構成情報。 |
| DataDisks | Array of [DataDisk](#DataDisk) | インスタンスデータディスク構成情報。|
| LoginSettings | [LimitedLoginSettings](#LimitedLoginSettings) | インスタンスログイン設定。 |
| InternetAccessible | [InternetAccessible](#InternetAccessible) | パブリックネットワーク帯域幅の関連情報設定。 |
| SecurityGroupIds | Array of String | インスタンス所属セキュリティグループ。 |
| AutoScalingGroupAbstractSet | Array of [AutoScalingGroupAbstract](#AutoScalingGroupAbstract) | 起動構成関連スケーリンググループ。 |
| UserData | String | カスタムデータ。 |
| CreatedTime | Timestamp | 起動構成の作成時間。 |
| EnhancedService | [EnhancedService](#EnhancedService) | インスタンス拡張サービス起動状況とその設定。 |
| ImageId | String | イメージID。 |
| LaunchConfigurationStatus | String | 起動構成の現在のステータス。値範囲：<br><li>NORMAL：正常<br><li>IMAGE_ABNORMAL：起動構成イメージ異常<br><li>CBS_SNAP_ABNORMAL：起動構成データディスクスナップショット異常<br><li>SECURITY_GROUP_ABNORMAL：起動構成セキュリティグループ異常<br> |
| InstanceChargeType | String | インスタンス課金タイプ、CVMのデフォルト値はPOSTPAID_BY_HOURによって処理します。<br/><br><li>POSTPAID_BY_HOUR：時間性後払い<br/><br><li>SPOTPAID：入札支払 |
| InstanceMarketOptions | [InstanceMarketOptionsRequest](#InstanceMarketOptionsRequest) | インスタンスマーケット関連オプション、入札インスタンスに関するパラメータを例として、指定したインスタンスの支払モードは入札支払であれば、このパラメータを転送する必要があります。 |
| InstanceTypes | Array of String | インスタンスモデルリスト。 |

## LimitedLoginSettings

インスタンスログインの関連構成および情報を説明します。セキュリティ上の理由から、機密性の高い情報を説明しません。

以下のAPIによって参照されます：DescribeLaunchConfigurations。

| 名称 | タイプ |  説明 |
|------|------|-------|
| KeyIds | Array of String | 暗号鍵IDリスト。 |

## LoginSettings

インスタンスログインの関連構成および情報を説明します。

以下のAPIによって参照されます：CreateLaunchConfiguration。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Password | String | いいえ| インスタンスのログインパーワード。オペレーションシステムタイプによってパスワードの複雑レベルが異なります。具体的には以下のとおりです：<br><li>Linuxインスタンスのパスワードは8-16桁で、[a-z，A-Z]、[0-9] と [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]内の特殊記号の中に、少なくとも2つが含まれます。<br><li>Windowsインスタンスのパスワードは12-16桁で、[a-z]、[A-Z]、[0-9] と [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]内の特殊記号の中に、少なくとも3つが含まれます。<br><br>このパラメータを指定しなければ、システムによってランダムにパスワードを生成し、サイト内メッセージでユーザーに通知します。 |
| KeyIds | Array of String | いいえ | 暗号鍵IDリスト。暗号鍵が関連付けられた後は、対応する秘密鍵を介してインスタンスにアクセスできます。KeyIdはAPI DescribeKeyPairsにより取得できます。暗号鍵とパスワードを同時に指定することはできず、同時にWindowsオペレーションシステムは暗号鍵の指定をサポートしません。現時点では購入する場合1つの暗号鍵を指定することのみサポートします。 |
| KeepImageLogin | Boolean | いいえ | イメージの初期設定の維持。このパラメータはPasswordまたはKeyIds.Nと同時に指定されることができません。このパラメーターは、カスタムイメージ、共有イメージ、または外部イメージのインポートでインスタンスを作成する場合のみ、TRUEとして指定できます。値範囲：<br><li>TRUE：イメージのログイン設定を維持すると示します<br><li>FALSE：イメージのログイン設定を維持しないと示します<br><br>デフォルト値：FALSE。 |

## RunMonitorServiceEnabled

「CM」サービスの関連情報を説明します。

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Enabled | Boolean | いいえ | [CM](https://cloud.tencent.com/document/product/248)サービスを有効にするかどうか。値範囲：<br><li>TRUE：CMサービスを有効にすると示します<br><li>FALSE：CMサービスを有効にしないと示します<br><br>デフォルト値：TRUE。 |

## RunSecurityServiceEnabled

「クラウドセキュリティ」サービスの関連情報を説明します

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Enabled | Boolean | いいえ | [クラウドセキュリティ](https://cloud.tencent.com/document/product/296)サービスを有効にするかどうか。値範囲：<br><li>TRUE：クラウドセキュリティサービスを有効にすると示します<br><li>FALSE：クラウドセキュリティサービスを有効にしないと示します<br><br>デフォルト値：TRUE。 |

## ScheduledAction

時限タスクの情報を説明します

以下のAPIによって参照されます：DescribeScheduledActions。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ScheduledActionId | String | 時限タスクID。 |
| ScheduledActionName | String | 時限タスク名称。 |
| AutoScalingGroupId | String | 時限タスクの所属スケーリンググループID。 |
| StartTime | Timestamp | 時限タスクの開始時間。値は`北京時間`（UTC+8）、`ISO8601`標準に従って、フォーマット：`YYYY-MM-DDThh:mm:ss+08:00`。 |
| Recurrence | String | 時限タスクの繰り返し方式。 |
| EndTime | Timestamp | 時限タスクの終了時間。値は`北京時間`（UTC+8）、`ISO8601`標準に従って、フォーマット：`YYYY-MM-DDThh:mm:ss+08:00`。 |
| MaxSize | Integer | 時限タスクが設定した最大インスタンス数。 |
| DesiredCapacity | Integer | 時限タスクが設定した希望インスタンス数。 |
| MinSize | Integer | 時限タスクが設定した最小インスタンス数。 |
| CreatedTime | Timestamp | 時限タスクの作成時間。値は`UTC`時間、`ISO8601`標準に従って、フォーマット：`YYYY-MM-DDThh:mm:ssZ`。 |

## SpotMarketOptions

入札関連オプション

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| MaxPrice | String | はい | 入札価格、例えば「1.05」 |
| SpotInstanceType | String | いいえ | 入札リクエストタイプ、現時点でサポートするタイプはone-timeのみです。デフォルト値はone-timeです |

## SystemDisk

起動構成のシステムディスク構成情報。このパラメータを指定しないと、システムのデフォルト値に従って割り当てられます。

以下のAPIによって参照されます：CreateLaunchConfiguration、DescribeLaunchConfigurations。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| DiskType | String | いいえ | システムディスクタイプ。システムディスクタイプの制限については、[CVMインスタンス構成](https://cloud.tencent.com/document/product/213/2177)を参照してください。値範囲：<br><li>LOCAL_BASIC：ローカルディスク<br><li>LOCAL_SSD：ローカルSSDディスク<br><li>CLOUD_BASIC：HDD Cloud Storage<br><li>CLOUD_PREMIUM：Premium Cloud Storage<br><li>CLOUD_SSD：SSD Cloud Storage<br><br>デフォルト値：LOCAL_BASIC。 |
| DiskSize | Integer | いいえ | システムディスクサイズ、単位：GB。デフォルト値は50です |

## TargetAttribute

CLB装置目標属性

以下のAPIによって参照されます：CreateAutoScalingGroup、DescribeAutoScalingGroups、ModifyLoadBalancers。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Port | Integer | はい | ポート |
| Weight | Integer | はい | 重み付け |



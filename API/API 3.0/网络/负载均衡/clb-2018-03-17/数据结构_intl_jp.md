## Backend

リスナーのバックエンドにバインディングされるマシンの詳細情報

次のAPIによって参照されます：DescribeTargets。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Type | String | 転送先のタイプであり、現在、値はCVMのみ可能です |
| InstanceId | String | CVMの一意IDであり、DescribeInstances APIでフィールド中のunInstanceIdフィールドを返すことにより取得可能です |
| Port | Integer | バックエンドCVMのリスニングポート |
| Weight | Integer | バックエンドCVMの転送重みであり、値の範囲は0～100で、デフォルトは10です。 |
| PublicIpAddresses | Array of String | CVMのパブリックネットワークIP<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| PrivateIpAddresses | Array of String | CVMのプライベートネットワークIP<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| InstanceName | String | CVMインスタンス名<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。|
| RegisteredTime | String | CVMがリスナーにバインディングされる時間<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## CertificateInput

証明書情報

次のAPIによって参照されます：CreateListener、CreateRule、ModifyListener。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| SSLMode | String | はい | 認証タイプであり、UNIDIRECTIONALは一方向認証、MUTUALは双方向認証です |
| CertId | String | いいえ | サーバー証明書のIDであり、この項目を入力しない場合は証明書をアップロードしなければならず、CertContent、CertKey、CertNameを含みます。 |
| CertCaId | String |いいえ | クライアント証明書のIDです。SSLMode=mutualの場合、リスナーでこの項目を入力しないとクライアント証明書をアップロードしなければならず、CertCaContent、CertCaNameを含みます。 |
| CertName | String | いいえ | アップロードするサーバー証明書の名称であり、CertIdがない場合、この項目を送信する必要があります。 |
| CertKey | String | いいえ | アップロードするサーバー証明書のkeyであり、CertIdがない場合、この項目を送信する必要があります。 |
| CertContent | String | いいえ | アップロードするサーバー証明書の内容であり、CertIdがない場合、この項目を送信する必要があります。 |
| CertCaName | String | いいえ | アップロードするクライアントCA証明書の名称です。SSLMode=mutualでCertCaIdがない場合、この項目を送信する必要があります。 |
| CertCaContent | String | いいえ | アップロードするクライアント証明書の内容です。SSLMode=mutualでCertCaIdがない場合、この項目を送信する必要があります。 |

## CertificateOutput

証明書関連情報

次のAPIによって参照されます：DescribeListeners。

| 名称 | タイプ |  説明 |
|------|------|-------|
| SSLMode | String | 認証タイプであり、unidirectionalは一方向認証、mutualは双方向認証です |
| CertId | String | サーバー証明書のID。 |
| CertCaId | String | クライアント証明書のID。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。|

## ClassicalHealth

従来型CLBの正常性情報

次のAPIによって参照されます：DescribeClassicalLBHealthStatus。

| 名称 | タイプ |  説明 |
|------|------|-------|
| IP | String | CVMプライベートネットワークIP |
| Port | Integer | CVMポート |
| ListenerPort | Integer | CLBリスニングポート |
| Protocol | String | 転送プロトコル |
| HealthStatus | Integer | 正常性検査の結果であり、1は正常、0は異常を表します |

## ClassicalListener

従来型CLBのリスナー情報

次のAPIによって参照されます：DescribeClassicalLBListeners。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ListenerId | String | CLBリスナーID |
| ListenerPort | Integer | CLBリスナーポート |
| InstancePort | Integer | リスナーバックエンド転送ポート |
| ListenerName | String | リスナー名 |
| Protocol | String | リスナーのプロトコルタイプ |
| SessionExpire | Integer | セッション保留時間 |
| HealthSwitch | Integer | 検査を有効化したかということであり、1（有効化）、0（無効化）です |
| TimeOut | Integer | 応答のタイムアウト時間 |
| IntervalTime | Integer | 検査間隔 |
| HealthNum | Integer | 正常しきい値 |
| UnhealthNum | Integer | 異常しきい値 |
| HttpHash | String | パブリックネットワーク固定IP型のHTTP、HTTPSプロトコルリスナーのラウンドロビン方法。wrrは重み付きラウンドロビンを表し、ip_hashはアクセスのソースIPに基づきコンシステントハッシュ法により分配することを表します |
| HttpCode | Integer | パブリックネットワーク固定IP型のHTTP、HTTPSプロトコルリスナーの正常性検査戻り値。詳細はリスナーを作成する時にこのフィールドに対する説明を参照することができます |
| HttpCheckPath | String | パブリックネットワーク固定IP型のHTTP、HTTPSプロトコルリスナーの正常性検査パス |
| SSLMode | String | パブリックネットワーク固定IP型のHTTPSプロトコルリスナーの認証方式 |
| CertId | String | パブリックネットワーク固定IP型のHTTPSプロトコルリスナーのサーバー証明書ID |
| CertCaId | String | パブリックネットワーク固定IP型のHTTPSプロトコルリスナーのクライアント証明書ID |
| Status | Integer | リスナーのステータスであり、0は作成中、1は動作中を表します |

## ClassicalLoadBalancerInfo

CLB情報

次のAPIによって参照されます：DescribeClassicalLBByInstanceId。

| 名称 | タイプ |  説明 |
|------|------|-------|
| InstanceId | String | バックエンドインスタンスID|
| LoadBalancerIds | Array of String | ロードバランサーインスタンスIDリスト<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## ClassicalTarget

従来型CLBバックエンド情報

次のAPIによって参照されます：DescribeClassicalLBTargets。

| 名称 | タイプ |  説明 |
|------|------|-------|
| Type | String | 転送先のタイプであり、現在、値はCVMのみ可能です |
| InstanceId | String | CVMの一意IDであり、DescribeInstances APIでフィールド中のunInstanceIdフィールドを返すことにより取得可能です |
| Weight | Integer | バックエンドCVMの転送重みであり、値の範囲は0～100で、デフォルトは10です。 |
| PublicIpAddresses | Array of String | CVMのパブリックネットワークIP<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| PrivateIpAddresses | Array of String | CVMのプライベートネットワークIP<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| InstanceName | String | CVMインスタンス名<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。|
| RunFlag | Integer | CVMのステータス。<br/>1：故障、2：実行中、3：作成中、4：終了、5：払い戻し済み、6：払い戻し中、7：再起動中、8：スタートアップ中、9：シャットダウン中、10：パスワードリセット中、11：フォーマット化中、12：イメージ作成中、13：帯域幅設定中、14：システムの再インストール中、19：アップグレード中、21：ホットマイグレーション中。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## ClassicalTargetInfo

従来型バックエンド情報

次のAPIによって参照されます：RegisterTargetsWithClassicalLB。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| InstanceId | String | はい | バックエンドインスタンスID |
| Weight | Integer | いいえ | 重み付けであり、値は0～100です |

## HealthCheck

正常性検査情報

次のAPIによって参照されます：CreateListener、CreateRule、DescribeListeners、ModifyListener、ModifyRule。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| HealthSwitch | Integer | いいえ | 正常性検査を有効化するかということであり、1（有効化）、0（無効化）です。 |
| TimeOut | Integer | いいえ | 正常性検査の応答タイムアウト時間。選択可能な値は2～60、デフォルト値は2で、単位は秒です。応答のタイムアウト時間は検査間隔より短い必要があります。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| IntervalTime | Integer | いいえ | 正常性検査の検出間隔。デフォルト値は5、選択可能な値は5～300で、単位は秒です。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HealthNum | Integer | いいえ | 正常しきい値。デフォルト値は3で、連続3回正常であることを検出すると、転送が正常であることを表します。選択可能な値は2～10で、単位は回です。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| UnHealthNum | Integer | いいえ | 異常しきい値。デフォルト値は3で、連続3回異常であることを検出すると、転送が異常であることを表します。選択可能な値は2～10で、単位は回です。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HttpCode | Integer | いいえ | 正常性検査状態コード（HTTP/HTTPS転送規則にのみ適用）。選択可能な値は1～31、デフォルト値は31です。<br/>1は検出後の戻り値が1xxなら正常であることを表します。2は戻り値が2xxなら正常であることを表し、4は戻り値が3xxなら正常であることを表し、8は戻り値が4xxなら正常であることを表し、16は戻り値が5xxなら正常であることを表します。さらに多くのコードで正常状態を表すことが望ましい場合、対応する値を追加します。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HttpCheckPath | String | いいえ | 正常性検査パス（HTTP/HTTPS転送規則にのみ適用）。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HttpCheckDomain | String | いいえ | 正常性検査ドメイン名（HTTP/HTTPS転送規則にのみ適用）。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HttpCheckPath | String | いいえ | 正常性検査方法（HTTP/HTTPS転送規則にのみ適用）。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## Listener

リスナーの情報

次のAPIによって参照されます：DescribeListeners。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ListenerId | String | アプリケーション型CLBリスナーID |
| Protocol | String | リスナーのプロトコル |
| Port | Integer | リスナーのポート |
| Certificate | [CertificateOutput](#CertificateOutput) | リスナーにバインディングされる証明書の情報<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| HealthCheck | [HealthCheck](#HealthCheck) | リスナーの正常性検査情報<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Scheduler | String | リクエストのスケジューリング方式<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| SessionExpireTime | Integer | セッション保留時間<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| SniSwitch | Integer | SNI特性を有効化するか（このパラメータはHTTPSリスナーに対してのみ有効）<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Rules | Array of [RuleOutput](#RuleOutput) | リスナー下のすべての転送規則（このパラメータはHTTP/HTTPSリスナーに対してのみ有効）<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| ListenerName | String | リスナー名<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## ListenerBackend

リスナーに登録されたRSの情報

次のAPIによって参照されます：DescribeTargets。

| 名称 | タイプ |  説明 |
|------|------|-------|
| ListenerId | String | リスナーID |
| Protocol | String | リスナーのプロトコル |
| Port | Integer | リスナーのポート |
| Rules | Array of [RuleTargets](#RuleTargets) | リスナー下の規則情報（HTTP/HTTPSリスナーに対してのみ適用）<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Targets | Array of [Backend](#Backend) | リスナーに登録されたマシンリスト（TCP/UDP/TCP_SSLリスナーに対してのみ適用）<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## LoadBalancer

ロードバランサーインスタンスの情報

次のAPIによって参照されます：DescribeLoadBalancers。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| LoadBalancerId | String | いいえ | ロードバランサーインスタンスID。 |
| LoadBalancerName | String | いいえ | ロードバランサーインスタンス名。 |
| LoadBalancerType | String | いいえ | ロードバランサーインスタンスのネットワークタイプ。<br/>OPEN：パブリックネットワーク属性、INTERNAL：プライベートネットワーク属性。 |
| Forward | Integer | いいえ | アプリケーション型CLBタグであり、1はアプリケーション型CLB、0は従来型CLBです。 |
| Domain | String | いいえ | ロードバランサーインスタンスのドメイン名であり、プライベートネットワークタイプのCLBおよびアプリケーション型ロードバランサーインスタンスはこのフィールドを提供しません。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| LoadBalancerVips | Array of String | いいえ | ロードバランサーインスタンスのVIPリスト。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Status | Integer | いいえ | ロードバランサーインスタンスのステータスであり、<br/>0：作成中、1：正常に実行を含みます。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| CreateTime | String | いいえ | ロードバランサーインスタンスの作成時間。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| StatusTime | String | いいえ | ロードバランサーインスタンスの前回のステータス変換時間。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| ProjectId | Integer | いいえ | ロードバランサーインスタンスが所属するプロジェクトIDであり、0はデフォルトのプロジェクトを表します。 |
| VpcId | String | いいえ | VPCのID<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| OpenBgp | Integer | いいえ | Anti-DDoS LBのタグであり、1はAnti-DDoS CLB、0は非Anti-DDoS CLBです。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Snat | Boolean | いいえ | 2016年12月以前の従来型プライベートネットワークCLBでは、すべてsnatが有効になっています。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Isolation | Integer | いいえ | 0：隔離されていない、1：隔離されている。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Log | String | いいえ | ユーザーのログ有効化情報。パブリックネットワーク属性でHTTP、HTTPSリスナーを作成したCLBのみがログを持ちます。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| SubnetId | String | いいえ | ロードバランサーインスタンスが所在するサブネット（プライベートネットワークVPC型LBに対してのみ有効）<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## RuleInput

HTTP/HTTPS転送規則（入力）

次のAPIによって参照されます：CreateRule。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| Domain | String | はい | 転送規則のドメイン名。 |
| Url | String | はい | 転送規則のパス。 |
| SessionExpireTime | Integer | いいえ | セッション保留時間 |
| HealthCheck | [HealthCheck](#HealthCheck) | いいえ | 正常性検査情報 |
| Certificate | [CertificateInput](#CertificateInput) | いいえ | 証明書情報 |
| Scheduler | String | いいえ | 規則のリクエスト転送方式 |

## RuleOutput

HTTP/HTTPS転送規則（出力）

次のAPIによって参照されます：DescribeListeners。

| 名称 | タイプ |  説明 |
|------|------|-------|
| LocationId | String | 転送規則のIDであり、入力時にこのフィールドは必要ではありません |
| Domain | String | 転送規則のドメイン名。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Url | String | 転送規則のパス。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| SessionExpireTime | Integer | セッション保留時間 |
| HealthCheck | [HealthCheck](#HealthCheck) | 正常性検査情報<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Certificate | [CertificateOutput](#CertificateOutput) | 証明書情報<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Scheduler | String | 規則のリクエスト転送方式 |

## RuleTargets

HTTP/HTTPSリスナー下の転送規則のマシンバインディング情報

次のAPIによって参照されます：DescribeTargets。

| 名称 | タイプ |  説明 |
|------|------|-------|
| LocationId | String | 転送規則のID |
| Domain | String | 転送規則のドメイン名 |
| Url | String | 転送規則のパス。 |
| Targets | Array of [Backend](#Backend) | RSの情報<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |

## Target

転送先であり、すなわちCLBにバインディングされるRSです

次のAPIによって参照されます：DeregisterTargets、ModifyTargetPort、ModifyTargetWeight、RegisterTargets。

| 名称 | タイプ | 必須項目 | 説明 |
|------|------|----------|------|
| InstanceId | String | 是 | CVMの一意のIDであり、DescribeInstances APIでフィールド中のunInstanceIdフィールドを返すことにより取得可能です<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Port | Integer | はい | バックエンドCVMの監視ポート<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Url | String いいえ| 転送先のタイプであり、現在は値がCVMのみ可能。<br/>注意：このフィールドはnullを返す可能性があり、有効値を取得できないことを表します。 |
| Weight | Integer | いいえ | バックエンドCVMの転送重みであり、値の範囲は0～100で、デフォルトは10です。 |



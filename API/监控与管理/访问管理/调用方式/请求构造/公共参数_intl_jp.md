完全なTencent Cloud APIリクエストには、共通リクエストパラメータとAPIリクエストパラメータの2種類のリクエストパラメータが必要です。この文章では、Tencent Cloud APIリクエストに必要な6つの共通リクエストパラメータについて説明します。APIリクエストパラメータの詳細については、「APIリクエストパラメータ」の章を参照してください。
共通リクエストパラメータは、各APIに必要なリクエストパラメータです。開発者はTencent Cloud APIを使用してリクエストを送信するたびにこれらの共通リクエストパラメータも送信する必要があります。そうしないと、リクエストは失敗します。APIリクエストパラメータと異なって、共通リクエストパラメータの最初の文字は大文字です。

共通リクエストパラメータの具体的なリスとは以下の通りです：

|パラメータ名   | 必須項目  |  タイプ | 説明  |
| ------------ | ------------ | ------------ | ------------ |
| Action |  はい | String |  具体的な操作の命令APIの名前、例えば、統合身元の一時的認証情報APIを呼び出したい場合は、GetFederationTokenです。 |
| Region  |  いいえ | String  |  地域パラメータは、どの地域のSTSサービスを呼び出したいかを識別するために使用されます。注：1. 現在、ap-guangzhouとap-shanghaiのみが公開されており、他の地域はまだ内部テスト中です；2. デフォルトはap-guangzhouです。|
|  Timestamp | はい  | UInt  | 現在のUNIXタイムスタンプ。APIリクエストの送信時間を記録可能。  |
|  Nonce | はい  |  UInt | ランダムな正の整数。リプレイ攻撃を防ぐために、Timestampと組み合わせて使用。 |
| SecretId  | はい  |  String |  [クラウドAPI暗号鍵](https://console.cloud.tencent.com/capi)で申請された身元を識別するためのSecretId。1つのSecretIdが唯一のSecretKeyに対応し、SecretKeyがリクエストの署名Signatureを生成するために使用されます。詳細については、[署名方法](https://cloud.tencent.com/document/api/377/4214)の章を参照してください。　|
|  Signature |  はい |  String |  リクエストの署名。このリクエストの正当性を検証するために使用され、ユーザーは実際の入力パラメーターに基づいて計算する必要があります。計算方法については、[署名方法](https://cloud.tencent.com/document/api/377/4214)の章を参照してください。　|
|  SignatureMethod | はい  | String  | 署名方法。現在HmacSHA256とHmacSHA1をサポートします。このパラメータがHmacSHA256と指定されている場合にのみ、HmacSHA256アルゴリズムを使用して署名を検証します。それ以外の場合は、HmacSHA1を使用して署名を検証します。署名の計算方法については、[署名方法](https://cloud.tencent.com/document/api/377/4214)のページを参照してください。　　|


**使用例**

Tencent Cloudの各クラウド製品APIリクエストリンクでは、共通リクエストパラメータは次の通りです。Tencent Cloud CVMを例として、ユーザーが広州地域のCVMインスタンスのリストを照合したい場合、リクエストリンクは次の形式になります。
```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<APIリクエストパラメータ>
```


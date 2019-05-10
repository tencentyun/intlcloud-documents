

完全なTencent Cloud APIリクエストには、共通リクエストパラメータとAPIリクエストパラメータの2種類のリクエストパラメータが必要です。この文章では、Tencent Cloud APIリクエストに必要な6つの共通リクエストパラメータについて説明します。APIリクエストパラメータの詳細については、[APIリクエストパラメータ](https://cloud.tencent.com/document/product/1014/31225)の章を参照してください。
共通リクエストパラメータは、各APIに必要なリクエストパラメータです。開発者はTencent Cloud APIを使用してリクエストを送信するたびにこれらの共通リクエストパラメータも送信する必要があります。そうしないと、リクエストは失敗します。APIリクエストパラメータと異なって、共通リクエストパラメータの最初の文字は大文字です。

共通リクエストパラメータの具体的なリスとは以下の通りです：
>**注意：**
>文章に記載されているAPIインスタンスはTencent Cloud CVMを例として挙げられますが、各Tencent Cloud製品の具体的な使用方法については、実際の製品を参照してください。

| パラメータ名 |  説明 |タイプ |必須|
|---------|---------|---------|---------|
| Action | 具体的な操作の命令API名。例えば、Tencent Cloud CVMユーザーが[インスタンスリストの照合](https://cloud.tencent.com/document/api/213/9388) APIを呼び出すと、ActionパラメータがDescribeInstancesとなります。 | String |はい|
| Region | 地域パラメータ。操作したい地域を識別するためのインスタンス。詳細な情報については、[地域とAvailability Zone](https://cloud.tencent.com/document/product/213/6091)リストを参照するか、[地域リストの照合](https://cloud.tencent.com/document/api/213/9456) APIを使用して確認してください。<br>**注意：**1. 対応するAPIで説明されない限り、このパラメータが必須です。<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. 一部の区域は現在内部テスト中で、現在は一部のユーザーにしか公開されていません。| String |いいえ|
| Timestamp | 現在のUNIXタイムスタンプ。APIリクエストの送信時間を記録可能。| UInt |はい|
| Nonce | ランダムな正の整数。リプレイ攻撃を防ぐために、Timestampと組み合わせて使用。| UInt |はい|
| SecretId | [クラウドAPI暗号鍵](https://console.cloud.tencent.com/capi)で申請された身元を認識するためのSecretId。1つのSecretIdが唯一のSecretKeyに対応し、SecretKeyがリクエストの署名Signatureを生成するために使用されます。詳細については、[署名方法](https://cloud.tencent.com/document/product/215/1693)の章を参照してください。|String|はい|
| Signature |リクエストの署名。このリクエストの正当性を検証するために使用され、ユーザーは実際の入力パラメータに基づいて計算する必要があります。計算方法については、[署名方法](https://cloud.tencent.com/document/product/215/1693)の章を参照してください。|String|はい|
| SignatureMethod | 署名方法。現在HmacSHA256とHmacSHA1をサポートします。このパラメータがHmacSHA256と指定されている場合にのみ、HmacSHA256アルゴリズムを使用して署名を検証します。それ以外の場合は、HmacSHA1を使用して署名を検証します。詳細な署名の計算方法については、[署名方法](https://cloud.tencent.com/document/product/215/1693)の章を参照してください。|String|いいえ|
| Token | 一時証明書で使用されるToken。一時暗号鍵と一緒に使用する必要があります。長期暗号鍵はTokenを必要としません。|String|いいえ|

### 使用例
Tencent Cloudの各クラウド製品APIリクエストリンクでは、共通リクエストパラメータは次の通りです。Tencent Cloud CVMを例として、ユーザーが広州地域のCVMインスタンスのリストを照合したい場合、リクエストリンクは次の形式になります。

<pre>
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=ap-guangzhou
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature
&SignatureMethod=HmacSHA256
&<APIリクエストパラメータ>
</pre>




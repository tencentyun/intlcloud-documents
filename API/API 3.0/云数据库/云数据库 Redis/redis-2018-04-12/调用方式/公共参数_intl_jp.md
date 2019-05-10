共通パラメータは、ユーザーとインターフェースの認証目的を識別するためのパラメータです。必要ない場合、各インターフェースの個別のインターフェースドキュメントでは、これらのパラメータについて説明しません。ただし、各リクエストはいずれもこれらのパラメータを持っていない限り正常にリクエストを開始することはできません。

## 署名方法 v3

TC3-HMAC-SHA256 による署名方法を使用する場合、共通パラメータは以下のように統一して HTTP Header リクエストヘッドに配置する必要があります。

|パラメータ名|タイプ|選択必須|説明|
|--------|----|----|----|
| X-TC-Action | String | 要 | 操作するインターフェースの名称です。値は、インターフェースドキュメントの入力パラメータの共通パラメータ Action の説明を参照してください。CVM の 照会インスタンスリストのインターフェースの場合、値は DescribeInstances です。|
| X-TC-Region | String | 要 | リージョンパラメータ。どのリージョンのデータを操作したいか識別するために使用します。インターフェースが取得したリージョンの値は、インターフェースドキュメントの入力パラメータの共通パラメータ Region の説明を参照してください。注意：このパラメータを伝達する必要のないインターフェースもあります。これについて、インターフェースドキュメントに特別な説明があります。この場合、このパラメータを伝達しても効力が発生しません。|
| X-TC-Timestamp | Integer | 要 | 現在の UNIX タイムスタンプ。API リクエストを開始する時間を記録できます。例えば、1529223702 のようにします。注意：サーバ時間との差が5分以上ある場合、署名の期限切れエラーが発生します。|
| X-TC-Version | String | 要 | 操作する API のバージョンです。値については、インターフェースドキュメントのパラメータ入力の共通パラメータ Version の説明を参照してください。例えば、CVM のバージョン 2017-03-12 などです。|
| Authorization |String | 要 | HTTP 標準の本人認証ヘッダフィールドです。例：<br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 <br/>そのうち、<br/>- TC3-HMAC-SHA256：署名方法であり、現在一定してこの値を取得します。<br/>- Credential：署名の証明書。AKIDEXAMPLE は SecretId、Date は UTC 標準時間による日時です。値は共通パラメータ X-TC-Timestamp と換算した UTC 標準時間の日時と一致する必要があります。service は製品名です。cvm など、呼び出す製品のドメインンと一致する必要があります。<br/>- SignedHeaders：署名計算に関わるヘッダ情報であり、content-type と host は選択必須のヘッダです。<br/>- Signature：署名の概要です。|
| X-TC-Token|String |不要 | 一時証明書に使用する Token。一時キーと共に使用する必要があります。一時キーと Token は、CAM サービスの呼び出しインターフェースで取得する必要があります。長期的なキーは、Token が必要ありません。|

広州リージョンの CVM インスタンスリストを照会したいと考えた場合、そのリクエスト構造はリクエスト URL、リクエストヘッダ、リクエスト本体に基づき、以下のようになります。

HTTP GET リクエスト構造の例は次の通りです。

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKIDz8krbsJ5yKBZQpn74WFkmLPx3EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

HTTP POST （application/json） リクエスト構造の例は次の通りです（特定のインターフェースのみサポート）。

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: application/json
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

{"Offset":0,"Limit":10}
```

HTTP POST （multipart/form-data）リクエスト構造の例は次の通りです（特定のインターフェースのみサポート）。

```
https://cvm.tencentcloudapi.com/

Authorization: TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/2018-05-30/cvm/tc3_request, SignedHeaders=content-type;host, Signature=582c400e06b5924a6f2b5d7d672d79c15b13162d9279b0855cfba6789a8edb4c
Content-Type: multipart/form-data; boundary=58731222010402
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1527672334
X-TC-Region: ap-guangzhou

--58731222010402
Content-Disposition: form-data; name="Offset"

0
--58731222010402
Content-Disposition: form-data; name="Limit"

10
--58731222010402--
```

## 署名方法 v1

HmacSHA1 と HmacSHA256 による署名方法を使用する場合、共通パラメータは以下のように統一してリクエスト文字列に配置する必要があります。

| パラメータ名 | タイプ | 選択必須 | 説明 |
|:---------|:---------|:-----|:---- |
| Action | String | 要 | 操作するインターフェースの名称。値は、インターフェースドキュメントの入力パラメータの共通パラメータ Action の説明を参照してください。CVM の 照会インスタンスリストのインターフェースの場合、値は DescribeInstances です。|
| Region| String | 要 | リージョンパラメータ。どのリージョンのデータを操作したいか識別するために使用します。インターフェースが取得したリージョンの値は、インターフェースドキュメントの入力パラメータの共通パラメータ Region の説明を参照してください。注意：このパラメータを伝達する必要のないインターフェースもあります。これについて、インターフェースドキュメントに特別な説明があります。この場合、このパラメータを伝達しても効力が発生しません。|
| Timestamp | Integer | 要 | 現在の UNIX タイムスタンプ。API リクエストを開始する時間を記録できます。例えば1529223702のように、現在の時間との差が非常に大きい場合、署名の期限切れエラーが発生します。|
| Nonce | Integer | 要 |ランダムな正の整数。Timestamp と組み合わせてリプレイアタックの防止に使用します。|
| SecretId | String | 要 | <a href="https://console.cloud.tencent.com/capi">クラウドAPIキー</a>で申請する身分を識別する SecretIdです。SecretId は 一意の SecretKey に対応し、SecretKey はリクエスト署名 Signature を生成するために使用します。|
| Signature | String | 要 | 署名リクエスト。このリクエストの合法性を検証するために使用し、ユーザーが実際に入力したパラメータに基づいて算出する必要があります。具体的な計算方法については、インターフェース認証ドキュメントを参照してください。|
| Version | String | 要 | 操作する API のバージョンです。値については、インターフェースドキュメントのパラメータ入力の共通パラメータ Version の説明を参照してください。例えば、CVM のバージョン 2017-03-12 などです。|
| SignatureMethod | String |不要 | 署名方式。現在のところ、 HmacSHA256 と HmacSHA1をサポートしています。このパラメータを HmacSHA256 に指定した時のみ、HmacSHA256 アルゴリズムを使用した署名検証が可能になります。それ以外の状況では HmacSHA1 を使用して署名を認証します。|
| Token | String | 不要 | 一時証明書に使用する Token は、一時キーと共に使用する必要があります。一時キーと Token は、CAM サービスの呼び出しインターフェースで取得する必要があります。長期キーは、Token を使用する必要がありません。|


広州リージョンの CVM インスタンスリストを照会したいと考えた場合、そのリクエスト構造はリクエスト URL、リクエストヘッダ、リクエスト本体に基づき、以下のようになります。

HTTP GET リクエスト構造の例は次の通りです。
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

HTTP POST リクエスト構造の例は次の通りです。

```
https://cvm.tencentcloudapi.com/

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded

Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```


## リージョンリスト

本製品の全てのインターフェース Region フィールドのオプション値を以下の表に示します。インターフェースがこの表の全リージョンをサポートしない場合、インターフェースドキュメントで個別に説明します。


| エリア| 値 |
|------|------|
|アジア太平洋エリア(バンコク)|ap-bangkok|
|華北エリア(北京)|ap-beijing|
|西南エリア(成都)|ap-chengdu|
|西南エリア(重慶)|ap-chongqing|
|華南エリア(広州)|ap-guangzhou|
|東南アジアエリア(中国香港)|ap-hongkong|
|アジア太平洋エリア(ムンバイ)|ap-mumbai|
|アジア太平洋エリア(ソウル)|ap-seoul|
|華東エリア(上海)|ap-shanghai|
|華東エリア(上海金融)|ap-shanghai-fsi|
|華南エリア(深圳金融)|ap-shenzhen-fsi|
|東南アジアエリア(シンガポール)|ap-singapore|
|アジア太平洋エリア(東京)|ap-tokyo|
|欧州エリア(フランクフルト)|eu-frankfurt|
|欧州エリア(モスクワ)|eu-moscow|
|米国東部(ヴァージニア)|na-ashburn|
|米国西部(シリコンバレー)|na-siliconvalley|
|北米エリア(トロント)|na-toronto|


共通パラメータは、ユーザーとAPI認証を識別するために使用されるパラメータで、必要でない場合は、各APIの個別のAPIドキュメントには記載されていませんが、リクエストを正常に開始するためにリクエストごとにこれらのパラメータを渡す必要があります。

## 署名方法 v3

TC3-HMAC-SHA256署名方式を使用する場合は、共通パラメータをHTTP Headerリクエストヘッダーに統一に配置する必要があります。以下のとおりです：

|パラメータ名称|タイプ|必須項目|説明|
|--------|----|----|----|
| X-TC-Action | String | はい | 具体的な操作の命令API名。例えば、CVMのインスタンスリスト照合APIを呼び出す場合は、ActionパラメータはDescribeInstancesです。|
| X-TC-Region | String | はい | 地域パラメータ、どの地域のデータを操作したいのかを識別します。|
| X-TC-Timestamp | Integer | はい | 現在のUNIXタイムスタンプが、APIリクエストの送信時間を記録することができます。例えば、1529223702、現在のAPIサーバーとの時差が5分を超えると、署名の有効期限切れエラーが発生します。|
| X-TC-Version| String | はい | APIのバージョン。例えば2017-03-12。|
| Authorization|String | はい | HTTP標準認証ヘッダーフィールド、例えば：<br/>TC3-HMAC-SHA256 Credential=AKIDEXAMPLE/Date/service/tc3_request, SignedHeaders=content-type;host, Signature=fe5f80f77d5fa3beca038a248ff027d0445342fe2855ddc963176630326f1024 <br/>その中、<br/>- TC3-HMAC-SHA256：署名方法、現在固定的にこの値を取ります；<br/>- Credential：署名クレデンシャル、AKIDEXAMPLEはSecretIdです；DateはUTC標準時間の日付、その値は共通パラメータX-TC-Timestampによって変換されたUTC標準時間の日付と同じである必要があります；serviceは製品名で、呼び出された製品ドメイン名と一致する必要があります。例えばcvm；<br/>- SignedHeaders：署名計算に関わるヘッダー情報、content-typeとhostは必須ヘッダーです；<br/>- Signature：署名概要。|
| X-TC-Token|String |いいえ |一時証明書で使用されるトークン。一時暗号鍵と一緒に使用する必要があります。一時暗号鍵とトークンはCAMサービス呼び出しAPIから取得する必要があります。長期暗号鍵はトークンを必要としません。|

例えばユーザーが広州地域のCVMインスタンスリストを照合したければ、そのリクエスト構造は次のように、リクエストURL、リクエストヘッダー、およびリクエスト本体から構成されています：

HTTP GETリクエスト構造例:

```
https://cvm.tencentcloudapi.com/?Limit=10&Offset=0

Authorization: TC3-HMAC-SHA256 Credential=AKID**********************0123456789EXAMPLE/2018-10-09/cvm/tc3_request, SignedHeaders=content-type;host, Signature=5da7a33f6993f0614b047e5df4582db9e9bf4672ba50567dba16c6ccf174c474
Content-Type: application/x-www-form-urlencoded
Host: cvm.tencentcloudapi.com
X-TC-Action: DescribeInstances
X-TC-Version: 2017-03-12
X-TC-Timestamp: 1539084154
X-TC-Region: ap-guangzhou
```

HTTP POST （application/json） リクエスト構造の例：

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

HTTP POST （multipart/form-data）リクエスト構造の例（特定APIのみ対応）：

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

HmacSHA1とHmacSHA256署名方法を使用する場合は、共通パラメータをリクエスト列に統一に配置する必要があります。以下のとおりです

| パラメータ名称 | タイプ | 必須項目 | 説明 |
|:---------|:---------|:-----|:---- |
| Action | String | はい | 具体的な操作の命令API名。例えば、CVMのインスタンスリスト照合APIを呼び出す場合は、ActionパラメータはDescribeInstancesです。|
| Region| String | はい | 地域パラメータ、どの地域のデータを操作したいのかを識別します。|
| Timestamp | Integer | はい | 現在のUNIXタイムスタンプが、APIリクエストの送信時間を記録することができます。例えば、1529223702、現在との時差が大きい過ぎると、署名の有効期限切れエラーが発生します。|
| Nonce | Integer | はい |ランダムな正の整数。リプレイ攻撃を防ぐために、Timestampと組み合わせて使用。|
| SecretId | String | はい | <a href="https://console.cloud.tencent.com/capi">クラウドAPI暗号鍵</a>で申請された身元を識別するためのSecretId。1つのSecretIdが唯一のSecretKeyに対応し、SecretKeyがリクエストの署名Signatureを生成するために使用されます。|
| Signature | String | はい | リクエスト署名。このリクエストの正当性を検証するために使用され、ユーザーが実際の入力パラメータに基づいて計算する必要があります。具体的な計算方法については、API認証ドキュメントを参照してください。|
| Version | String | はい | API のバージョン。例えば2017-03-12。|
| SignatureMethod | String | いいえ | 署名方式。現在、HmacSHA256とHmacSHA1をサポートします。このパラメータをHmacSHA256に指定した場合のみ、HmacSHA256アルゴリズムで署名を検証します。その他の場合、HmacSHA1で署名を検証します。|
|Token | String |いいえ |一時証明書で使用されるトークン。一時暗号鍵と一緒に使用する必要があります。一時暗号鍵とトークンはCAMサービス呼び出しAPIから取得する必要があります。長期暗号鍵はトークンを必要としません。|


例えばユーザーが広州地域のCVMインスタンスのリストを照合したければ、そのリクエスト構造は次のように、リクエストURL、リクエストヘッダー、およびリクエスト本体から構成されています：

HTTP GETリクエスト構造例:
```
https://cvm.tencentcloudapi.com/?Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded
```

HTTP POST リクエスト構造の例：

```
https://cvm.tencentcloudapi.com/

Host: cvm.tencentcloudapi.com
Content-Type: application/x-www-form-urlencoded

Action=DescribeInstances&Version=2017-03-12&SignatureMethod=HmacSHA256&Timestamp=1527672334&Signature=37ac2f4fde00b0ac9bd9eadeb459b1bbee224158d66e7ae5fcadb70b2d181d02&Region=ap-guangzhou&Nonce=23823223&SecretId=AKIDEXAMPLE
```


## 地域リスト

次のテーブルに、この製品のすべてのAPIのRegionフィールドで利用可能な値を示します。APIがテーブル内のすべての地域をサポートしていない場合は、APIドキュメントで個別に説明されます。


| エリア | 値 |
|------|------|
|アジア太平洋地区（バンコク）|ap-bangkok|
|華北地区（北京）|ap-beijing|
|西南地区（成都）|ap-chengdu|
|西南地区（重慶）|ap-chongqing|
|華南地区（広州）|ap-guangzhou|
|華南地区（広州Open）|ap-guangzhou-open|
|東南アジア地区（中国香港）|ap-hongkong|
|アジア太平洋地区（ムンバイ）|ap-mumbai|
|アジア太平洋地区（ソウル）|ap-seoul|
|華東地区（上海）|ap-shanghai|
|華東地区（上海金融）|ap-shanghai-fsi|
|華南地区（深セン金融）|ap-shenzhen-fsi|
|東南アジア地区（シンガポール）|ap-singapore|
|アジア太平洋地区（東京）|ap-tokyo|
|ヨーロッパ地区（フランクフルト）|eu-frankfurt|
|ヨーロッパ地区（モスクワ）|eu-moscow|
|米国東部（バージニア）|na-ashburn|
|米国西部（シリコンバレー）|na-siliconvalley|
|北米地区（トロント）|na-toronto|


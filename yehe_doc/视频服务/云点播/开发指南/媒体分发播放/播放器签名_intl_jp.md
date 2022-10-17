プレーヤーの署名は、App再生サービスによる端末の再生を承認するために使用されます。下図の手順5に示すとおり、 App再生サービスが端末での再生を承認すると、有効な署名が配布されます。端末では、署名の有効時間内にビデオコンテンツを再生することができます。
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

>! 次のいずれかの状況が発生した場合、アプリ端末で再生するにはプレーヤー署名が必要です。
>- ドメイン名で[Keyリンク不正アクセス防止](https://intl.cloud.tencent.com/document/product/266/33986)を有効にしている場合。
>- default以外の [プレーヤー設定](https://intl.cloud.tencent.com/document/product/266/38296)を使用している場合。
>- [暗号化](https://intl.cloud.tencent.com/document/product/266/38294)したビデオコンテンツを再生する場合。

以下で、プレーヤー署名のパラメータと生成規則について説明します。

## 署名パラメータ

| パラメータ名 | 入力必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| appId |はい| Integer | アカウントappId|
| fileId |はい| String | ドキュメントID|
| currentTimeStamp |はい| Integer | 配布された署名のUnixタイムスタンプ|
| expireTimeStamp | いいえ | Integer | 配付された署名の有効期限のUnixタイムスタンプ、空のままは有効期限内であることを表します |
| pcfg | いいえ | String | 使用される再生の設定名。 defaultの場合は空のままにします|
| urlAccessInfo | いいえ | Object | 再生リンクのリンク不正アクセス防止設定パラメータ、 [UrlAccessInfo タイプ](#p1) |
| drmLicenseInfo | いいえ | Object | 暗号化コンテンツのキー設定パラメータ、 [DrmLicenseInfo タイプ](#p2) |

#### UrlAccessInfoタイプ[](id:p1)

| パラメータ名 | 入力必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| t | いいえ | String | <ul style="margin:0;"><li>16進文字列、リンクの有効期限を表します</li><li>具体的な意味と値については [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) の t パラメータをご参照ください</li><li>空のままは有効期限内であることを表します</li>|
| exper | いいえ | Integer | <ul style="margin:0;"> <li>プレビュー時間、単位は秒、10進法で表示します</li><li>プレビュー時間を指定する場合、時間は30秒未満とする必要があります</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のexperパラメータをご参照ください</li> |
| rlimit | いいえ | Integer |<ul style="margin:0;"><li>異なるIPの端末で許可される最大再生数、10進法で表示します</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のrlimitパラメータをご参照ください</li>|
| us | いいえ |String |<ul style="margin:0;"><li>リンクを一意に識別できるリンクID</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のusパラメータをご参照ください</li>|
| uid | いいえ |String | <ul style="margin:0;"><li>再生者のIDで、16進数の全8桁で表します。このパラメータは[トレーサビリティウォーターマーク](https://intl.cloud.tencent.com/document/product/266/47920)のユースケースで使用します</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F)のuidパラメータをご参照ください</li> |

#### DrmLicenseInfoタイプ[](id:p2)

| パラメータ名 | 入力必須 | タイプ | 説明 |
| -- | -- | -- | -- |
| expireTimeStamp | いいえ | Integer | キーの有効期限のUnixタイムスタンプ、空のままは有効期限内であることを表します |

>?
>- [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987) を使用する場合、appIdパラメータとしてサブアプリケーションAppIdを設定する必要があります。
>- 署名パラメータの`t`、`exper`、`rlimit`、`us`、`uid`の説明と値は、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) の同名パラメータと完全に一致します。

## 署名計算

VODプレーヤーの署名には、Header、PayLoad、Key によって計算され組み合わせられたデジタルトークンである [JWT](https://tools.ietf.org/html/rfc7519)（JSON Web Token）を採用します。

### Header

HeaderはJSON形式であり、JWTで使用されるアルゴリズム情報を表し、その内容は次のとおり固定的 に使用されます：

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

Payload はJSON形式であり、次に例示するようにプレーヤーの署名パラメータのコンテンツです。

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546300,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101",
    "uid": "1234abcd"
  }
}
```

### Key

Keyは署名計算時に使用するキーであり、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) の`KEY`パラメータと一致します。

### 計算式

1. Signatureの計算：
`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), KEY)`
2. Tokenの計算：
`Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
最終的に得られたTokenが、VODプレーヤー署名となります。

>?HMACSHA256については、[RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3) をご参照ください。base64UrlEncodeについては [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7) をご参照ください。

署名の計算および署名の検証を容易にするため、VODはオンライン署名発行、検証ツールを提供します。
* [Player+ - 署名発行ツール](https://vods.cloud.tencent.com/signature/super-player-sign.html)により高速で署名を発行します。
* [Player+ - 署名検証ツール](https://vods.cloud.tencent.com/signature/super-player-check-sign.html)により高速で署名を検証します。

### 計算例

例えば、ユーザーのappIdが`1255566655`、fileIdが`4564972818519602447`のビデオについてプレーヤー署名が生成され、かつ:

* 有効なリンク不正アクセス防止KEYが`24FEQmTzro4V5u3D5epW`。
* カスタムプレーヤー設定を使用し、カスタム設定名が`MyCfg`。
* プレーヤー署名の配布時間が2019/1/1 19:00:00、対応するUnix時間が`1546300`。
* プレーヤー署名の有効期限が2019/1/1 20:00:00、対応するUnix時間が`1546344000`。
* リンク不正アクセス防止の有効期限が2019/1/1 20:00:00、対応するUnix時間が`5c2b5640`。
* URLでの再生を最大3つの異なるIPで許可。
* 生成されたランダムな文字列が`72d4cd1101`。

この場合の署名手順は、次のとおりです.
1. Headerのコンテンツ：
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
base64UrlEncode で処理した後の結果：
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`。
2. Payloadのコンテンツ：
```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "currentTimeStamp": 1546300,
  "expireTimeStamp": 1546344000,
  "urlAccessInfo": {
    "t": "5c2b5640",
    "rlimit": 3,
    "us": "72d4cd1101",
    "uid": "1234abcd"
  }
}
```
base64UrlEncode で処理した後の結果：
`eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSIsInVpZCI6IjEyMzRhYmNkIn19`。
3. `24FEQmTzro4V5u3D5epW`をKEYとしてHMAC計算を実行した場合、Signature は次のようになります。
`j3WJ9W3V4ve_N_Z157_B9AKkT0GhSmGAEdhv6YtoZSY`。
4. 最終的に Token はこのようになります。
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImN1cnJlbnRUaW1lU3RhbXAiOjE1NDYzNDA0MDAsImV4cGlyZVRpbWVTdGFtcCI6MTU0NjM0NDAwMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNWMyYjU2NDAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSIsInVpZCI6IjEyMzRhYmNkIn19.j3WJ9W3V4ve_N_Z157_B9AKkT0GhSmGAEdhv6YtoZSY`。

## コード例

VODはPython、Java、Go、C#、PHPおよびNode.jsなどの言語用に複数のプレーヤーのサンプルコードを提供しています。詳細については[プレーヤー署名 - 署名の例](https://intl.cloud.tencent.com/document/product/266/38096)をご参照ください。

## インターフェースの説明

- 小さなファイル（5MB未満）のアップロードに使用するAPIは、[シンプルなファイルアップロード](https://intl.cloud.tencent.com/document/product/436/7749)をご参照ください。
- 大きなファイル（5MB超過）のアップロードに使用するAPI、[パートアップロードの初期化](https://intl.cloud.tencent.com/document/product/436/7746)、[パートごとのアップロード](https://intl.cloud.tencent.com/document/product/436/7750)、[パートアップロードの終了](https://intl.cloud.tencent.com/document/product/436/7742)をご参照ください。

## 機能説明
1. メディア（およびカバー）ファイルをアップロードします。
2. APIをサーバーでアップロードする手順は、[サーバーからのアップロードの概要](https://intl.cloud.tencent.com/document/product/266/33910)をご参照ください。

## SDKから
[コンテナのSDK](https://intl.cloud.tencent.com/document/product/436/6474)を使用してAPIを呼び出すことを推奨します。

## APIから

使用方法は、上記APIリンクの中のドキュメントをご参照ください。各APIの構文は次のとおりです。
```
PUT <ObjectName> HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

構文の中の以下の変数は、[VODのアップロード申請で戻ってくる結果](https://intl.cloud.tencent.com/document/product/266/34120)の値を取ります。  

- `<ObjectName>` は**MediaStoragePath**（カバーファイルに対応するのは **CoverStoragePath**）です。
- `<BucketName>-<APPID>` は**StorageBucket**です。
- `<Region>` は**StorageRegion**です。

APIリクエストについて、注意すべき点は以下のとおりです。

- Authorizationの署名には、[VODのアップロード申請で戻ってくる結果](https://intl.cloud.tencent.com/document/product/266/34120)の中の**TempCertificate**のSecretIdとSecretKeyを使用します。[署名のドキュメント](https://intl.cloud.tencent.com/document/api/436/7778)を参照して計算してください。
- HTTPヘッダーまたはPOSTリクエストパケットのform-dataの中で**x-cos-security-token**フィールド（そのリクエストに使用するセキュリティトークンが表示される）を渡します。戻り値は、**TempCertificate**の中のTokenフィールドとなります。

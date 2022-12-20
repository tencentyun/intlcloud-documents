# 目的

ここでは主に、サードパーティプレーヤーを使用してVOD暗号化ビデオ（Widevine、FairPlay）を再生する方法についてご説明します。

# 概要

ビデオの再生情報を取得してからサードパーティプレーヤーを使用するだけで、暗号化されたビデオを復号し再生できます。

再生情報は次のとおりです。

- Widevine
  - DrmToken （再生ライセンスの取得に使用します）
  - コンテンツURL
  - 再生ライセンスURL （License URL）
- FairPlay
  - DrmToken （再生ライセンスの取得に使用します）
  - コンテンツURL
  - 再生ライセンスURL （License URL）
  - 証明書URL （Certificate URL）

## アーキテクチャフローチャート

### 商用DRM（Widevine、FairPlay）

![](https://qcloudimg.tencent-cloud.cn/raw/c77d070232e66d1eef6a6a91b5e8561e.jpg)

- 再生情報および署名の取得
  APP端末での業務認証の成功後、AppサーバーからAPP端末に再生情報および署名（DrmToken）を配布します。

- ビデオコンテンツ、証明書のダウンロードおよびLicenseの取得

  再生情報を取得後、プレーヤーは再生をトリガーすると同時に、ライセンス（License）取得および証明書取得のリクエストをトリガーします。

- 復号と再生

  Licenseを取得後、プレーヤーはLicenseを使用してビデオを復号し再生します。

# DrmTokenの生成方法

DrmTokenは本質的には[Json Web Token](https://jwt.io/introduction) (JWT)の変形です。DrmTokenもHeader、PayLoad、Signatureの3つの部分に分けられますが、VODでは「~」を使用してこれらの3つの部分をスプライシングする点が異なります。具体的には次のとおりです。

### Header

HeaderはJSON形式であり、JWTで使用されるアルゴリズム情報を表し、その内容は次のとおり固定的 に使用されます：

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

### PayLoad

PayloadはJSON形式であり、次に例示するようにプレーヤーの署名パラメータの内容です。

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

#### PayLoadパラメータ説明

| **パラメータ名**       | **タイプ**   | **入力必須かどうか** | **説明**                                                     |
| ---------------- | ---------- | ------------ | ------------------------------------------------------------ |
| type             | string     | はい           | tokenタイプ。`DrmToken`と入力します。                               |
| appId            | int64      | はい           | AppId。                                                      |
| fileId           | string     | はい           | ファイルId。                                                     |
| issuer       | string | はい       | 発行者。常に`client`と入力します。                                |
| currentTimeStamp | int64      | はい           | 現在のUnixタイムスタンプ。                                           |
| expireTimeStamp  | int64      | いいえ           |  期限切れとなったUnixタイムスタンプ。空のままは有効期限内であることを表します。      |
| random           | int64      | いいえ           | 乱数。                                                     |


### Signatrue

### 計算方法

`Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), pkey)`

>? HMACSHA256については、[RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3) をご参照ください。base64UrlEncodeについては[RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7)をご参照ください。

このうち、再生キー（pkey）はコンソールで照会し取得できます。

VODコンソールの左側ナビゲーションバーの**配信と再生の設定**>**デフォルト配信設定**をクリックすると、ページ右側に再生キーを見つけることができます。

![](https://qcloudimg.tencent-cloud.cn/raw/d3bebcb860f8c9900fca9a645a0879be.png)

### DrmTokenの生成例

- `Header`の内容は次のようになります。

```json
{
 "alg": "HS256",
 "typ": "JWT"
}
```

base64UrlEncodeはエンコード後、`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`となります。

- `PayLoad`は次のようになります。

```json
{
  "type": "DrmToken",
  "appId": 1500014561,
  "fileId": "387702307091793695",
  "currentTimeStamp": 1650964374,
  "expireTimeStamp": 2147483647,
  "random": 4220003655,
  "issuer": "client"
}
```

base64UrlEncodeはエンコード後、`eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9`となります。

- `Signature`を `pkey` （仮に`JduzsUuRvGVPRHvIYwLv`とします）で暗号化すると、`muHWnxX9dXsUAkCzw4uXGcvwKDoA19BkR-hCJVrXyvY`となります。

この場合、`Header`、`PayLoad`、`Signature`を`~`でスプライシングすると、`DrmToken`は`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`となります。

# 再生URLの生成方法

- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)インターフェースを呼び出してコンテンツURLを取得できます。コンテンツURLは返された結果の中の`MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `フィールドです。

- Keyリンク不正アクセス防止を有効にしている場合は、[Keyリンク不正アクセス防止](https://intl.cloud.tencent.com/document/product/266/33986)を参照してリンク不正アクセス防止署名付きのコンテンツURLを生成することができます。


# ライセンスURLの生成方法

商用DRMについては、プレーヤーはライセンス（LIcense）を取得しなければビデオの復号と再生を行うことができません。ライセンスURLによってライセンスのリクエストを送信する方法について次に説明します。

## リクエスト

リクエストURI:

- Widevine:  `https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2`
- FairPlay: `https://fairplay.drm.vod-qcloud.com/fairplay/getlicense/v2`

リクエストメソッド：`POST`

リクエストパラメータ：

| **パラメータ名**        | **説明**                                                     |
| ---------------- | ------------------------------------------------------------ |
| drmToken     | 検証証明書。 |

>? リクエストBODYには、DRMクライアントモジュールで生成したライセンスリクエストデータ（License Request Data）を含める必要があります。

## レスポンス

- 成功の場合、`Status Code`は200で、かつLicenseのバイナリーデータが返されます。

- 失敗の場合、`Status Code`は200以外となります。

### Status Codeリスト
| **Status Code**        | **説明**                                                     |
| ---------------- | ------------------------------------------------------------ |
| 200     | リクエストに成功しました。 |
| 400     | パラメータエラーです。 |
| 403     | 認証に失敗しました。 |
| 500     | 内部エラーです。 |

## 事例

上記のリクエストルールに基づき、`Widevine`スキームのライセンスURLは`https://widevine.drm.vod-qcloud.com/widevine/getlicense/v2?drmToken=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`となります。

# 証明書URLの取得方法

`FairPlay`スキームを使用した暗号化ビデオを再生したい場合は、まず`FairPlay`証明書情報を[申請](https://www.tencentcloud.com/document/product/266/46643)および[送信](https://www.tencentcloud.com/document/product/266/49668)する必要があります。`Widevine`スキームの場合は、証明書URLの取得は不要です。

証明書情報を送信すると、コンソールで証明書URLを確認できます。各サブアプリケーションは同一の証明書URLを共用します。

# サードパーティプレーヤーを使用した再生

再生URL、ライセンスURL、証明書URLを取得後、サードパーティプレーヤーを使用してDRM暗号化ビデオを再生できます。

# まとめ

これで、サードパーティプレーヤーを使用してVODのDRM暗号化ビデオを再生する方法の説明は完了です。
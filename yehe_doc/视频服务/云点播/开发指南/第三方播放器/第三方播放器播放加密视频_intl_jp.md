# 目的

ここでは主に、サードパーティプレーヤーを使用してVOD暗号化ビデオ（SimpleAES）を再生する方法についてご説明します。

# 概要

ビデオの再生情報を取得してからサードパーティプレーヤーを使用するだけで、暗号化されたビデオを復号し再生できます。

再生に関連する情報は次のとおりです。

- DrmToken (ビデオ復号キーの取得に使用します)。
- コンテンツURL。

## アーキテクチャフローチャート

![](https://qcloudimg.tencent-cloud.cn/raw/0869fb5666a8d93a57ae0202f7468c97.jpg)

- 再生情報および署名の取得
  業務認証の成功後、AppサーバーからAPP端末に再生情報および署名（DrmToken）を配布します。

- ビデオコンテンツのダウンロードとキー情報の取得

  再生情報（DrmToken、コンテンツURL）を取得後、再生URLを生成します。プレーヤーは再生をトリガーするとともに、キー情報取得のリクエストを自動的にトリガーします。

- 復号と再生

  プレーヤーはキー情報を取得後、ビデオを自動的に復号して再生します。

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

- `Signature`を`pkey` （仮に`JduzsUuRvGVPRHvIYwLv`とします）で暗号化すると、`NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`となります。

この場合、`Header`、`PayLoad`、`Signature`を`~`でスプライシングすると、`DrmToken`は`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`となります。

# 再生URLの生成方法

- [DescribeMediaInfos](https://intl.cloud.tencent.com/document/product/266/34181)インターフェースを呼び出してコンテンツURLを取得できます。コンテンツURLは返された結果の中の`MediaInfoSet.AdaptiveDynamicStreamingInfo.AdaptiveDynamicStreamingSet.Url `フィールドです。

- Keyリンク不正アクセス防止を有効にしている場合は、[Keyリンク不正アクセス防止](https://intl.cloud.tencent.com/document/product/266/33986)を参照してリンク不正アクセス防止署名付きのコンテンツURLを生成することができます。

- 次の方法に従って再生URLを構築します。

  元のコンテンツURLが`http(s)://xxx.com/xxx/xxx/test.m3u8`であるとします。

  この場合、再生URLは`http(s)://xxx.com/xxx/xxx/voddrm.token.<DrmToken>.test.m3u8`となります。

  このうちのファイル名に`voddrm.token.`プレフィックスを追加し、`<DrmToken>`には上記で生成した`DrmToken`を入力します。

### 事例

コンテンツURLが` https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff `であるとします。

`DrmToken`は`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY`となります。

この場合、最終的な再生URLは次のようになります。

`https://1500014561.vod2.myqcloud.com/4395be81vodtranscq1500014561/8f8e01fb387702307091793695/voddrm.token.eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9~eyJ0eXBlIjoiRHJtVG9rZW4iLCJhcHBJZCI6MTUwMDAxNDU2MSwiZmlsZUlkIjoiMzg3NzAyMzA3MDkxNzkzNjk1IiwiY3VycmVudFRpbWVTdGFtcCI6MTY1MDk2NDM3NCwiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3LCJyYW5kb20iOjQyMjAwMDM2NTUsImlzc3VlciI6ImNsaWVudCJ9~NN_EBW7VxGK69v-w9Q7Dw-sm8Uryfe_NdRUe3RZZ4wY.adp.12.m3u8?t=9ee2bdd0&sign=46f6120466d6e931ad792bad8e4f8dff`

# サードパーティプレーヤーを使用した再生

再生URLを生成すると、サードパーティプレーヤーを使用して暗号化ビデオを再生できます。

# まとめ

これで、サードパーティプレーヤーを使用してVOD暗号化ビデオを再生する方法の説明は完了です。
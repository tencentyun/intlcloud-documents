## 機能説明

DELETE Object APIリクエストは、COSのバケット内のファイル（オブジェクト）を削除することができます。この操作は、リクエスト者がバケットに対する書き込み権限を持っている必要があります。

### 詳細分析

- DELETE Objectリクエストにおいて存在しないオブジェクトを削除することは依然として成功したと見なされ、`204 No Content`を返します。
- DELETE Objectは、ユーザーがこのオブジェクトへの書き込み権限を持っていることを要求します。

## リクエスト

### リクエスト例
```shell
DELETE /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](/document/product/436/7778)ドキュメントを参照してください）。

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー

このリクエスト操作には、特別なリクエストヘッダー情報はありません。


### リクエストボディ

このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 

この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。
#### 特有の応答ヘッダー

このリクエスト操作には、特別な応答ヘッダーがありません。

### 応答ボディ

このリクエストの応答ボディはブランクです。

### エラー分析

このリクエストが発生する可能性がある特別、且つ一般的なエラー状況は以下のとおりです：

|エラーコード|HTTPステータスコード|説明|
|--|--|--|
| NoSuchBucket |404 Not Found|バケットが存在しません| 

COSエラーコード情報、または製品のすべてのエラーリストの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。
## 実際のケース

### リクエスト
```shell
DELETE /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213409;32557109409&q-key-time=1484213409;32557109409&q-header-list=host&q-url-param-list=&q-signature=1c24fe260ffe79b8603f932c4e916a6cbb0af44a
```

### 応答
```shell
HTTP /1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjYTRfYmRjMzVfMzFhOF82MmM3Yg==
```


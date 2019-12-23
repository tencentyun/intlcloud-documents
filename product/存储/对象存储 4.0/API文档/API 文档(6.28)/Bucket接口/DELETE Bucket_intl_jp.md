## 機能説明
DELETE Bucketリクエストは、指定されたアカウントの下のバケットを削除するために使用されます。
>!バケットを削除する前に、バケット内のデータとアップロードされていないパートデータがすべて消去されていることを確認してください。そうでなければ、バケットを削除することができません。

## リクエスト
### リクエスト例
```
DELETE / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
この応答ボディはブランクです。

### エラー分析
以下は、このリクエストで発生する可能性がある特別で一般的なエラー状況です。COSエラーコードの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

|エラーコード|HTTPステータスコード|説明|
|-------|------|------|
|BucketNotEmpty|409 Conflict|空でないバケットを削除することができません|
|AccessDenied|403 Forbidden|バケットを削除するには署名も必要ですが、アクセス権限ないバケットを削除しようとすると、エラーが返されます|
|NoSuchBucket|404 Not Found|存在していないバケットを削除すると、このエラーが返されます|


## 実際のケース

### リクエスト
```
DELETE / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484708950;32557604950&q-key-time=1484708950;32557604950&q-header-list=host&q-url-param-list=&q-signature=2b27b72ad2540ff2dde341dc7579a66ee8cb2afc
```

### 応答
```
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZWRjNjBfOTgxZjRlXzZhYjlfMTg0
```


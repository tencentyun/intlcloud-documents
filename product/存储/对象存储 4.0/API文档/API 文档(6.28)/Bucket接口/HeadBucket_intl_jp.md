## 機能説明
HEAD Bucketリクエストは、このバケットが存在し、それにアクセスする権限を持っているかどうかを確認できます。HEAD権限はReadと同じです。いくつかの状況があります：
- バケットが存在しています。返されたHTTPステータスコードは200です。
- バケットはアクセス権限を持っていません。返されたHTTPステータスコードは403です。
- バケットが存在しません。返されたHTTPステータスコードは404です。

>!現時点では、バケット属性のAPIを公開的に取得していません（つまり、aclなどの情報を返す可能です）。

## リクエスト
### リクエスト例

```shell
HEAD / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）。

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

## 実際のケース

### リクエスト
```shell
HEAD / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 27 Oct 2015 20:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484640517;32557536517&q-key-time=1484640517;32557536517&q-header-list=host&q-url-param-list=&q-signature=7bedc2f84a0a3d29df85fe727d0c1e388c410376
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Thu, 27 Oct 2015 20:32:00 GMT
x-cos-request-id: NTg3ZGQxNDNfNDUyMDRlXzUyOWNfMjY5
```


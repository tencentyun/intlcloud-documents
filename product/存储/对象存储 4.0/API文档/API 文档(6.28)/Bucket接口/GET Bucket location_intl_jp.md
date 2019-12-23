## 機能説明
GET Bucket location APIは、バケットの所属地域情報を取得するために使用されます。このGET操作は、locationパラメータを使用してバケットの地域を返します。APIの操作権限を持つのはバケット所有者のみです。

## リクエスト
### リクエスト例

```
GET /?location HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）。

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
応答ボディは地域情報を返します。

```
<?xml version="1.0" encoding="UTF-8" ?>
<LocationConstraint>cos.ap-beijing</LocationConstraint>
```

具体的なデータ説明は以下のとおりです：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
LocationConstraint|無し|バケットの所属地域を説明します。列挙値について、[地域とアクセスドメイン名](https://cloud.tencent.com/document/product/436/6224)ドキュメントを参照してください。例えば：ap-beijing、ap-hongkong、eu-frankfurtなど|string|はい

###　エラーコード
このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、[エラーコード](https://cloud.tencent.com/document/product/436/7730)セクションを参照してください。


## 実際のケース

### リクエスト

```
GET /?location HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484817522;32557713522&q-key-time=1484817522;32557713522&q-header-list=host&q-url-param-list=location&q-signature=ceb96fc929663dd4d2e6dc0aeb304cdde6761ed
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 92
Connection: keep-alive
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDg0NzlfNDYyMDRlXzM0OWFfZjFk

<LocationConstraint>cos.ap-beijing</LocationConstraint>
```


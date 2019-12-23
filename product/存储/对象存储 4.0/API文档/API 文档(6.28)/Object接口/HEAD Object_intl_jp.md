## 機能説明
HEAD Object APIリクエストは対応するオブジェクトのmeta情報データを取得することができます。HEADの権限はGETの権限と一致します。

### バージョン

デフォルトでは、HEAD操作は現在のバージョンのオブジェクトからメタデータを検索します。異なるバージョンからメタデータを検索するには、versionIdサブリソースを使用してください。

## リクエスト
リクエスト例：
```
HEAD /<ObjectName> HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエスト行

```
HEAD /{ObjectName} HTTP/1.1
```

APIは`HEAD`リクエストを受け付けます。


### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728 "公共请求头部") セクションを参照してください。

#### 非共通のヘッダー

名称|タイプ|必須項目|説明
---|---|---|---
If-Modified-Since|string|いいえ|指定された時間後にオブジェクトが変更された場合、対応するオブジェクトのmeta情報を返します。そうではなければ、304を返します


### リクエストボディ
このリクエストのリクエストボディはブランクです。
## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729 "公共响应头部")セクションを参照してください。

#### 特有の応答ヘッダー

このリクエスト操作の応答ヘッダーの具体的なデータは：

|名称|タイプ|説明|
|---|---|---|
|x-cos-meta- *|string|ユーザーがカスタマイズしたmeta|
|x-cos-object-type|string|オブジェクトを追加でアップロードできるかどうかを示すために使用されます。列挙値：normalまたはappendable|
|x-cos-storage-class|string|オブジェクトのストレージレベル、列挙値：STANDARD、STANDARD_IA|
|x-cos-version-id|string|返したオブジェクトのバージョンID。|
|x-cos-server-side​-encryption|string|オブジェクトがCOS管理サーバーの暗号化によって保管されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値AES256を含めます|


### 応答ボディ
このリクエストの応答ボディはブランクです。

## 実際のケース

### リクエスト

```
HEAD /123 HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2017 17:26:53 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213210;32557109210&q-key-time=1484213210;32557109210&q-header-list=host&q-url-param-list=&q-signature=ac61b8eb61964e7e6b935e89de163a479a25c210
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
Date: Thu, 12 Jan 2017 17:26:53 GMT
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 11 Jan 2017 07:30:07 GMT
Server: tencent-cos
x-cos-object-type: normal
x-cos-request-id: NTg3NzRiZGRfYmRjMzVfM2Y2OF81N2YzNA==
x-cos-storage-class: STANDARD
```




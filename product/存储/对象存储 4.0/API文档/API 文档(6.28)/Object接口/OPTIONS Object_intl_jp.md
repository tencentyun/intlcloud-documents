## 機能説明
OPTIONS Object APIは、オブジェクトのクロスオリジンアクセス構成のプリフライトリクエストを実行します。つまり、クロスオリジンリクエストが送信される前に、オプションリクエストが送信され、特定のソースドメイン、HTTPメソッド、およびヘッダー情報などをCOSに送信され、実際のクロスオリジンリクエストを送信できるかどうかが判断されます。CORS構成が存在していない場合、リクエストは403 Forbiddenを返します。PUT Bucket cors APIを通してバケットのCORSサポートを起動することができます。

## リクエスト
### リクエスト例

```
OPTIONS /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Origin: Origin
Access-Control-Request-Method: HTTPMethod
Access-Control-Request-Headers: RequestHeader
Authorization: Auth String
```

> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）。

### リクエストヘッダー
#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー

名称|タイプ|説明|必須項目
---|---|---|---
Origin|string|シミュレートクロスオリジンアクセスのリクエストソースドメイン名|はい
Access-Control-Request-Method|string|シミュレートクロスオリジンアクセスのHTTPリクエスト方法|はい
Access-Control-Request-Headers|string|シミュレートクロスオリジンアクセスのリクエストヘッダー|いいえ

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答
### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。

#### 特有の応答ヘッダー

このリクエスト操作の特有の応答ヘッダーの具体的なデータは：

|名称|タイプ|説明|
|---|---|---|
|Access-Control-Allow-Origin|string|シミュレートクロスオリジンアクセスのリクエストソースドメイン名。ソースが許可していない場合、このヘッダーは返されません|
|Access-Control-Allow-Methods|string|シミュレートクロスオリジンアクセスのHTTPリクエスト方法。リクエスト方法が許可していない場合、このヘッダーは返されません|
|Access-Control-Allow-Headers|string|シミュレートクロスオリジンアクセスのリクエストヘッダー。任意のリクエストヘッダーのシミュレーションが許可していない場合、このヘッダーはこのリクエストヘッダーを返しません|
|Access-Control-Expose-Headers|string|シミュレートクロスオリジンアクセスのHTTPリクエスト方法。リクエスト方法が許可していない場合、このヘッダーは返されません|
|Access-Control-Max-Age|string|オプションリクエストが取得される結果の有効期間を設定します|

### 応答ボディ
この応答ボディはブランクです。

## 実際のケース

### リクエスト

```
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2017 17:26:53 GMT
Origin: http://www.qq.com
Access-Control-Request-Method: PUT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1487070734;32466654734&q-key-time=1487070734;32559966734&q-header-list=host&q-url-param-list=&q-signature=2ac3ada19910f44836ae0df72a0ec1003f34324b
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
x-cos-request-id: NTg3NzRiZGRfYmRjMzVfM2Y2OF81N2YzNA==
Date: Thu, 12 Jan 2017 17:26:53 GMT
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Access-Control-Allow-Origin: http://www.qq.com
Access-Control-Allow-Methods: PUT
Access-Control-Expose-Headers: x-cos-request-id
Server: tencent-cos
```


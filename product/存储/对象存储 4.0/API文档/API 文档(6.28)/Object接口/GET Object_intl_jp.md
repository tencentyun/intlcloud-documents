## 機能説明
GET Object APIリクエストは、COSバケット内のファイル（オブジェクト）をローカルにダウンロードすることができます。この操作では、リクエスト者はターゲットオブジェクトへの読み取り権限、またはターゲットオブジェクトは全員への読み取り権限（パブリック読み取り）を許可する必要があります。

### バージョン
複数のバージョンが有効になっている場合、このGET操作はオブジェクトの現在のバージョンを返します。異なるバージョンを返すには、versionIdパラメータを使用してください。

>**注意**
もしこのオブジェクトの現在のバージョンが削除タグである場合、COSはこのオブジェクトが存在しないように動作し、応答x-cos-delete-marker：trueを返します。

## リクエスト

リクエスト例：
```
GET /<ObjectName> HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエスト行

```
GET /{ObjectName} HTTP/1.1
```

APIは`GET`リクエストを受け付けます。

#### リクエストパラメータ


| 名称                         | タイプ   | 必須項目 | 説明                                      |
| ---------------------------- | ------ | ---- | ----------------------------------------- |
| response-content-type        | string | いいえ   | 応答ヘッダーのContent-Typeパラメータを設定します        |
| response-content-language    | string | いいえ   | 応答ヘッダーのContent-Languageパラメータを設定します    |
| response-expires             | string | いいえ   | 応答ヘッダーのContent-Expiresパラメータを設定します     |
| response-cache-control       | string | いいえ   | 応答ヘッダーのCache-Controlパラメータを設定します       |
| response-content-disposition | string | いいえ   | 応答ヘッダーのContent-Dispositionパラメータを設定します |
| response-content-encoding    | string | いいえ   | 応答ヘッダーのContent-Encodingパラメータを設定します    |

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728 "公共请求头部") セクションを参照してください。

#### 非共通のヘッダー

| 名称                | タイプ   | 必須項目 | 説明                                                         |
| ------------------- | ------ | ---- | ------------------------------------------------------------ |
| Range               | string | いいえ   | RFC 2616で定義されたファイルダウンロードの指定範囲、単位はバイト（bytes）です     |
| If-Unmodified-Since | string | いいえ   | ファイル変更時間が指定された時間より早いか等しい場合、ファイルの内容を返します。そうでなければ、412（precondition failed）を返します|
| If-Modified-Since   | string | いいえ   | 指定された時間後にオブジェクトが変更された場合、対応するObject meta情報を返します。そうではなければ、304（not modified）を返します|
| If-Match            | string | いいえ   | ETagが指定された内容と一致する場合、ファイルを返します。そうでなければ、412（precondition failed）を返します|
| If-None-Match       | string | いいえ   | ETagが指定された内容と一致しない場合、ファイルを返します。そうでなければ、304（not modified）を返します|

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
|x-cos-meta- *|string|ユーザーがカスタマイズしたメタデータ|
|x-cos-object-type|string|オブジェクトを追加でアップロードできるかどうかを示すために使用されます。列挙値：normalまたはappendable|
|x-cos-storage-class|string|オブジェクトのストレージレベル、列挙値：STANDARD、STANDARD_IA|
|x-cos-version-id|string|検索されたオブジェクトに一意のバージョンIDがある場合、バージョンIDを返します。|
|x-cos-server-side​-encryption|string|オブジェクトがCOS管理サーバーの暗号化によって保管されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値AES256を含めます。|


### 応答ボディ

ダウンロード成功、ファイル内容は応答ボディにあります。

###　エラーコード

| エラーコード                | 説明                               | HHTPステータスコード                                                  |
| --------------------- | ---------------------------------- | ------------------------------------------------------------ |
| InvalidArgument       | 提供されたパラメータエラー                     | 400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) |
|SignatureDoesNotMatch|提供された署名は規則に適合しません。このエラーコードを返します|403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchKey             | ダウンロードされたファイルが存在しない場合、エラーコードが返されます|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) 

## 実際のケース

### リクエスト1

```
GET /123 HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639
```

### 応答1

```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/octet-stream
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename=\"filename.jpg\"
Content-Range: bytes 0-16086/16087
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==
x-cos-storage-class: STANDARD

[Object]
```

### リクエスト2

**response-xxxパラメータが持っています**

```
GET /123?response-content-type=application%2fxml HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639

```

### 応答2

```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename=\"filename.jpg\"
Content-Range: bytes 0-16086/16087
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==
x-cos-storage-class: STANDARD

[Object]
```



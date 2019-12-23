## 機能説明
Upload Part APIリクエストは、オブジェクトをパートの方式でCOSにアップロードします。最大10000パートをサポートし、各パートサイズは1MB - 5GBで、最後のパートは1MB未満できます。

### 詳細分析
1. マルチパートアップロードは、まずInitiate Multipart Upload APIを使用して初期化する必要があります。初期化後、今回のアップロードを一意に識別するuploadIdを取得します。
2. Upload Partをリクエストするたびに、partNumberとuploadIdを送信する必要があります。partNumberはパート番号です。アウトオブオーダーアップロードをサポートします。
3. 渡されたuploadIdとpartNumber両方が同じ場合、後で渡されるパートは前に渡されたパートを上書きします。uploadIdが存在しない場合は、404エラーNoSuchUploadを返します。

## リクエスト
### リクエスト例

```shell
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: Size
Authorization: Auth String

[Object]
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー
**必須ヘッダー**
該当リクエスト操作ではリクエストヘッダーが必須ヘッダーを使用する必要があります。具体的な内容は以下のとおりです：

| 名称             | 説明                            | タイプ     | 必須項目   |
| :------------- | :---------------------------- | :----- | :--- |
| Content-Length | RFC 2616の中で定義されたHTTPリクエスト内容の長さ（バイト） | String | はい    |

**推薦ヘッダー**
該当リクエスト操作はリクエストヘッダーが推薦ヘッダーを使用することを勧めます。具体的な内容は以下のとおりです：

| 名称          | 説明                                       | タイプ     | 必須項目   |
| :---------- | :--------------------------------------- | :----- | :--- |
| Expect      | RFC 2616の中で定義されたHTTPリクエスト内容の長さ（バイト）            | String | いいえ    |
| Content-MD5 | RFC 1864で定義された、Base64エンコードされた128-bit内容MD5チェック値。このヘッダーは、ファイルの内容が変更されたかどうかを確認するために使用されます| String | いいえ    |

#### リクエストパラメータ
具体的な内容は以下のとおりです：

| パラメータ名称       | 説明                                       | タイプ     | 必須項目   |
| :--------- | :--------------------------------------- | :----- | :--- |
| partNumber | 今回のマルチパートアップロードの番号を識別します                              | String | はい    |
|uploadId|今回マルチパートアップロードのIDを識別します。<br>Initiate Multipart Upload APIを使ってマルチパートアップロードを初期化すると、uploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、このパートデータはファイル全体における相対位置も識別します | String | はい    |

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
**サーバーの暗号化による応答ヘッダ**

アップロード時にサーバーの暗号化を指定した場合、応答ヘッダーには次の情報が含まれます：

| 名称                           | 説明                                       | タイプ     |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | オブジェクトにサーバーの暗号化を有効にする方法を指定します。<br/>COSマスタ暗号鍵で暗号化します：AES256 | String |

### 応答ボディ
この応答ボディはブランクです。

## 実際のケース

### リクエスト
```shell
PUT /exampleobject?partNumber=1&uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727403;32557623403&q-key-time=1484727403;32557623403&q-header-list=host&q-url-param-list=partNumber;uploadId&q-signature=bfc54518ca8fc31b3ea287f1ed2a0dd8c8e88a1d
Content-Length: 10485760

[Object]
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Etag: "e1e5b4965bc7d30880ed6d226f78a5390f1c09fc"
Server: tencent-cos
x-cos-request-id: NTg3ZjI0NzlfOWIxZjRlXzZmNGJfMWYy

```


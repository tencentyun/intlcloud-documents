## 機能説明
Abort Multipart Uploadは、1つのマルチパートアップロードを破棄し、アップロードされたパートを削除するために使用されます。このAbort Multipart Uploadを呼び出すとき、このUpload Partsを使用しているリクエストがあると、Upload Partsは失敗を返します。このUploadIdが存在していなければ、404 NoSuchUploadを返します。

>!アップロードされたが終了していないパートはストレージスペースを占有し、ストレージコストを発生させるため、タイムリーにマルチパートアップロードを完了するか、またはマルチパートアップロードを破棄することをお勧めします。

## リクエスト

### リクエスト例
```shell
DELETE /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

#### リクエストパラメータ

具体的な内容は以下のとおりです：

|パラメータ名|説明|タイプ |必須項目|
|---|---|---|---|
|uploadId|今回マルチパートアップロードのIDを識別します。<br>Initiate Multipart Upload APIを使ってマルチパートアップロードを初期化するとき、uploadIdが取得されます。このIDは、このパートデータを一意に識別するだけでなく、ファイル全体におけるこのパートデータの相対位置も識別します |String|はい|

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


## 実際のケース

### リクエスト
```shell
DELETE /exampleobject?uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 26 Oct 2013 21:22:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484728626;32557624626&q-key-time=1484728626;32557624626&q-header-list=host&q-url-param-list=uploadId&q-signature=2d3036b57cade4a257b48a3a5dc922779a562b18
```

### 応答
```shell
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 26 Oct 2013 21:22:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI5MzlfOTgxZjRlXzZhYjNfMjBh
```


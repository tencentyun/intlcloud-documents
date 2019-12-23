## 機能説明
Upload Part - Copyリクエストは、オブジェクトのパート内容をソースパスからターゲットパスにコピーすることを実装しています。x-cos-copy-sourceを指定してソースオブジェクトを指定し、x-cos-copy-source-rangeはバイト範囲（パートサイズは5MB - 5GBです）を指定します。

>!
>- ターゲットオブジェクトとソースオブジェクトが同じ地域に属しておらず、ターゲットオブジェクトのパートが5GBを超える場合、オブジェクトをコピーするために、マルチパートアップロードまたはパートコピーAPIを使用する必要があります。
>- アップロードマルチパートオブジェクトを使用するには、まずマルチパートアップロードを初期化する必要があります。マルチパートアップロードを初期化する応答で、一意の記述子（upload ID）が返されます。このIDをマルチパートアップロードリクエストに含める必要があります。

### バージョン
バケットが複数のバージョンを有効にする場合、x-cos-copy-sourceはコピーされるオブジェクトの現在のバージョンを識別します。現在のバージョンが削除タグであり、x-cos-copy-sourceがバージョンを指定していない場合、COSは該当オブジェクトが削除されたとみなして404エラーを返します。x-cos-copy-sourceにversionIdを指定し、versionIdが削除タグの場合、削除タグはx-cos-copy-sourceのバージョンとして使用できないため、COSはHTTP 400エラーを返します。

## リクエスト
### リクエスト例

```http
PUT /examplebucket?partNumber=PartNumber&uploadId=UploadId  HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
x-cos-copy-source: <Bucketname>-<APPID>.cos.<Region>.myqcloud.com/filepath
x-cos-copy-source-range: bytes=first-last
x-cos-copy-source-if-match: etag
x-cos-copy-source-if-none-match : etag
x-cos-copy-source-if-unmodified-since: time_stamp
x-cos-copy-source-if-modified-since: time_stamp
```

>Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照します）。


### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー

**必須ヘッダー**

このリクエスト操作の実現では、以下の必須ヘッダーを使用します：

| 名称         | 説明           | タイプ     | 必須項目   |
| ----------- | ----------- | ------------- | ---- |
| x-cos-copy-source     | ソースオブジェクトURLパス、versionidサブリソースを通して、履歴バージョンを指定します| String | はい    |


**推薦ヘッダー**

このリクエスト操作の実現では、以下の推薦リクエストヘッダーを使用します：

| 名称          | 説明      | タイプ     | 必須項目   |
| ---------------- | ---------- | ------ | -------- |
| x-cos-copy-source-range                    | ソースオブジェクトのバイト範囲。範囲値はbytes = first-lastフォーマットでなければならず、firstとlastはどちらも0から始まるオフセットです。<br>例えば、bytes = 0-9は、ソースオブジェクトデータの最初の10バイトをコピーすることを意味します。指定されていない場合は、オブジェクト全体をコピーすることを意味します       | Integer | はい    |
| x-cos-copy-source-If-Modified-Since   | 指定された時間後、オブジェクトが変更されると、操作を実行します。そうではなければ、412を返します<br>x-cos-copy-source-If-None-Matchと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します | String | いいえ    |
x-cos-copy-source-If-Unmodified-Since|指定された時間後、オブジェクトが変更されていなければ、操作を実行します。そうではなければ、412を返します<br>x-cos-copy-source-If-Matchと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します | String | いいえ    |
| x-cos-copy-source-If-Match            | オブジェクトのEtagが指定と一致する場合、操作を実行します。そうではなければ、412を返します<br>x-cos-copy-source-If-Unmodified-Sinceと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します | String | いいえ    |
| x-cos-copy-source-If-None-Match       | オブジェクトのEtagが指定と一致する場合、操作を実行します。そうではなければ、412を返します<br>x-cos-copy-source-If-Modified-Sinceと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します | String | いいえ    |

### リクエストパラメータ

 名称|説明|タイプ|必須項目
---|---|---|---
partNumber|パートコピーのパート番号|string|はい
uploadId|アップロードマルチパートファイルを使用するには、まずマルチパートアップロードを初期化する必要があります。マルチパートアップロードを初期化する応答で、一意の記述子（upload ID）が返されます。このIDをマルチパートアップロードリクエストに含める必要があります|string|はい

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー

名称|説明|タイプ
---|---|---
x-cos-copy-source-version-id|ソースバケットでバージョン制御を有効にした場合は、ソースオブジェクトのバージョンをコピーします|string
x-cos-server-side-encryption|オブジェクトがCOS管理のサーバー暗号化によって保存されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値を含めます：AES256 | String

### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

具体的なデータ内容は以下のとおりです：

| 名称          | 説明             | タイプ     |
| ---------- | ------------------- | ------ |
| CopyPartResult | コピー結果情報を返します           | String |
| ETag             | オブジェクトのMD5アルゴリズムチェック値を返します。ETagの値を使用して、オブジェクトの内容が変更されたかどうかを確認できます。| String |
| LastModified     | オブジェクトの最後の変更時間を返します。GMTフォーマット        | String |

## 実際のケース
### リクエスト

```HTTP
PUT /exampleobject?partNumber=1&uploadId=1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 HTTP/1.1
User-Agent: curl/7.19.7 (x86_64-redhat-linux-gnu) libcurl/7.19.7 NSS/3.13.1.0 zlib/1.2.3 libidn/1.18 libssh2/1.2.2
Accept: */*
x-cos-copy-source:examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/exampleobject1
x-cos-copy-source-range: bytes=10-100
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1507530223;1508530223&q-key-time=1507530223;1508530223&q-header-list=&q-url-param-list=&q-signature=d02640c0821c49293e5c289fa07290e6b2f05cb2
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133 
Connection: keep-alive 
Date: Mon, 04 Sep 2017 04:45:45 GMT
Server: tencent-cos
x-cos-request-id: NTlkYjFjYWJfMjQ4OGY3MGFfNGIzZV9k

<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```


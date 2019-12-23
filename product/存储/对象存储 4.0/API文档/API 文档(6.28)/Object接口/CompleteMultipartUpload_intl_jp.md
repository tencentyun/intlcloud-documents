## 機能説明
Complete Multipart Upload APIリクエストは、全体のマルチパートアップロードを完了するために使用されます。Upload Partsを使用してすべてのパートをアップロードした後、ファイル全体のマルチパートアップロードを完了するためにAPIを呼び出す必要があります。このAPIを使用するとき、パートの正確さを検証するために、リクエストボディの各パートにPartNumberとETagを指定する必要があります。
マルチパートアップロード後にマージする必要があり、マージに数分かかるため、パートのマージが開始されると、COSはすぐにステータスコード200を返します。マージ中、COSは定期的にスペース情報を返して接続を保持します。マージが完了してから、COSがボディのなかでマージされたパートの内容を返します。
- アップロードパートが1MB未満の場合、APIが呼び出されると、400 EntityTooSmallが返されます。
- アップロードパート番号が連続していない場合、このAPIが呼び出されると400 InvalidPartが返されます。
- リクエストボディのパート情報が番号の昇順に並んでいない場合、APIが呼び出されたときに400 InvalidPartOrderが返されます。
- UploadIdが存在しない場合は、APIが呼び出されたときに404 NoSuchUploadが返されます。

>!アップロードされたが終了していないパートはストレージスペースを占有し、ストレージコストを発生させるため、タイムリーにマルチパートアップロードを完了するか、またはマルチパートアップロードを破棄することをお勧めします。

## リクエスト

### リクエスト例
```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）


### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ
このAPIリクエストのリクエストボディの具体的なノード内容は：
```shell
<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
    ...
</CompleteMultipartUpload>
```

具体的なデータ内容は以下のとおりです：

| ノード名称（キーワード）               |親ノード | 説明              | タイプ        |必須項目   |
| :---------------------- | :--- | :-------------- | :-------- | :--- |
| CompleteMultipartUpload | 無し    | 今回のマルチパートアップロードのすべての情報を説明するために使用されます | Container | はい    |

コンテナノードCompleteMultipartUploadの内容：

| ノード名称（キーワード） |親ノード                     | 説明                | タイプ        |必須項目   |
| :-------- | :---------------------- | :---------------- | :-------- | :--- |
| Part      | CompleteMultipartUpload | 今回のマルチパートアップロードのすべてのパートの情報を説明するために使用されます | Container | はい    |

コンテナノードPartの内容：

| ノード名称（キーワード）  |親ノード                          | 説明               | タイプ      |必須項目   |
| :--------- | :--------------------------- | :--------------- | :------ | :--- |
| PartNumber | CompleteMultipartUpload.Part | パート番号              | Integer | はい    |
| ETag       | CompleteMultipartUpload.Part | 各パートファイルのMD5アルゴリズムチェック値 | String  | はい    |

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
**サーバーの暗号化による応答**

アップロード時にサーバーの暗号化を指定した場合、応答ヘッダーには次の情報が含まれます：

| 名称                           | 説明                                       | タイプ     |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | オブジェクトにサーバーの暗号化を有効にする方法を指定します。<br/>COSマスタ暗号鍵で暗号化します：AES256 | String |

### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：
```shell
<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/ObjectName</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>examplebucket</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```
具体的なデータ内容は以下のとおりです：

| ノード名称（キーワード）                     | 親ノード  | 説明       | タイプ        |
| :---------------------------- | :--- | :------- | :-------- |
| CompleteMultipartUploadResult | 無し    | すべての返し情報を説明します | Container |

コンテナノード CompleteMultipartUploadResultの内容：

| ノード名称（キーワード） | 親ノード                           | 説明                                       | タイプ     |
| :-------- | :---------------------------- | :--------------------------------------- | :----- |
| Location  | CompleteMultipartUploadResult | オブジェクトのパブリックネットワークアクセスドメイン名を作成します                         | URL    |
| Bucket    | CompleteMultipartUploadResult | マルチパートアップロードされたターゲットバケット。ユーザーがカスタマイズで生成された文字列とシステムで生成されたappid数値列をハイフンで接続します。例えば：examplebucket-1250000000 | String |
| Key       | CompleteMultipartUploadResult | オブジェクト名称                                | String |
| ETag      | CompleteMultipartUploadResult | マージされたオブジェクトの一意のタグ値。この値はオブジェクト内容のMD5チェック値ではなく、オブジェクトの一意性をチェックするためにのみ使用できます                        | String |

## 実際のケース

### リクエスト
```shell
POST /exampleobject?uploadId=1484728886e63106e87d8207536ae8521c89c42a436fe23bb58854a7bb5e87b7d77d4ddc48 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484729794;32557625794&q-key-time=1484729794;32557625794&q-header-list=host&q-url-param-list=uploadId&q-signature=23627c8fddb3823cce4257b33c663fd83f9f820d
Content-Length: 138

<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9774"</ETag>
  </Part>
</CompleteMultipartUpload>
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 277
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjJlMjVfNDYyMDRlXzM0YzRfMjc1

<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/ObjectName</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>examplebucket</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```


## 機能説明
List Multipart Uploadsは、実行中のマルチパートアップロードを照合するために使用されます。単回リクエスト操作で、最大1000個の実行中のマルチパートアップロードがリストされます。

>!このリクエストはバケットの読み取り権限が必要です。

## リクエスト
### リクエスト例

```
GET /?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストパラメータ

具体的な内容は以下のとおりです：<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| 名称               | 説明                                       | タイプ     | 必須項目   |
| ---------------- | ---------------------------------------- | ------ | ---- |
| delimiter        | 区切りは記号の1つです。オブジェクト名に含まれた指定のプレフィックスと最初出現したデリミター文字の間にあるオブジェクトを同じ要素セットとします：common prefix。prefixがなければ、パスの先頭から始めます | String | いいえ    |
| encoding-type    | 戻り値のエンコードフォーマットを指定します。正しい値：url                               | String | いいえ    |
| prefix           | 返したオブジェクトキーはプレフィックスの値をプレフィックスとする必要があります。</br>プレフィックスを使って照合する場合、返したキーにはまだプレフィックスが含まれることをご注意ください | String | いいえ    |
| max-uploads      | 返したmultipartの最大数量を設定します。正しい値は1 - 1000です。デフォルトでは1000です                       | String | いいえ    |
| key-marker       | upload-id-markerと一緒に使用します<Br/>upload-id-markerが指定されていない場合は、ObjectNameがkey-markerの後（アルファベット順）にあるエントリがリストされます<Br/>upload-id-markerが指定されている場合、ObjectNameがkey-markerの後（アルファベット順）にあるエントリがリストされます。ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後（アルファベット順）にあるエントリがリストされます。 | String | いいえ    |
| upload-id-marker | key-markerと共に使用され、<Br/>key-markerが指定されていない場合、upload-id-markerが無視されます。<Br/>key-markerが指定された場合、ObjectNameがkey-markerの前（アルファベット順）にあるエントリがリストされます。ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの前（アルファベット順）にあるエントリがリストされます。| String | いいえ    |

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：

```
<ListMultipartUploadsResult>
  <Bucket></Bucket>
  <Encoding-Type></Encoding-Type>
  <KeyMarker></KeyMarker>
  <UploadIdMarker></UploadIdMarker>
  <NextKeyMarker></NextKeyMarker>
  <NextUploadIdMarker></NextUploadIdMarker>
  <MaxUploads></MaxUploads>
  <IsTruncated></IsTruncated>
  <Prefix></Prefix>
  <Delimiter></Delimiter>
  <Upload>
    <Key></Key>
    <UploadID></UploadID>
    <StorageClass></StorageClass>
    <Initiator>
      <ID></ID>
	<DisplayName></DisplayName>
    </Initiator>
    <Owner>
      <ID></ID>
	<DisplayName></DisplayName>
    </Owner>
    <Initiated></Initiated>
  </Upload>
  <CommonPrefixes>
    <Prefix></Prefix>
  </CommonPrefixes>
</ListMultipartUploadsResult>
```

具体的なデータ内容は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| ListMultipartUploadsResult |無し| すべてのマルチパートアップロード情報を表すために使用されます | Container |

コンテナノードListMultipartUploadsResultの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| Bucket | ListMultipartUploadsResult | マルチパートアップロードのターゲットバケット。ユーザーがカスタマイズで生成された文字列とシステムで生成されたappid数値列をハイフンで接続します。例えば：mybucket-1250000000 |  String |
| Encoding-Type | ListMultipartUploadsResult | 戻り値のエンコードフォーマットを指定します。正しい値：url |  String |
| KeyMarker | ListMultipartUploadsResult| キー値から始まるエントリをリストします |  String |
| UploadIdMarker | ListMultipartUploadsResult | リストされたエントリはこのUploadId値から始まります |  String |
| NextKeyMarker | ListMultipartUploadsResult | 仮に返されたエントリが遮断された場合、返されたNextKeyMarkerが次のエントリの開始点です | String |
| NextUploadIdMarker | ListMultipartUploadsResult | 仮に返されたエントリが遮断された場合、返されたUploadIdが次のエントリの起点です |  String |
| MaxUploads | ListMultipartUploadsResult | 返したmultipartの最大数量を設定します。正しい値は0 - 1000です | String |
| IsTruncated | ListMultipartUploadsResult | 返されたエントリが遮断されたかどうか、ブール値：TRUE、FALSE |  Boolean |
| Prefix | ListMultipartUploadsResult | 返したオブジェクトキーはプレフィックスの値をプレフィックスとする必要があります。</br>プレフィックスの値を使って照合する場合、返したキーにはまだプレフィックスが含まれることをご注意ください | String |
| Delimiter | ListMultipartUploadsResult | 区切りは記号の1つです。オブジェクト名に含まれた指定のプレフィックスと最初出現したデリミター文字の間にあるオブジェクトを同じ要素セットとします：common prefix。プレフィックスがなければ、パスの先頭から始めます |  String |
| Upload | ListMultipartUploadsResult  | 各Uploadの情報 |  Container |
| CommonPrefixes | ListMultipartUploadsResult | プレフィックスとデリミターの間の同じパスが1つのタイプに分類され、Common Prefixとして定義されます |  Container |

コンテナノードアップロードの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| Key | ListMultipartUploadsResult.Upload |  オブジェクトの名称 |  String |
| UploadID | ListMultipartUploadsResult.Upload |  今回のマルチパートアップロードIDを示します | String |
| StorageClass | ListMultipartUploadsResult.Upload |  パートのストレージレベルを示すために使用されます。列挙値：STANDARD、STANDARD_IA、ARCHIVE |  String |
| Initiator | ListMultipartUploadsResult.Upload |  このアップロード発起者の情報を表すために使用されます |  Container |
| Owner | ListMultipartUploadsResult.Upload | これらのパート所有者の情報を表すために使用されます |  Container |
| Initiated | ListMultipartUploadsResult.Upload |  マルチパートアップロードの開始時間 |  Date |

コンテナノードInitiatorの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Initiator | ユーザー唯一のCAM身元ID | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Initiator | ユーザー身元IDの略語（UIN） | String  |

コンテナノードオーナーの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Owner | ユーザー唯一のCAM身元ID  | String    |
| DisplayName | ListMultipartUploadsResult.Upload.Owner| ユーザー身元IDの略語（UIN） | String  |

コンテナノードCommonPrefixesの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| Prefix | ListMultipartUploadsResult.CommonPrefixes | 具体的なCommonPrefixesを示します | String    |

### エラー分析
このリクエストが発生する可能性がある特別、且つ一般的なエラー状況は以下のとおりです：

| エラーコード             | HTTPステータスコード         |説明                    | 
| ------------- | ------------------------------------ | ------------- |
| InvalidArgument | 400 Bad Request |1.max-uploadsは整数であり、且つその値が0~1000の間でなければなりません。そうでなければ、InvalidArgumentを返します；<br>2.encoding-typeの値はurlしか取りません。そうでなければ、InvalidArgument を返します | 

COSエラーコード情報、または製品のすべてのエラーリストの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

## 実際のケース

### リクエスト

```
GET /?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Jan 2015 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727508;32557623508&q-key-time=1484727508;32557623508&q-header-list=host&q-url-param-list=uploads&q-signature=5bd4759a7309f7da9a0550c224d8c61589c9dbbf
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1203
Date: Wed, 18 Jan 2015 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI0ZGRfNDQyMDRlXzNhZmRfMjRl

<ListMultipartUploadsResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Encoding-Type/>
    <KeyMarker/>
    <UploadIdMarker/>
    <MaxUploads>1000</MaxUploads>
    <Prefix/>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <Upload>
        <Key>Object</Key>
        <UploadID>1484726657932bcb5b17f7a98a8cad9fc36a340ff204c79bd2f51e7dddf0b6d1da6220520c</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:04:17 2017</Initiated>
    </Upload>
    <Upload>
        <Key>Object</Key>
        <UploadID>1484727158f2b8034e5407d18cbf28e84f754b791ecab607d25a2e52de9fee641e5f60707c</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:12:38 2017</Initiated>
    </Upload>
    <Upload>
        <Key>exampleobject</Key>
        <UploadID>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:14:30 2017</Initiated>
    </Upload>
</ListMultipartUploadsResult>

```


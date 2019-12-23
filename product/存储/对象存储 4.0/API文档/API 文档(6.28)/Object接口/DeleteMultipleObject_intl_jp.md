## 機能説明
DELETE Multiple Object APIリクエストは、指定されたバケット内のオブジェクトの一括削除を実現し、単回リクエストで最大1000個のオブジェクトの一括削除をサポートします。応答結果に対して、COSはVerboseとQuietという2つのモードを提供します：Verboseモードは各オブジェクトの削除結果を返します；Quietモードはエラーのオブジェクト情報のみを返します。
>!このリクエストは、ボディの完全性を確認するためにContent-MD5が持つ必要です。

### 詳細分析
1. 各一括削除リクエストには、削除が必要な最大1000個のオブジェクトしか含めることができません。
2. 一括削除は、verboseとquietという2つの返しモードをサポートしています。デフォルトはverboseモードです。verboseモードは各キーの削除状況を返し、quietモードは削除失敗したキーの状況のみを返します。
3. 一括削除は、リクエストボディが変更されていないことを確認するために、Content-MD5ヘッダーを持つ必要があります。
4. 一括削除リクエストを使用すると、存在しないキーを削除しても、削除成功と見なされます。

## リクエスト

文法の例：
```shell
POST /?delete HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

### リクエスト行
```shell
POST /?delete HTTP/1.1
```
APIはPOSTリクエストを受け付けます。

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー
**必須ヘッダー**
このリクエスト操作の実現では、以下の必須ヘッダーを使用します：
<style rel="stylesheet"> table th:nth-of-type(1) { width: 200px;	} </style>

|名称|説明|タイプ|必須項目|
|:---|:---|:---|:---|
| Content-Length | RFC 2616の中で定義されたHTTPリクエスト内容の長さ（バイト）| String | はい |
| Content-MD5 | RFC 1864の中で定義された、Base64エンコードされた128-bit内容MD5チェック値。このヘッダーは、ファイルの内容が変更されたかどうかを確認するために使用されます| String | はい |

### リクエストボディ
このリクエストのリクエストボディの具体的なノード内容は：
```shell
<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

具体的な説明は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:---|:---|:---|:---|
| DELETE |無し| 今回の削除結果を返す方式とターゲットオブジェクトを説明します | Container | はい |
| Quiet | DELETE|ブール値、この値はQuietモードを起動するかどうかを決定します。<br> 値はtrueである場合、Quietモードを起動し、値はfalseである場合、Verboseモードを起動します。デフォルト値はFalseです | Boolean | いいえ |
| Object |DELETE |各削除するターゲットオブジェクト情報を説明します| Container | はい |
| Key | DELETE.Object |ターゲットオブジェクトファイル名称| String | はい |


## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。
#### 特有の応答ヘッダー
このリクエスト操作には、特別な応答ヘッダーがありません。

### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：
```shell
<DeleteResult>
  <Deleted>
    <Key></Key>
  </Deleted>
  <Error>
    <Key></Key>
    <Code></Code>
    <Message></Message>
  </Error>
</DeleteResult>
```
具体的な内容は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:---|:---|:---|
| DeleteResult |無し| 今回の削除結果を返す方式とターゲットオブジェクトを説明します | Container | 

コンテナノードDeleteResultの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:---|:---|:---|
| Deleted | DeleteResult |今回削除に成功したObject情報を説明します | Boolean | 
| Error| DeleteResult | 今回削除に失敗したオブジェクト情報を説明します | Container | 

コンテナノードDeleted内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:---|:---|:---|
| Key | DeleteResult.Deleted | オブジェクトの説明 | String |

コンテナノードエラー内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:---|:---|:---|
| Key | DeleteResult.Error | 削除に失敗したオブジェクトの名称 | String |
| Code  | DeleteResult.Error | 削除に失敗したエラーコード | String |
Message | DeleteResult.Error | 削除に失敗したエラー情報 | String |


### エラー分析
このリクエストが発生する可能性がある特別、且つ一般的なエラー状況は以下のとおりです：

|エラーコード            |HTTPステータスコード         |説明                                       |
| ------------- | --------------------------------------- | -------------- |
| InvalidRequest | 400 Bad Request |必須フィールドContent-MD5が持っていません。同時に`Missing required header for this request: Content-MD5`エラー情報を返します | 
| MalformedXML   | 400 Bad Request |もしリクエストされたキーの数は1000を超えると、MalformedXMLエラーを返します。その同時に`delete key size is greater than 1000`を返します | 
| InvalidDigest  | 400 Bad Request |持っているContent-MD5とサーバーの計算されたリクエストボディと一致しません          | 


COSエラーコード情報、または製品のすべてのエラーリストの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

## 実際のケース

### リクエスト
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: yoLiNjQuvB7lu8cEmPafrQ==
Content-Length: 125

<Delete>
  <Quiet>true</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 17
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:00:48 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzFjZjBfZWFhZDM1MGFfMjkwZV9lZGM3ZQ==

<DeleteResult/>
```

### リクエスト
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Tue, 22 Aug 2017 12:16:35 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: V0XuU8V7aqMYeWyD3BC2nQ==
Content-Length: 126

<Delete>
  <Quiet>false</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### 応答
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 111
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:16:35 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzIwYTNfMzFhYzM1MGFfMmNmOWZfZWVhNjQ=

<DeleteResult>
 <Deleted>
  <Key>aa</Key>
 </Deleted>
 <Deleted>
  <Key>aaa</Key>
 </Deleted>
</DeleteResult>
```



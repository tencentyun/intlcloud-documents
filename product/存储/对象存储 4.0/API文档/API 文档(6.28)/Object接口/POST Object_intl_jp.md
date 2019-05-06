## 機能説明
POST Object APIリクエストにより、ユーザーはファイル（オブジェクト）をフォームの形で指定されたバケットにアップロードすることができます。この操作では、リクエスト者はバケットに対する書き込み権限を持っている必要があります。HTTPヘッダーに含めるすべてのAPIパラメータは、フォームフィールドを使用してリクエストされます。

### バージョン

バケットに対して、バージョン制御を有効にする場合、POST操作は追加されるオブジェクトに一意のバージョンIDを自動的に生成します。COSは、x-cos-version-id応答ヘッダーを使用してこの識別子を応答中に返します。
バケットのバージョン制御を一時停止する必要がある場合、COSはそのnullをバケットに格納されているオブジェクトのバージョンIDとして常に使用します。

### 詳細分析
1. バケットの書き込み権限が必要です。
2. 追加しようとしているオブジェクトと同じ名前のファイルがすでに存在する場合、新しくアップロードされたファイルは元のファイルを上書きし、成功した場合は200 OKを返します。

## リクエスト
### リクエスト例

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Headers
Form
```

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。の詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728 "公共请求头部")ドキュメントを参照してください。

#### 非共通のヘッダー
該当リクエスト操作は以下の必須リクエストヘッダーが必要です：

|名称|説明|タイプ| 必須項目|
|:---|:-- |:---|:-- |
| Content-Length | RFC 2616の中で定義されたHTTPリクエスト内容の長さ（バイト）|String| はい|

### フォームフィールド

<table>
   <tr>
      <th>名称</td>
      <th>説明</td>
      <th>タイプ</td>
      <th>必須項目</td>
   </tr>
   <tr>
      <td>acl</td>
      <td>オブジェクトのACL属性を定義します。有効値：private、public-read、default；デフォルト値：default（バケット権限を継承します）；<br>注意：現時点でアクセスポリシーエントリは1000に制限されています。Object ACLコントロールが不要な場合は、defaultを入力するか、この項目を設定しないでください。デフォルトでは、バケット権限を継承します</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires</td>
      <td>RFC 2616で定義されたヘッダーの詳細について、<a href="https://cloud.tencent.com/document/product/436/7749">PUT Object</a>ドキュメント</td>を参照してください
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>file</td>
      <td>ファイルの内容はフォームの最後のフィールドとして取り扱います</td>
      <td>String</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>key</td>
      <td>アップロードされたファイル名、$ {filename}を使用して置き換えます。例えば、a/b/${filename}、ファイルphoto.jpgをアップロードすると、最終的なアップロードパスはa/b/photo.jpgになります</td>
      <td>String</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>success_action_redirect</td>
      <td>優先有効を設定した場合、303を返し、ロケーションヘッダーを提供し、URLの末尾にbucket={bucket}&key={key}&etag={%22etag%22} パラメータを追加します</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>success_action_status</td>
      <td>200、201、204を選択できます。デフォルトでは204を返します。success_action_redirectを入力すると、この設定を無視します</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>ユーザー定義ヘッダーサフィックスとユーザー定義ヘッダー情報がObjectメタデータとして返されます。サイズ制限は2 KBです。注意：ユーザー定義ヘッダー情報はアンダースコアをサポートしますが、ユーザー定義ヘッダーサフィックスはアンダースコアをサポートしません</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>x-cos-storage-class</td>
      <td>Objectのストレージレベルを設定します。列挙値：STANDARD、STANDARD_IA、デフォルト値：STANDARD</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>policy</td>
      <td>Base64エンコード。リクエストチェックのために使用されます。もしリクエスト内容はPolicyが指定された条件と一致していなければ、403 AccessDeniedを返します</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>x-cos-server-side-encryption</td>
      <td>オブジェクトにサーバーの暗号化を有効にする方法を指定します。COSマスタ暗号鍵で暗号化する場合、AES256を入力します</td>
      <td>String</td>
      <td nowrap="nowrap">暗号化が必要な場合、是</td>
   </tr>
</table>

#### 署名保護

フォームでHTTP POSTリクエストをアップロードする際に、署名保護が必要な場合、フォームには次の内容構造form-dataを含める内容が必要です：

| フォームフィールド         | 説明                                                         |
| ---------------- | ----------------------------------------- |
| policy           | Base64暗号化されたポリシー内容。ポリシー内容はリクエスト内容を検査するために使用されます。リクエスト内容がポリシー指定の条件に一致しない場合、リクエストは拒否されます。|
| q-sign-algorithm | 署名計算に使用されるアルゴリズム、Tencent Cloud COSは現在SHA1をサポートしています。ここでは小文字の`sha1`を入力します。|
| q-ak             | Tencent Cloudのアカウント暗号鍵IDはSecretIdです                     |
| q-key-time      | 署名をリクエストするために使用された暗号鍵の有効な開始時刻と終了時刻。Unixタイムスタンプにより開始時刻と終了時刻（秒単位）を説明します。フォーマットは[start-seconds];[end-seconds]。例えば、`1480932292;1481012298` |
| q-signature      | 上記の要素によって計算されたリクエスト署名を使用して、COSはフォーム要素と署名内容を使用して検証します。署名が署名された内容と一致しない場合、リクエストは拒否されます |

#### 署名計算

署名q-signatureの計算は3つのステップがあります：

1. 暗号鍵内容を使用して、q-key-timeの時間値に対して値SignKeyの計算を暗号化します。
2. POSTリクエストポリシーを作成し、内容をsha1暗号化してStringToSignを取得します。
3. SignKeyを使用してStringToSignに対して暗号化して、署名を生成します。

#### Policy
以下は完全なポリシーの例です：

```shell
{ "expiration": "2007-12-01T12:00:00.000Z",
  "conditions": [
    {"acl": "public-read" },
    {"bucket": "examplebucket-1250000000" },
    ["starts-with", "$key", "user/eric/"],
    {"q-sign-algorithm": "sha1" },
    {"q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q" },
    {"q-sign-time": "1480932292;1481012298" }
  ]
}
```

**Expiration**
ISO8601 GMT時間を使用してこのPOST Policyのタイムアウトを設定します。例えば、2017-12-01T12:00:00.000Z。

**Conditions規則**

| タイプ   | 説明                                       |
| ---- | ---------------------------------------- |
| 完全マッチ | `{"key": "value"}`または`["eq", "$key", "value"]`方式で表現します |
| プレフィックスマッチ | `["starts-with", "$key", "value"]`方式で表現します。valueはブランクにすることができます |
| 範囲マッチ | `["content-length-range", int1, int2]`の場合のみを使用します。ファイルのバイト数はint1とint2の範囲内でなければなりません|

**Conditionsパラメータ**
すべてのパラメータはオプションであり、入力されていない場合は検証しません。

| 名称             | 説明             | マッチ方式  |
| --------------- | ---------------------- | ----- |
| acl                     | ファイルACL属性の許容範囲。空白可                       | 完全、プレフィックス |
| bucket                  | アップロードするBucketを指定します                             | 完全    |
| content-length-range    | ファイルのアップロードサイズの範囲を指定します                              | 範囲    |
| key                     | オブジェクトのストレージパス                                  | 完全、プレフィックス |
| success_action_redirect | アップロード成功してから返されたURL                             | 完全、プレフィックス |
| success_action_status   | アップロード成功してから返されたステータス                               | 完全    |
| x-cos-meta-\*            | ユーザー定義ヘッダーサフィックスとユーザー定義ヘッダー情報がObjectメタデータとして返されます。サイズ制限は2 KBです。<br>**注意：**ユーザー定義ヘッダー情報はアンダースコアをサポートしますが、ユーザー定義ヘッダーサフィックスはアンダースコアをサポートしません  | 完全、プレフィックス |
| x-cos-\*      | 他の署名が必要なCOSヘッダー            | 完全    |


## 応答
### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー
該当リクエストは以下の応答ヘッダーを返します：

|名称|説明|タイプ|
|:---|:-- |:-- |
|success_action_redirect|アップロードが成功したときにクライアントがリダイレクトされたURL|String|
|x-cos-version-id|ターゲットバケットでオブジェクトのバージョンをコピーします。有効にするかまたは有効にしてから一時停止しているバケットは、このヘッダーに応答します|String|
|x-cos-server-side-encryption|オブジェクトがCOS管理のサーバー暗号化によって保存されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値を含めます：AES256|string|


### 応答パラメータ
|名称|説明|タイプ|
|:---|:-- |:-- |
| ETag| ファイルのMD5アルゴリズムチェック値を返します。ETagの値を使用して、アップロード処理中にオブジェクトが破損していないかどうかを確認できます|String|
| Location| upload success_action_redirectのアップロードを指定した場合、対応する値を返し、指定しない場合、オブジェクトの完全のパスを返します|String|


### 応答ボディ
この応答ボディはapplication/xmlデータとして返され、完全なノードデータを含む内容は以下のようになります：

```shell
<PostResponse>
        <Location>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg</Location>
        <Bucket>examplebucket-1250000000</Bucket>
        <Key>photo.jpg</Key>
        <ETag>d41d8cd98f00b204e9800998ecf8427e</ETag>
</PostResponse>
```

具体的なデータ説明は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:-- |:--|:--|:--|
| PostResponse |無し| POST Objectの結果を保存するコンテナー | Container |はい|

コンテナノードPostResponse内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:-- |:--|:--|:--|
| Location | PostResponse | オブジェクトの完全パス |  String |はい|
| Bucket | PostResponse | オブジェクトの所属するバケット |  String |はい|
| Key | PostResponse | オブジェクトkey名 |  String |はい|
| ETag | PostResponse | Etag内容 |  String |はい|

###　エラーコード
以下は、このリクエストで発生する可能性がある特殊で一般的なエラー状況を説明します。COSエラーコードの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

| エラーコード                  |   HTTPステータス コード                                      |    説明       |
| ------------------- | --------------------------------------- | ------------------ |
| InvalidDigest        |400 Bad Request     | ユーザーがContent-MD5ヘッダーを含むファイルをアップロードすると、COSはボディのMd5はユーザーが持っているMD5と一致であることを確認します。一致しなければInvalidDigestを返します |
| KeyTooLong           |400 Bad Request     | ファイルをアップロードするときに含める、x-cos-metaで始まるカスタムヘッダー、各カスタムヘッダーのkeyとvalueは合計で4kを超えてはいけません。そうではなければ、KeyTooLongエラーを返します |
| MissingContentLength | 411 Length Required |ファイルのアップロード時にContent-Lengthヘッダーが追加されていないと、該当エラーコードが返されます     |
| NoSuchBucket         | 404 Not Found       |追加しようとしているObjectが所属するBucketが存在しない場合、404 Not Foundエラーを返します。エラーコード：NoSuchBucket |
| EntityTooLarge       | 400 Bad Request     |追加されたファイルが5Gより長い場合は、EntityTooLargeを返して、エラーメッセージ`“Your proposed upload exceeds the maximum allowed object size”`を返します|
| InvalidURI           | 400 Bad Request     | オブジェクトkeyの長さは850に制限されています。これが850を超えると、InvalidURIが返されます      |


## 実際のケース
### リクエスト

```
POST / HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1352
Content-Type: multipart/form-data; boundary=e07f2a7876ae4755ae18d300807ad879

--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key"

a/${filename}
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="success_action_status"

201
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Acl"

public-read
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-cos-storage-class"

STANDARD
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Signature"

q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1512983814;1512984814&q-key-time=1512983814;1512984814&q-url-param-list=&q-header-list=host&q-signature=2ffd2ae714e7445a8da000ec5d51771ff5056500
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogImtpdG1hbnMzdGVzdDEifSwgWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsIDAsIDEwMDAwMDAwXSwgWyJzdGFydHMtd2l0aCIsICJ4LWNvcy1tZXRhLWJiIiwgIjEyIl1dLCAiZXhwaXJhdGlvbiI6ICIyMDQ3LTEyLTAxVDEyOjAwOjAwLjAwMFoifQ==
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-Cos-meta-bb"

124
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key1"

1
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="file"; filename="empty:a"


--e07f2a7876ae4755ae18d300807ad879--
```

### 応答

```shell
HTTP/1.1 204
Content-Type: application/xml
Content-Length: 232
Connection: keep-alive
Date: Mon, 11 Dec 2017 09:16:56 GMT
ETag: "d41d8cd98f00b204e9800998ecf8427e"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg
Server: tencent-cos
x-cos-request-id: NWEyZTRkMDZfMjQ4OGY3MGFfNTE4Yl81
```


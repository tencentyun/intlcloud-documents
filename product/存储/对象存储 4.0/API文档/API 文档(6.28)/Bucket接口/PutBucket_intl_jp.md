## 機能説明
PUT Bucket APIリクエストは指定されたアカウントでバケットを作成することができます。このAPIは匿名リクエストをサポートしていません。新しいバケットを作成するには、Authorization署名認証付きのリクエストを使用する必要があります。バケットを作成したユーザーは、デフォルトでバケットの所有者になります。
### 詳細分析
1.バケットを作成するとき、アクセス権限を指定していない場合は、デフォルトでプライベートの読み書き（private）権限を使用します。

## リクエスト

文法の例：
```
PUT / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエスト行
~~~
PUT / HTTP/1.1
~~~
APIはPUTリクエストを受け付けます。

### リクエストヘッダー

**パブリックヘッダー**
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

**非パブリックヘッダー**
このリクエスト操作の実現では、PUTリクエストのx-cos-aclヘッダーによってバケットアクセス権限を設定できます。現時点では、3種類のバケットアクセス権限があります：public-read-write、public-readとprivate。設定しなければ、デフォルトではprivate権限です。ユーザーに読み取り、書き込み、または読み書き権限を明示的に付与することもできます。内容は以下のとおりです：
>aclリクエストの詳細について、[Put Bucket ACL](https://cloud.tencent.com/document/product/436/7737)ドキュメントを参照似てください。

|名称|説明|タイプ|必須項目|
|:---|:-- |:--|:--|
| x-cos-acl | オブジェクトのacl属性を定義します。有効値：private、public-read-write、public-read；デフォルト値：private | String|  いいえ |
| x-cos-grant-read | 権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "；<br/>サブアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"，<br/>ルートアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" | String |  いいえ |
| x-cos-grant-write | 権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "；<br/>サブアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"，<br/>ルートアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" | String |  いいえ |
| x-cos-grant-full-control | 権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "；<br/>サブアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"，<br/>ルートアカウントに権限を付与するとき、id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" | String |  いいえ |

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。
### 応答ボディ
この応答ボディは空を返します。
### エラー分析
このリクエストが発生する可能性がある特別、且つ一般的なエラー状況は以下のとおりです：

|エラーコード|HTTPステータスコード|説明|
|--------|--------|--------------|
| BucketAlreadyExists |409 Conflict|リクエストで作成されたバケットが存在しており、且つ、リクエストで作成されたユーザーが所有者です| 
| InvalidBucketName | 400 Bad Request|バケットの名前は標準ではありません。具体的な原因について、メッセージの説明を参照してください|
| InvalidRequest | 400 Bad Request|バケットの名前は標準ではありません。具体的な原因について、メッセージの説明を参照してください| 
バケットによって設定されたACLが正しくない場合も、バケットの作成に失敗し、「Failed to set access control authority for the bucket」というエラーメッセージが返されます。具体的なエラー原因について、返したエラーコードに基づき、[Put Bucket ACL](https://cloud.tencent.com/document/product/436/7737)の関連するドキュメントを参照してください

COSエラーコード情報、または製品のすべてのエラーリストの詳細については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

## 実際のケース

### リクエスト
```
PUT / HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2016 19:12:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484708728;32557604728&q-key-time=1484708728;32557604728&q-header-list=host&q-url-param-list=&q-signature=b394a86624cbcc705b11bc6fc505843c5e2dd9c9
```

### 応答
```
HTTP /1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 12 Jan 2016 19:12:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZWRiODJfOWIxZjRlXzZmNDBfMTUz

```



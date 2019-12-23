## 機能説明
PUT Object - Copyリクエストは、ソースパスからターゲットパスにファイルをコピーすることを実装します。ファイルサイズは1M - 5Gで、5Gを超えるファイルは、Upload - Copyマルチパートアップロードを使用してください。ファイル要素の属性とACLは、コピー処理中に変更できます。
ユーザーはこのAPIを使用して、ファイルの移動、ファイル名の変更、ファイル属性の変更、およびコピーの作成を実行できます。

### バージョン

デフォルトでは、ターゲットバケットでバージョン制御を有効にして、オブジェクトストレージはコピー中のオブジェクトに一意のバージョンIDを生成します。このバージョンIDは、ソースオブジェクトのバージョンIDとは異なります。COSは、x-cos-version-id応答の応答ヘッダーにコピーされたオブジェクトのバージョンIDを返します。
ターゲットバケットでバージョン制御を有効にしたりバージョン制御を一時停止したりしない場合、COSによって生成されたバージョンIDは常にnullになります。

>!クロスアカウントでコピーする場合は、コピーされたファイルの権限をパブリック読み取りに設定するか、またはターゲットアカウントに対して、権限を付与する必要があります。同じアカウントは設定する必要がありません。

## リクエスト
### リクエスト例

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
x-cos-copy-source: <BucketName-APPID>.cos.<Region>.myqcloud.com/filepath
```

>Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）。


### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー

名称|説明|タイプ|必須項目
---|---|---|---
x-cos-copy-source|ソースファイルURLパス、versionidサブリソースを通して、履歴バージョンを指定します|string|はい
X-cos-metadata-directive|ソースファイルのメタデータをコピーするかどうか、列挙値：Copy、Replaced、デフォルト値はCopyです。マークがCopyの場合、ソースファイルのメタデータをコピーし、マークがReplacedの場合、今回リクエストヘッダー情報に従ってメタデータを変更します。ターゲットパスとソースパスが一致する場合、つまりユーザーがメタデータを変更しようとしている時、マークがReplacedである必要があります|string|いいえ
x-cos-copy-source-If-Modified-Since|指定された時間後、オブジェクトが変更されると、操作を実行します。そうではなければ、412を返します。x-cos-copy-source-If-None-Matchと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します|string|いいえ
x-cos-copy-source-If-Unmodified-Since|指定された時間後、オブジェクトが変更されていなければ、操作を実行します。そうではなければ、412を返します。x-cos-copy-source-If-Matchと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します|string|いいえ
x-cos-copy-source-If-Match|オブジェクトのEtagが指定と一致する場合、操作を実行します。そうではなければ、412を返します。x-cos-copy-source-If-Unmodified-Sinceと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します|string|いいえ
x-cos-copy-source-If-None-Match|オブジェクトのEtagが指定と一致する場合、操作を実行します。そうではなければ、412を返します。x-cos-copy-source-If-Modified-Sinceと一緒に使用可能です。他の条件と合わせて使用すれば、競合を返します|string|いいえ
x-cos-storage-class|オブジェクトのストレージレベルを設定します、列挙値：STANDARD、STANDARD_IA。デフォルト値：STANDARD|string|いいえ
x-cos-acl|オブジェクトのACL属性を定義します。有効値：private、public-read；デフォルト値：private|string|いいえ
x-cos-grant-read |権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id="[OwnerUin]"|string|いいえ
x-cos-grant-write| 権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id="[OwnerUin]"|string|いいえ
x-cos-grant-full-control | 権限が付与された者にすべての権限を付与します。フォーマット：x-cos-grant-full-control: id="[OwnerUin]"|string|いいえ
x-cos-meta-\*|ユーザー定義ヘッダーサフィックスとユーザー定義ヘッダー情報がオブジェクトメタデータとして返されます。サイズ制限は2 KBです。<br>**注意：**ユーザー定義ヘッダー情報はアンダースコアをサポートしますが、ユーザー定義ヘッダーサフィックスはアンダースコアをサポートしません|string|いいえ

**サーバーの暗号化による関連ヘッダー**

このリクエスト操作は、Tencent Cloud COSがデータストレージを行う場合、アプリケーションデータ暗号化の保護ポリシーを指定します。Tencent Cloud COSは、データーをデーターセンターに書き込むときに自動的に暗号化し、アクセスするとき、自動的に復号化するのに役立ちます。現時点では、Tencent Cloud COSマスタ暗号鍵を使用してデーターに対してAES-256暗号化することをサポートしています。データーに対してサーバーの暗号化を有効にする必要があれば、以下のヘッダーを渡しなければいけません：

| 名称         | 説明          | タイプ     | 必須項目     |
| --------- | ---------- | ------ | ------ |
| x-cos-server-side-encryption | オブジェクトにサーバーの暗号化を有効にする方法を指定します。<br/>COSマスタ暗号鍵暗号化を使用して入力します：AES256 | String | 暗号化必要があれば、はい |

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー

| 名称         | 説明          | タイプ     |
| --------- | ---------- | ------ |
|x-cos-version-id|ターゲットバケットでオブジェクトのバージョンをコピーします。有効にするかまたは有効にしてから一時停止しているバケットでなければ、このパラメータに応答しません|String|
|x-cos-server-side-encryption|オブジェクトがCOS管理のサーバー暗号化によって保存されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値を含めます：AES256。 | String |

### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：

```shell
<CopyObjectResult>
    <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
    <LastModified>2017-08-04T02:41:45</LastModified>
</CopyObjectResult>
```

具体的なデータ内容は以下のとおりです：

| 名称               | 説明                                       | タイプ     |
| ---------------- | ---------------------------------------- | ------ |
| CopyObjectResult | コピー結果情報を返します                                 | String |
| ETag             | ファイルのMD5アルゴリズムチェック値を返します。ETagの値を使用して、オブジェクトの内容が変更されたかどうかを確認できます。| String |
| LastModified     | ファイルの最後の変更時間を返します。GMTフォーマット                        | String |


## 実際のケース

### リクエスト

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 04 Aug 2017 02:41:45 GMT
Connection: keep-alive Accept-Encoding: gzip, deflate Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=&q-header-list=host&q-signature=eacefe8e2a0dc8a18741d9a29707b1dfa5aa47cc
x-cos-copy-source: sourcebucket-1250000001.cos.ap-beijing.myqcloud.com/picture.jpg
Content-Length: 0
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133
Connection: keep-alive
Date: Fri, 04 Aug 2017 02:41:45 GMT
Server: tencent-cos
x-cos-request-id: NTk4M2RlZTlfZDRiMDM1MGFfYTA1ZV8xMzNlYw==

<CopyObjectResult>
    <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
    <LastModified>2017-08-04T02:41:45</LastModified>
</CopyObjectResult>
```




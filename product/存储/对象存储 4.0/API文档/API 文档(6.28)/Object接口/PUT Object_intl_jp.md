## 機能説明
PUT Object APIリクエストは、ローカルオブジェクト（Object）を指定されたバケットにアップロードできます。この操作について、リクエスト者がバケットへの書き込み権を持っている必要があります。

### バージョン

バケットに対して、バージョン制御を有効にする場合、COSは追加されるオブジェクトに一意のバージョンIDを自動的に生成します。オブジェクトストレージは、x-cos-version-id応答ヘッダーを使用してこの識別子を応答中に返します。
バケットのバージョン制御を一時停止する必要がある場合、COSはそのnullをバケットに格納されているオブジェクトのバージョンIDとして常に使用します。

### 詳細分析
1. バケットの書き込み権限が必要です。
2. リクエストヘッダーのContent-Length値が実際のリクエストボディ（body）で送信されたデーターの長さより小さい場合でも、COSはファイルを正常に作成しますが、オブジェクトのサイズはContent-Lengthで定義されたサイズと等しいだけで、他のデーターが破棄されます。
3. 追加しようとしているオブジェクトと同じ名前のファイルがすでに存在する場合、新しくアップロードされたファイルは元のファイルを上書きし、成功した場合は200 OKを返します。

## リクエスト
### リクエスト例

```shell
PUT /<ObjectName> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー
該当操作を実現するには、以下のリクエストヘッダーを使用することもできます。

名称|説明|タイプ|必須項目
---|---|---|---
Content-Disposition|RFC 2616で定義されたファイル名称は、オブジェクトメタデータとして保存されます|string|いいえ
Content-Encoding|RFC 2616で定義されたエンコードフォーマットは、オブジェクトメタデータとして保存されます|string|いいえ
Expect|Expect: 100-continueを使用する場合、サーバーから承認を受け取らないと、リクエスト内容を送信しません|string|いいえ
Expires|RFC 2616で定義されたキャッシュポリシーは、オブジェクトメタデータとして保存されます|string|いいえ
x-cos-meta-\*|ユーザー定義ヘッダーサフィックスとユーザー定義ヘッダー情報がオブジェクトメタデータとして返されます。サイズ制限は2 KBです。<br>**注意：**ユーザー定義ヘッダー情報はアンダースコアをサポートしますが、ユーザー定義ヘッダーサフィックスはアンダースコアをサポートしません。|string|いいえ
x-cos-storage-class|オブジェクトのストレージレベルを設定します、列挙値：STANDARD、STANDARD_IA。デフォルト値：STANDARD|string|いいえ
x-cos-acl|オブジェクトのACL属性を定義します。有効値：private、public-read-write、public-read、default；デフォルト値：default（バケット権限を継承します）；注：現時点でアクセスポリシーエントリは1000に制限されています。Object ACLコントロールが不要な場合は、defaultを入力するか、この項目を設定しないでください。デフォルトでは、バケット権限を継承します。|string|いいえ
x-cos-grant-read |権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id="[OwnerUin]"| String |  いいえ 
x-cos-grant-write| 権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id="[OwnerUin]"|String |  いいえ 
x-cos-grant-full-control | 権限が付与された者にすべての権限を付与します。フォーマット：x-cos-grant-full-control: id="[OwnerUin]"|String| いいえ 

#### サーバーの暗号化に関連するヘッダー

このリクエスト操作は、Tencent Cloud COSがデータストレージを行う場合、アプリケーションデータ暗号化の保護ポリシーを指定します。Tencent Cloud COSは、データーをデーターセンターに書き込むときに自動的に暗号化し、アクセスするとき、自動的に復号化するのに役立ちます。現時点では、Tencent Cloud COSマスタ暗号鍵を使用してデーターに対してAES-256暗号化することをサポートしています。データーに対してサーバーの暗号化を有効にする必要があれば、以下のヘッダーを渡しなければいけません：

| 名称        | 説明    | タイプ     | 必須項目     |
| --------- | --------- | ------ | ------ |
| x-cos-server-side-encryption | オブジェクトにサーバーの暗号化を有効にする方法を指定します。<br/>COSマスタ暗号鍵暗号化を使用して入力します：AES256 | String | 暗号化必要があれば、はい |

### リクエストボディ
このリクエストのリクエストボディはオブジェクトファイル内容です。

## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー

このリクエスト操作の応答ヘッダーの具体的なデータは：

|名称|タイプ|説明|
|---|---|---|
|ETag|string|アップロードファイル内容のMD5値|
|x-cos-version-id|string|オブジェクトのバージョンを返します
|x-cos-server-side​-encryption|string|オブジェクトがCOS管理のサーバー暗号化によって保存されている場合、応答にはこのヘッダーの値と使用されている暗号化アルゴリズムの値を含めます：AES256。|

### 応答ボディ
このリクエストの応答ボディはブランクです。

###　エラーコード
このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、 [エラーコード](https://cloud.tencent.com/document/product/436/7730) ドキュメントを参照してください。

## 実際のケース

### リクエスト

```shell
PUT /picture.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484639384;32557535384&q-key-time=1484639384;32557535384&q-header-list=host&q-url-param-list=&q-signature=5c07b7c67d56497d9aacb1adc19963135b7d00dc
Content-Length: 64

[Object]
```

### 応答

```shell
HTTP/1.1200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed,16 Aug 2017 11: 59: 33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```




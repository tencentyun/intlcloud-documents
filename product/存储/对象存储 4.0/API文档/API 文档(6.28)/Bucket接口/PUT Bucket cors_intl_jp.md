## 機能説明
PUT Bucket cors APIは、Bucketのクロスオリジンリソース共有権限の設定をリクエストするために使用されます。XMLフォーマットの構成ファイルを渡すことで構成できます。ファイルサイズの上限が64 KBです。デフォルトでは、Bucketの所有者はAPIに直接アクセスでき、Bucket所有者は他のユーザーに権限を付与できます。

## リクエスト
リクエスト例：

```
PUT /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

<XML file>
```
> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエスト行

```
PUT /?cors HTTP/1.1
```

APIは `PUT` リクエストを受け付けます。


### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728 "公共请求头部") セクションを参照してください。

#### 非共通のヘッダー


このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ
リクエストのリクエストボディはクロスオリジン規則です。
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
  <CORSRule>
    <ID>string</ID>
    <AllowedOrigin>string</AllowedOrigin>
    <AllowedMethod>string</AllowedMethod>
    <AllowedHeader>string</AllowedHeader>
    <MaxAgeSeconds>0</MaxAgeSeconds>
    <ExposeHeader>string</ExposeHeader>
  </CORSRule>
</CORSConfiguration>
```


具体的なデータ説明は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|---|---|---|---|---|
|CORSConfiguration|無し|クロスオリジンリソース共有構成のすべての情報を説明します。最大100個のCORSRuleを含めることができます。|Container|はい|

コンテナノードCORSConfigurationの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|---|---|---|---|
|CORSRule|CORSConfiguration|クロスオリジンリソース共有構成のすべての情報を説明します。最大100個のCORSRuleを含めることができます。|Container|はい|

コンテナノードCORSRuleの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|---|---|---|---|---|
|ID|CORSConfiguration.CORSRule|構成規則のID、オプション|string|はい|
|AllowedOrigin|CORSConfiguration.CORSRule|許可されたアクセスソース、ワイルドカード * をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]例えば：http://www.qq.com|strings|strings|はい|
|AllowedMethod|CORSConfiguration.CORSRule|許可されたHTTP操作、列挙値：GET、PUT、HEAD、POST、DELETE|strings|はい|
|AllowedHeader|CORSConfiguration.CORSRule|OPTIONSリクエストを送信するときに、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知します。ワイルドカード *をサポートします|strings|はい|
|MaxAgeSeconds|CORSConfiguration.CORSRule|オプションリクエストが取得される結果の有効期間を設定します|integer|はい|
|ExposeHeader|CORSConfiguration.CORSRule|ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します|strings|はい|


## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729"公共响应头部")セクションを参照してください。

#### 特有の応答ヘッダー


このリクエスト操作には、特別な応答ヘッダー情報はありません。

### 応答ボディ
このリクエストの応答ボディはブランクです。

###　エラーコード

|エラーコード|説明|HTTPステータスコード|
|---|---|---|
|SignatureDoesNotMatch|提供された署名は規則に適合しません。このエラーコードを返します|403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
NoSuchBucket|追加しようとしている規則が所属するバケットが存在しない場合、このエラーコードを返します|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)

## 実際のケース

### リクエスト

```
PUT /?cors HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2017 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=cors&q-signature=8b9f05dabce2578f3a79d732386e7cbade9033e3
Content-Type: application/xml
Content-Length: 280

<CORSConfiguration>
    <CORSRule>
        <ID>1234</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
    </CORSRule>
</CORSConfiguration>
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 10 Mar 2017 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdiZWRfOWExZjRlXzQ2OWVfZGY0
```




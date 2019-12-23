## 機能説明
GET Bucket cors APIは、バケット所有者がバケット上でクロスオリジンリソース共有（W3C標準。CORS：Cross-origin resource sharing）の情報構成を取得します。デフォルトでは、バケット所有者はこのAPIに直接アクセスでき、バケット所有者は他のユーザーに権限を付与できます。

## リクエスト
### リクエスト例

```
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）。

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。
#### 非共通のヘッダー
このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。

### 応答ボディ
クロスオリジンリソース共有の構成情報を取得することに成功しました。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```

具体的なデータ説明は以下のとおりです：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
CORSConfiguration|無し|クロスオリジンリソース共有構成のすべての情報を説明します。最大100個のCORSRuleを含めることができます。|Container|はい

コンテナノードCORSConfigurationの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
CORSRule|CORSConfiguration|クロスオリジンリソース共有構成のすべての情報を説明します。最大100個のCORSRuleを含めることができます。|Container|はい

コンテナノードCORSRuleの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ID|CORSConfiguration.CORSRule|構成規則のID、オプション|string|はい
AllowedOrigin|CORSConfiguration.CORSRule|許可されたアクセスソース、ワイルドカード`*`をサポートします。フォーマット：プロトコル://ドメイン名[:ポート]例えば：`http://www.qq.com`|strings|はい
AllowedMethod|CORSConfiguration.CORSRule|許可されたHTTP操作、列挙値：GET、PUT、HEAD、POST、DELETE|strings|はい
AllowedHeader|CORSConfiguration.CORSRule|オプションリクエストを送信するときに、後続のリクエストがどのカスタムHTTPリクエストヘッダーを使用できるかをサーバーに通知します。ワイルドカード *をサポートします|strings|はい
MaxAgeSeconds|CORSConfiguration.CORSRule|オプションリクエストが取得される結果の有効期間を設定します|integer|はい
ExposeHeader|CORSConfiguration.CORSRule|ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します|strings|はい


###　エラーコード
このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、[エラーコード](https://cloud.tencent.com/document/product/436/7730)セクションを参照してください。

## 実際のケース

### リクエスト

```
GET /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=cors&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 345
Connection: keep-alive
Date: Wed, 28 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFfZTBh

<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```




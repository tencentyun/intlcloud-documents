## 機能説明
GET Service APIは、リクエスト者の名配下のすべてのストレージスペースリスト（Bucket list）を取得するために使用されます。

## リクエスト
### リクエスト例

```
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>Authorization: Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照ししてください）

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
この応答は、共通応答ヘッダーを使用します。パブリック応答ヘッダーの詳細については、[パブリック応答ヘッダ](https://cloud.tencent.com/document/product/436/7729 "公共响应头部")セクションを参照してください。

#### 特有の応答ヘッダー
このリクエスト操作には、特別な応答ヘッダー情報はありません。

### 応答ボディ
照合に成功、バケット内のオブジェクト情報を含むapplication/xmlデータを返します。
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<ListAllMyBucketsResult>
  <Owner>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Owner>
  <Buckets>
    <Bucket>
      <Name>string</Name>
      <Location>string</Location>
      <CreateDate>string</CreateDate>
    </Bucket>
    <DisplayName>string</DisplayName>
  </Buckets>
</ListAllMyBucketsResult>
```

具体的なデータ説明は以下のとおりです：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ListAllMyBucketsResult|無し|今回の応答のすべての情報を説明します|Container|はい

コンテナノードListAllMyBucketsResultの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
Owner|ListAllMyBucketsResult|バケット所有者の情報|Container|はい
Buckets|ListAllMyBucketsResult|今回の応答のすべてのバケットリスト情報を説明します|Container|はい
コンテナノードオーナーの内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
ID|ListAllMyBucketsResult.Owner|バケット所有者のID|string|はい
DisplayName|ListAllMyBucketsResult.Owner|バケット所有者の名称情報|string|はい
コンテナノードバケット内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
Bucket|ListAllMyBucketsResult.Buckets|単一バケットの情報|Container|はい
DisplayName|ListAllMyBucketsResult.Buckets|バケット所有者の名称情報|string|はい
コンテナノードバケット内容：

ノード名称（キーワード）|親ノード|説明|タイプ|必須項目
---|---|---|---|---
Name|ListAllMyBucketsResult.Buckets.Bucket|バケットの名称|string|はい
Location|ListAllMyBucketsResult.Buckets.Bucket|バケットの地域。列挙値については、ap-beijing、ap-hongkong、eu-frankfurtなどの[利用可能な地域](https://cloud.tencent.com/document/product/436/6224)のドキュメントを参照してください|string|はい
CreateDate|ListAllMyBucketsResult.Buckets.Bucket|バケット作成時間。ISO8601フォーマット、例えば、2016-11-09T08:46:32.000Z|string|はい


###　エラーコード

エラーコード|説明|HTTPステータスコード
---|---|---
InvalidBucketName|バケット名称は不正です|400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)
|SignatureDoesNotMatch|提供された署名は規則に適合しません。このエラーコードを返します|403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)
NoSuchBucket|バケットが存在しない場合、エラーコードが返されます|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## 実際のケース

### リクエスト

```
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: Thu, 12 Jan 2016 19:12:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1489110340;32468694340&q-key-time=1489110340;32562006340&q-header-list=host&q-url-param-list=&q-signature=cb46d5ce6daed2d3dc0db7130a5719349760562
```

### 応答

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 19935
Connection: keep-alive
Date: Thu, 12 Jan 2016 19:12:22 GMT
Server: tencent-cos
x-cos-request-id: NThjMjA1NGFfNTViMjM1XzI0NWRfMjA4OGIx

<ListAllMyBucketsResult>
    <Owner>
     <ID>qcs::cam::uin/1147518609:uin/1147518609</ID>
     <DisplayName>1147518609</DisplayName>
    </Owner>
    <Buckets>
        <Bucket>
            <Name>01</Name>
            <Location>ap-beijing</Location>
            <CreateDate>2016-09-13 15:20:15</CreateDate>
        </Bucket>
        <Bucket>
            <Name>0111</Name>
            <Location>ap-hongkong</Location>
            <CreateDate>2017-01-11 17:23:51</CreateDate>
        </Bucket>
        <Bucket>
            <Name>1201new</Name>
            <Location>eu-frankfurt</Location>
            <CreateDate>2016-12-01 09:45:02</CreateDate>
        </Bucket>
    </Buckets>
</ListAllMyBucketsResult
```




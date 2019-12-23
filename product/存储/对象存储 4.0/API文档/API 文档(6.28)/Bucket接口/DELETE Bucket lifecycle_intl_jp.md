## 機能説明
DELETE Bucket lifecycleは、バケットのライフサイクル構成を削除するために使用されます。バケットにライフサイクル規則が設定されていない場合は、NoSuchLifecycleConfigurationが返されます。

## リクエスト
### リクエスト例
```
DELETE /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String、詳細情報については [リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778) セクションを参照してください。

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
この応答ボディはブランクです。

###　エラーコード
このリクエスト操作は、次のエラーメッセージを返します。一般的なエラーメッセージについては、 [エラーコード](https://cloud.tencent.com/document/product/436/7730) セクションを参照してください。

エラーコード|説明|HTTPステータスコード
---|---|---
None|削除に成功、応答ボディは空を返します|204 [No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)
NoSuchBucket|アクセスしたバケットが存在しない場合、このエラーコードが返されます|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## 実際のケース

### リクエスト

```
DELETE /?lifecycle HTTP/1.1
Host:lifecycletest-73196696.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:59:09 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502859472;1502939472&q-key-time=1502859472;1502939472&q-header-list=host&q-url-param-list=lifecycle&q-signature=49c1414c700643f11139219384332a3ec4e9485b
```

### 応答

```
HTTP /1.1 204 No Content
Content-Type: application/xml
Date: Wed, 16 Aug 2017 12:59:09 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDQxOWNfMjQ4OGY3Xzc3NGRfMjE=
```




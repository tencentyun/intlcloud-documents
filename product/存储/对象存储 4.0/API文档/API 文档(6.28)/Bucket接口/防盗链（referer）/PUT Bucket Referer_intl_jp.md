## 機能説明

PUT Bucket Referer APIはバケットにRefererホワイトリストまたはブラックリストを設定するために使用されます。

## リクエスト

### リクエスト例

```shell
PUT /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:GMT Date
Authorization: Auth String
Content-Length:length
Content-MD5:MD5
```

> Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。 

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)ドキュメントを参照してください。

#### 非共通のヘッダー

**必須ヘッダー**

<table>
   <tr>
      <th>名称</th>
      <th>説明</th>
      <th>タイプ</th>
      <th>必須項目</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Length</td>
      <td>RFC 2616の中で定義されたHTTPリクエスト内容の長さ（バイト）。</td>
      <td>String</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>Content-MD5</td>
      <td>RFC 1864の中で定義された、Base64エンコードされた128-bit内容MD5チェック値。このヘッダーは、ファイルの内容が変更されたかどうかを確認するために使用されます。</td>
      <td>String</td>
      <td>はい</td>
   </tr>
</table>

このリクエスト操作には、特別なリクエストヘッダー情報はありません。

### リクエストボディ

このリクエストのリクエストボディの具体的なノード内容は：

```shell
<RefererConfiguration>
  <Status></Status>
  <RefererType></RefererType>
  <DomainList>
    <Domain></Domain>
    <Domain></Domain>
  </DomainList>
  <EmptyReferConfiguration></EmptyReferConfiguration>
</RefererConfiguration>
```

具体的な説明は以下のとおりです：

| 名称                    | 親ノード               | 説明                                                         | タイプ      | 必須項目 |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration    | 無し                   | ホットリンク保護の構成情報                                               | Container | はい   |
| Status                  | RefererConfiguration | ホットリンク保護を起動するかどうか、列挙値：Eabled、Disabled                | String    | はい   |
| RefererType             | RefererConfiguration | ホットリンク保護タイプ、列挙値：Black-List、White-List               | String    | はい   |
| DomainList              | RefererConfiguration | 有効ドメイン名リスト。複数のドメイン名をサポートし、プレフィックスマッチング。ポート付きのドメイン名とIPをサポートします。ワイルドカード`* `をサポートします。セカンドレベルドメイン名またはマルチレベルドメイン名ではワイルドカードがサポートされます | Container | はい   |
| Domain                  | DomainList           | 単一の有効ドメイン名、例えば `www.qq.com/example`、`192.168.1.2:8080`、`*.qq.com` | String    | はい   |
| EmptyReferConfiguration | RefererConfiguration | 空のReferアクセスを許可するかどうか、列挙値：Allow、Deny、デフォルト値はDenyです | String    | いいえ   |


## 応答

### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを含みます。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)ドキュメントを参照してください。

#### 特有の応答ヘッダー

この応答には、特別な応答ヘッダーがありません。

### 応答ボディ

この応答ボディはブランクです。

###　エラーコード

このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、 [エラーコード](https://cloud.tencent.com/document/product/436/7730) ドキュメントを参照してください。

## 実際のケース

### リクエスト

```shell
PUT /?referer HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1547105134;32526689134&q-key-time=1547105134;32620001134&q-header-list=content-md5;content-type;host&q-url-param-list=referer&q-signature=0f7fef5b1d2180deaf6f92fa2ee0cf87ae83f0cd\
Content-MD5: kOz7g54LMJZjxKs070V9jQ==
Content-Type: application/xml

<RefererConfiguration>
  <Status>Enabled</Status>
  <RefererType>White-List</RefererType>
  <DomainList>
    <Domain>*.qq.com</Domain>
    <Domain>*.qcloud.com</Domain>
  </DomainList>
  <EmptyReferConfiguration>Allow</EmptyReferConfiguration>
</RefererConfiguration>
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```


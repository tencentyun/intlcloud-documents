## 機能説明
GET Object acl APIは、あるバケット内のあるオブジェクトへのアクセス権限を取得するために使用され、バケットの所有者だけが操作権限を持ちます。

## バージョン
デフォルトでは、このGET操作はオブジェクトの現在のバージョンを返します。別のバージョンを返す必要がある場合は、version IDサブリソースを使用してください。

## リクエスト

リクエスト例：
```
GET /ObjectName?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

### リクエスト行
~~~
GET /ObjectName?acl HTTP/1.1
~~~
APIはGETリクエストを受け付けます。

### リクエストヘッダー

#### 共通のヘッダー
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

#### 非共通のヘッダー
**必須ヘッダー**
このリクエスト操作の実現では、以下の必須ヘッダーを使用します：

|名称|説明|タイプ|必須項目|
|:---|:-- |:--|:--|
| Authorization | 署名文字列 |String| はい |

### リクエストボディ
このリクエストのリクエストボディはブランクです。

## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー 
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。
### 応答ボディ
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：

```
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
    <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
      <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
      <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
      </Grantee>
      <Permission></Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
        <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
      </Grantee>
      <Permission></Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

具体的なデータ内容は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| AccessControlPolicy |無し| GET Object ACL結果を保存するコンテナ | Container |

コンテナノードAccessControlPolicyの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| Owner | AccessControlPolicy | オブジェクト所有者情報 |  Container |
| AccessControlList | AccessControlPolicy | 権限が付与された者情報と権限情報 |  Container |

コンテナノードオーナーの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| ID | AccessControlPolicy.Owner |  オブジェクト所有者ID，</br>フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; ルートアカウントであれば、&lt;OwnerUin&gt; と &lt;SubUin&gt;は同じ値です |  String |
| DisplayName | AccessControlPolicy.Owner |  オブジェクト所有者名称 |  String |

コンテナノードAccessControlListの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| Grant | AccessControlPolicy.AccessControlList | 単一オブジェクトの認証情報。1つのAccessControlListは100個のGrantを持つことができます | Container    |

コンテナノードGrantの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 権限が付与された者情報を説明します。タイプはRootAccountまたはSubaccountであってもよい；タイプはRootAccountであれば、IDで指定されたのはルートアカウントです；タイプはSubaccountであれば、IDで指定されたのはサブアカウントです| Container    |
| Permission | AccessControlPolicy.AccessControlList.Grant | 付与された権限情報を示します、列挙値：READ、WRITE、FULL_CONTROL  | String    |

コンテナノードGranteeの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | AccessControlPolicy.Owner | ユーザーのID、ルートアカウントであれば、フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt; または  qcs::cam::anyone:anyone （すべてのユーザーを指します）サブアカウントであれば、フォーマットは： qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;|  String |
| DisplayName | AccessControlPolicy.Owner |  ユーザー名称 |  String |


## 実際のケース

### リクエスト1
```
GET /ObjectName?acl HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b40652
```

### 応答1
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 266
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==

<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/12345:uin/12345</ID>
    <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/12345:uin/12345</ID>
        <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/54321:uin/54321</ID>
        <DisplayName>qcs::cam::anyone:anyone</DisplayName>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```


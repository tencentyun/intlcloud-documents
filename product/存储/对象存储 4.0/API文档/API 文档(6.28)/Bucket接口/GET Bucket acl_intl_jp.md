## 機能説明
GET Bucket acl APIは、バケットのアクセス権限制御リストを取得するために使用されます。

## リクエスト
### リクエスト例

```
GET /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization：Auth String（詳細については、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）

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
この応答ボディは **application/xml** データとして返され、完全なノードデータを含む内容は以下のようになります：

```
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
    <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:type=\"CanonicalUser\">
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
        <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:type=\"Group\">
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

具体的なデータ内容は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| AccessControlPolicy |無し| Get Bucket ACL結果を保存するコンテナ | Container |

コンテナノードAccessControlPolicyの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| Owner | AccessControlPolicy | バケット所有者情報 |  Container |
| AccessControlList | AccessControlPolicy | 権限が付与された者情報と権限情報 |  Container |

コンテナノードオーナーの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|
|:---|:-- |:--|:--|
| ID | AccessControlPolicy.Owner |  バケット所有者ID、</br>フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; ルートアカウントであれば、&lt;OwnerUin&gt; と &lt;SubUin&gt; は同じ値です |  String |
| DisplayName | AccessControlPolicy.Owner |  バケット所有者名称 |  String |

コンテナノードAccessControlListの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| Grant | AccessControlPolicy.AccessControlList | 単一バケットの認証情報。1つのAccessControlListは100個のGrantを持つことができます | Container    |

コンテナノードGrantの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 権限が付与された者情報を説明します。タイプはRootAccountまたはSubaccountであってもよい；タイプはRootAccountであれば、IDで指定されたのはルートアカウントです；タイプはSubaccountであれば、IDで指定されたのはサブアカウントです  | Container    |
| Permission | AccessControlPolicy.AccessControlList.Grant | 付与された権限情報を示します、列挙値：READ、WRITE、FULL_CONTROL  | String    |

コンテナノードGranteeの内容：

| ノード名称（キーワード）          |親ノード|説明                                    |タイプ        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | AccessControlPolicy.Owner | ユーザーのID、ルートアカウントであれば、フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt; または  qcs::cam::anyone:anyone （すべてのユーザーを指します）サブアカウントであれば、フォーマットは： qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;|  String |
| DisplayName | AccessControlPolicy.Owner |  ユーザー名称 |  String |

###　エラーコード
このリクエスト操作には、特別なエラーメッセージがありません。一般的なエラーメッセージについては、[エラーコード](https://cloud.tencent.com/document/product/436/7730)セクションを参照してください。


## 実際のケース

### リクエスト
``` 
GET /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b40652
```
### 応答
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
    <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
    <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:type=\"CanonicalUser\">
        <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
        <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:type=\"Group\">
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```



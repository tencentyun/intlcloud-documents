## 機能説明
PUT Object acl APIは、あるバケットのあるオブジェクトに対して、ACLテーブルを構成のために使用されます。Header：「x-cos-acl」、「x-cos-grant-read」、「x-cos-grant-full-control」を介して、ACL情報を渡しますか、ボディを介してXMLフォーマットでACL情報を渡します。

## リクエスト
### リクエスト例

```shell
PUT /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
>Authorization：Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください）。

### リクエストヘッダー

#### 共通のヘッダー

このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728 "公共请求头部")ドキュメントを参照してください。

#### 非共通のヘッダー

<table>
   <tr>
      <th>名称</th>
      <th>説明</th>
      <th>タイプ</th>
      <th>必須項目</th>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-acl</td>
      <td>オブジェクトのACL属性を定義します。有効値：private、public-read、default；デフォルト値：default（バケット権限を継承します）。<br>注：現時点でアクセスポリシーエントリは1000に制限されています。Object ACLコントロールが不要な場合は、defaultを入力するか、この項目を設定しないでください。デフォルトでは、バケット権限をします</td>
      <td>string</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-read</td>
      <td>権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id="[OwnerUin]"</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-full-control</td>
      <td>権限が付与された者にすべての権限を付与します。フォーマット：x-cos-grant-full-control: id="[OwnerUin]"</td>
      <td>String</td>
      <td>いいえ</td>
   </tr>
</table>


### リクエストボディ
このリクエストのリクエストボディはACL構成規則です。
```shell
<AccessControlPolicy>
   <Owner>
     <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
     <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
   </Owner>
   <AccessControlList>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
           <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
        </Grantee>
        <Permission>READ</Permission>
     </Grant>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
           <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
           <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
        </Grantee>
        <Permission>FULL_CONTROL</Permission>
     </Grant>
   </AccessControlList>
</AccessControlPolicy>
```


具体的なデータ内容は以下のとおりです：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:-- |:--|:--|:--|
| AccessControlPolicy |無し| GET Bucket acl結果を保存するコンテナ | Container |はい|

コンテナノードAccessControlPolicyの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:-- |:--|:--|:--|
| Owner | AccessControlPolicy | バケット所有者情報 |  Container |はい|
| AccessControlList | AccessControlPolicy | 権限が付与された者情報と権限情報 |  Container |はい|

コンテナノードオーナーの内容：

|ノード名称（キーワード）|親ノード|説明|タイプ|必須項目|
|:---|:-- |:--|:--|:--|
| ID | AccessControlPolicy.Owner |  バケット所有者ID、</br>フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;マスタアカウントであれば、&lt;OwnerUin&gt; と &lt;SubUin&gt; は同じ値です |  String |はい|
|DisplayName	|AccessControlPolicy.Owner |バケット所有者の名称情報	|string	|はい|

コンテナノードAccessControlListの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grant | AccessControlPolicy.AccessControlList | 単一バケットの認証情報。1つのAccessControlListは100個のGrantを持つことができます | Container    |はい|

コンテナノードGrantの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 権限が付与された者のリソース情報。タイプはRootAccount、またはSubAccountである可能性があります；</br>タイプがRootAccountの場合は、IDのuinにQQを入力するか、またはanyone（すべてのタイプのユーザーを示します）でuin/&lt;OwnerUin&gt; と uin/&lt;SubUin&gt;を取り替えます。</br>タイプがRootAccountの場合は、uinがルートアカウント、Subaccountがサブアカウントを示します | Container    |はい|
| Permission | AccessControlPolicy.AccessControlList.Grant | 付与された権限情報を示します。列挙値：READ、FULL_CONTROL  | String    |はい|

コンテナノードGranteeの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | ユーザーのID、</br>フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; マスタアカウントであれば、&lt;OwnerUin&gt; と &lt;SubUin&gt; は同じ値です |  String |はい|
|DisplayName|AccessControlPolicy.AccessControlList.Grant.Grantee |バケット所有者の名称情報|string	|はい|


## 応答
### 応答ヘッダー

#### 共通の応答ヘッダー

この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729 "公共响应头部")ドキュメントを参照してください。

#### 特有の応答ヘッダー
このリクエスト操作には、特別な応答ヘッダー情報はありません。

### 応答ボディ
このリクエストの応答ボディはブランクです。

###　エラーコード
この応答は、以下のエラーコードの情報が発生する可能性があります。一般的なエラー情報については、[エラーコード](https://cloud.tencent.com/document/product/436/7730)ドキュメントを参照してください。

<table>
   <tr>
      <th>エラーコード</th>
      <th>説明</th>
      <th>HTTPステータスコード</th>
   </tr>
   <tr>
      <td>SignatureDoesNotMatch</td>
      <td>提供された署名は規則に適合しません。このエラーコードを返します</td>
			<td nowrap="nowrap">403 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.3">Forbidden</a></td>
   </tr>
   <tr>
      <td>NoSuchBucket</td>
      <td>追加しようとしている規則が所属するバケットが存在しない場合、該当エラーコードを返します</td>
			<td nowrap="nowrap">404 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td>
   </tr>
   <tr>
      <td>MalformedXML</td>
      <td>XMLフォーマットが不正です。Restful APIドキュメントとよく比較してください</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
   <tr>
      <td>InvalidRequest</td>
      <td>リクエストは不正です。エラー説明に「header acl and body acl conflict」と表示されている場合、表示はヘッダーとボディ両方にaclパラメータを含めることはできません</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
</table>

## 実際のケース

### リクエスト

```shell
PUT /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

<AccessControlPolicy>
   <Owner>
     <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
     <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
   </Owner>
   <AccessControlList>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
           <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
        </Grantee>
        <Permission>READ</Permission>
     </Grant>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
           <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
           <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
        </Grantee>
        <Permission>FULL_CONTROL</Permission>
     </Grant>
   </AccessControlList>
</AccessControlPolicy>
```

### 応答

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT\
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```


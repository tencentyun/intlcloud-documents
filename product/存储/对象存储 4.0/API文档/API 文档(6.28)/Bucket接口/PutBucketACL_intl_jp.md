## 機能説明
PUT Bucket acl APIは、バケットのaclテーブルを書き込むために使用されます。ヘッダー：「x-cos-acl」、「x-cos-grant-read」、「x-cos-grant-full-control」を介して、acl情報を渡しますか、ボディを介してXMLフォーマットでacl情報を渡します。

>!
>- ヘッダーとボディのどちらか一方しか選択できません。そうでなければ、応答は競合します。
>- PUT Bucket aclは上書き操作です。新しいaclを渡しますと、元のaclが上書きされます。
>- バケット作成者だけが操作権限を持っています。

### 詳細分析
1. ヘッダーまたはxml ボディを通して設定できます。1つの方法だけを使用することをお勧めします。
2. プライベートバケットは、あるフォルダをパブリックに設定することができます。その後、このフォルダ配下のファイルは全部パブリックになります；ただし、フォルダをプライベートに設定した後は、フォルダに設定されたパブリックプロパティは有効になりません。

## リクエスト
### リクエスト例

```
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String（詳細については[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)セクションを参照してください）


### リクエストヘッダー

**パブリックヘッダー**
このリクエスト操作の実現では、共通リクエストヘッダーを使用します。共通リクエストヘッダーの詳細については、[共通リクエストヘッダー](https://cloud.tencent.com/document/product/436/7728)セクションを参照してください。

**非パブリックヘッダー** 
このリクエスト操作の実現では、PUTリクエストのx-cos-aclヘッダーによってバケットアクセス権限を設定できます。現時点では、3種類のバケットアクセス権限があります：public-read-write、public-readとprivate。設定しなければ、デフォルトではprivate権限です。ユーザーに読み取り、書き込み、または読み書き権限を明示的に付与することもできます。内容は以下のとおりです：

|名称|説明|タイプ|必須項目|
|:---|:-- |:--|:--|
| x-cos-acl | バケットのacl属性を定義します。有効値：private、public-read-write、public-read；デフォルト値：private | String|  いいえ |
| x-cos-grant-read |権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id="[OwnerUin]" | String |  いいえ |
| x-cos-grant-write| 権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id="[OwnerUin]" |String |  いいえ |
| x-cos-grant-full-control | 権限が付与された者にすべての権限を付与します。フォーマット：x-cos-grant-full-control: id="[OwnerUin]" | String|  いいえ |

### リクエストボディ
このリクエスト操作の実現は、リクエストボディ内の特定のリクエストパラメータを用いてバケットのアクセス権限を設定できるが、リクエストボディにパラメータ付き、および、リクエストヘッダーにaclサブリソース付きという2つの方法のうち、1つしか選択できません。
すべてのノード付きの例：
```
<AccessControlPolicy>
  <Owner>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>READ</Permission>
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

コンテナノードAccessControlListの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grant | AccessControlPolicy.AccessControlList | 単一バケットの認証情報。1つのAccessControlListは100個のGrantを持つことができます | Container    |はい|

コンテナノードGrantの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 権限が付与された者のリソース情報。タイプはRootAccount、またはSubAccountである可能性があります；</br>タイプがRootAccountの場合は、IDのuinにQQを入力するか、またはanyone（すべてのタイプのユーザーを示します）でuin/&lt;OwnerUin&gt; と uin/&lt;SubUin&gt;を取り替えます。</br>タイプがRootAccountの場合は、uinがルートアカウント、Subaccountがサブアカウントを示します | Container    |はい|
| Permission | AccessControlPolicy.AccessControlList.Grant | 付与された権限情報を示します、列挙値：READ、WRITE、FULL_CONTROL  | String    |はい|

コンテナノードGranteeの内容：

| ノード名称（キーワード）          |親ノード | 説明                                    | タイプ        |必須項目|
| ------------ | ------------------------------------- | --------- |:--|:--|
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | ユーザーのID、</br>フォーマット：qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; マスタアカウントであれば、&lt;OwnerUin&gt; と &lt;SubUin&gt; は同じ値です |  String |はい|


## 応答

### 応答ヘッダー
#### 共通の応答ヘッダー
この応答は、共通応答ヘッダーを使用します。共通応答ヘッダーの詳細については、[共通応答ヘッダー](https://cloud.tencent.com/document/product/436/7729)セクションを参照してください。
#### 特有の応答ヘッダー
この応答には、特別な応答ヘッダーがありません。
### 応答ボディ
この応答ボディは空を返します。

### エラー分析
このリクエストが発生する可能性がある特別、且つ一般的なエラー状況は以下のとおりです：

|エラーコード|説明|HTTPステータスコード|
|------|------|------|
|InvalidDigest|400 Bad Request|ユーザーに付いているContent-MD5とCOS計算ボディのContent-MD5は一致ではありません|
|MalformedXM|400 Bad Request|渡されたxmlフォーマットがエラーになり、restful apiドキュメントとよく比較してください|
|InvalidArgument|400 Bad Request|パラメータエラー、具体的にはエラーメッセージを参照してください|

## 実際のケース

### リクエスト
```
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT 
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

<AccessControlPolicy>
  <Owner>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### 応答
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT 
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw

```



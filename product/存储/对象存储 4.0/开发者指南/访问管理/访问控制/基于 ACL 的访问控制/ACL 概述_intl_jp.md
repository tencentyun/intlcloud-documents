## 基本概念

アクセス制御リスト（ACL）はXML言語で説明されており、リソースに関連する、認証対象者と権限を指定するリストです。それぞれのバケットとオブジェクトにはそれに関連するACLがあります。匿名ユーザーまたはその他Tencent Cloudのルートアカウントに基本的な読み取り・書き込み権限を付与することに対応しています。

>!リソースに関連するACL管理の使用には複数の制限があります：
>- リソースの保有者は常にリソースに対してFULL_CONTROL権限を有し、取り消しまたは変更ができません。
>- 匿名ユーザーはリソース保有者になることができません。このような場合、オブジェクトリソースの保有者はバケットの作成者に当たります（Tencent Cloudのルートアカウント）。
>- Tencent Cloud CAMのルートアカウントまたは匿名ユーザーにのみ権限を付与できるが、一方、サブユーザーまたはユーザーグループに権限を付与できません。
>- 権限に条件をつけることに対応していません。
>- 明示的拒否の権限に対応していません。
>- 1つのリソースあたり最大100までのACLポリシーを有することができます。

## ACLの要素

### 身分Grantee

承認された身分は、特定のCAMルートアカウントであり、あるいは特定のプリセットのCAMユーザーグループである可能性があります。

>!
>- その他Tencent Cloudルートアカウントにアクセス権限を付与した場合、権限が付与されたルートアカウントはその名義下のサブユーザー、ユーザーグループまたはロールにアクセス権限を付与することができます。
>- COSとしては、匿名ユーザーまたはCAMユーザーグループにWRITE、WRITE_ACPまたはFULL_CONTROL権限を付与することは望ましくないです。権限が付与されると、ユーザーグループがリソースをアップロード、ダウンロード、削除する可能性があるため、データ紛失や課金等のリスクにつながる恐れがあります。


バケットまたはオブジェクトのACLにおいて権限が付与された身分は下記を含みます：

- アカウント間操作：ルートアカウントのIDにより、【アカウントセンター】の[アカウント情報](https://console.cloud.tencent.com/developer)を通じて「アカウントID」を取得してください。例えば `398626565`。
- プリセットユーザーグループ： URIタグをプリセットのユーザーグループにつけてください。対応するユーザーグループは下記を含みます：
  - 匿名ユーザーグループ -`http://cam.qcloud.com/groups/global/AllUsers`。このグループは、世界中の誰でも認証がなくともリソースにアクセスできることを意味します。リクエストが署名あるいは未署名かを問いません。
  - 認証ユーザーグループ -`http://cam.qcloud.com/groups/global/AuthenticatedUsers`。このグループはすべての登録されたTencent Cloud CAMアカウントを認証せずにリソースにアクセスできることを意味します。


### 操作Permission

COSのリソースACLにおいて対応する操作は、実は一連の操作の集合であり、バケットとオブジェクトACLにとってそれぞれの意味は異なります。

**バケットの操作**

下記は、バケットACLにおいて設定可能な操作リストです：

| 操作集合       | 説明                 | 許可される行為                                                   |
| ------------ | -------------------- | ------------------------------------------------------------ |
| READ         | オブジェクトのリスト             | GetBucket、HeadBucket、GetBucketObjectVersions、ListMultipartUploads |
| WRITE        | オブジェクトのアップロード、上書きと削除 | PutObject、PutObjectCopy、PostObject、InitiateMultipartUpload、UploadPart、UploadPartCopy、CompleteMultipartUpload、DeleteObject |
| READ_ACP     | バケットのACLの読み取り     | GetBucketAcl                                                 |
| WRITE_ACP    | バケットのACLの書き込み     | PutBucketAcl                                                 |
| FULL_CONTROL | 以上の4種類の権限の集合   | 以上のすべて行為の集合                                           |

>!バケットにWRITE、WRITE_ACPまたはFULL_CONTROL権限を慎み深く付与してください。バケットにWRITE権限を付与すると、認証対象者は既存のすべてのオブジェクトを上書きまたは削除できるようになります。

**オブジェクトの操作**

下記は、オブジェクトACLにおいて設定可能な操作リストです：

| 操作       | 説明                 | 許可される行為                                                   |
| ------------ | ------------------ | --------------------------------------- |
| READ         | オブジェクトの読み取り           | GetObject、GetObjectVersion、HeadObject |
| READ_ACP     | オブジェクトのACLの読み取り     | GetObjectAcl、GetObjectVersionAcl       |
| WRITE_ACP    | オブジェクトのACLの書き込み     | PutObjectAcl、PutObjectVersionAcl       |
| FULL_CONTROL | 以上の4種類の権限の集合 | 以上のすべて行為の集合                      |

>!オブジェクトはWRITE操作を付与することができません。

### プリセットのACL

COSは一連のプリセットACLに権限を付与することができます。これで簡単な権限の説明は大いに便利になります。プリセットACL説明を使用する場合、PUT Bucket/ObjectまたはPUT Bucket/Object acl に`x-cos-acl`ヘッダーを付け、また必要な権限を説明する必要があります。更にリクエスト本文にはXMLの説明コンテンツがついている場合、優先的にヘッダーにおける説明は選択され、またリクエスト本文におけるXML説明は無視されます。

**バケットのプリセットACL**

| プリセット名           | 説明                                                         |
| ------------------ | ------------------------------------------------------------ |
| private            | 作成者（ルートアカウント）はFULL_CONTROL権限を有し、他人は権限を有しません。（デフォルト） |
| public-read        | 作成者はFULL_CONTROL権限を有し、匿名ユーザーグループはREAD権限を有します。     |
| public-read-write  | 作成者と匿名ユーザーグループはいずれもFULL_CONTROL権限を有します。通常、この権限を付与しないほうが望ましいです。 |
| authenticated-read | 作成者はFULL_CONTROL権限を有し、認証ユーザーグループはREAD権限を有します。     |

**オブジェクトのプリセットACL**

| プリセット名           | 説明                                                         |
| ------------------------- | ------------------------------------------------------------ |
| default                   | ブランク説明。このような場合、リクエストは許可と表示されるバケットまたはサブユーザーポリシーに準じます。宣言がなければ拒否します。 |
| private                   | 作成者（ルートアカウント）はFULL_CONTROL権限を有し、他人は権限を有しません。     |
| public-read               | 作成者はFULL_CONTROL権限を有し、匿名ユーザーグループはREAD権限を有します。     |
| authenticated-read        | 作成者はFULL_CONTROL権限を有し、認証ユーザーグループはREAD権限を有します。     |
| bucket-owner-read         | 作成者はFULL_CONTROL権限を有し、バケット保有者はREAD権限を有します。   |
| bucket-owner-full-control | 作成者とバケット保有者はいずれもFULL_CONTROL権限を有します。             |

>!オブジェクトはpublic-read-write権限を付与することができません。

## 例
### バケットのACL
バケットの作成にあたって、COSはデフォルトのACLを作成することでリソース保有者に対してリソースへの完全なる制御権限（FULL_CONTROL）を授与します。例えば：

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### オブジェクトのACL

**オブジェクトの作成にあたって、COSはデフォルトではACLを作成しません。このような場合、オブジェクトの保有者はバケット保有者となります。**オブジェクトが継承した権限はバケットのアクセス権限と同じです。オブジェクトにはデフォルトのACLがないため、それはバケットポリシー（Bucket Policy）におけるアクセス者とその行為への定義により、リクエストを許可できるかを判断します。詳細については、[アクセスポリシー言語概要](https://cloud.tencent.com/document/product/436/18023)のドキュメントを参照してください。

オブジェクトにその他アクセス権限を付与するには、上記に基づき、その他ACLを追加することでオブジェクトのアクセス権限を説明することができます。例えば、匿名ユーザーに、単一オブジェクトのみを読み取る権限を付与します。下記に例を示します：

```xml
<AccessControlPolicy>
  <Owner>
    <ID>Owner-Cononical-CAM-User-Id</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>Owner-Cononical-CAM-User-Id</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
        <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

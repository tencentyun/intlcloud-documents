## 基本概念

アクセス制御リスト（ACL）はXML言語を使用して記述する、リソースにバインドされた、被付与者と付与される権限を指定したリストです。各バケットとオブジェクトにはそれぞれに、これらとバインドされたACLがあり、匿名ユーザーまたはその他のTencent Cloudのルートアカウントに対し、基本的な読み取り/書き込み権限を付与することができます。

>! リソースにバインドされたACLを使用した管理にはいくつかの制限があります。
>- リソースの所有者は常にリソースに対してFULL_CONTROL権限を有し、その取り消しまたは変更はできません。
>- 匿名ユーザーはリソースの所有者にはなれません。この場合、オブジェクトリソースの所有者はバケットの作成者（Tencent Cloudルートアカウント）となります。
>- 権限はCloud Access Management（CAM）のルートアカウントまたは事前定義済みのユーザーグループにのみ付与することができます。カスタマイズしたユーザーグループに権限を付与することはできず、サブユーザーへの権限付与も推奨されません。
>- 権限の付加条件はサポートしていません。
>- 明示的な拒否の権限はサポートしていません。
>- 1つのリソースにつき最大100のACLポリシーを持つことができます。
>

## ユースケース

>! 匿名ユーザーにアクセスを開放すること（パブリック読み取り）はハイリスクな操作であり、トラフィックが不正使用される危険性があります。やむを得ずパブリック読み取りを使用する場合は、[リンク不正アクセス防止の設定](https://intl.cloud.tencent.com/document/product/436/13319)によってセキュリティ保護を実行できます。
>

バケットとオブジェクトに簡単なアクセス権限のみを設定したい場合、または匿名ユーザーにアクセスを開放したい場合はACLを選択できます。ただし、より多くの状況下では、バケットポリシーまたはユーザーポリシーの方が柔軟性が高いため、これらを優先的に使用することをお勧めします。ACLの適用ケースには次のものがあります。

- 簡単なアクセス権限のみを設定する場合。
- コンソールでアクセス権限をすばやく設定する場合。
- あるオブジェクト、ディレクトリまたはバケットへのアクセスをすべての匿名インターネットユーザーに開放したい場合は、ACLによる操作の方が便利です。


## ACLの要素

### 被付与者 Grantee

サポートする被付与者のIDは、何らかのCAMルートアカウントまたは何らかの事前定義済みのCAMユーザーグループです。

>!
>- 他のTencent Cloudルートアカウントにアクセス権限を付与する際、この権限を付与されたルートアカウントはそのアカウント下のサブユーザー、ユーザーグループまたはロールにアクセス権限を与えることができます。
>- Cloud Object Storage（COS）は、匿名のユーザーまたはCAMユーザーグループにWRITE、WRITE_ACPまたはFULL_CONTROL権限を与えることを強く非推奨とします。一度権限を許可すると、ユーザーグループはお客様のリソースのアップロード、ダウンロード、削除などを行うことができるようになり、このことはお客様のデータの消失、料金引き落としなどのリスクをもたらす場合があります。
>


バケットまたはオブジェクトのACLにおいてサポートされるIDには次のものがあります。

- クロスアカウント：ルートアカウントのIDを使用してください。アカウントIDは**アカウントセンター**の[アカウント情報](https://console.cloud.tencent.com/developer)で取得します（例：100000000001）。
- 事前定義済みのユーザーグループ：URIタグを使用して事前定義済みのタグ付けをしたユーザーグループを使用してください。次のユーザーグループをサポートしています。
  - 匿名ユーザーグループ -`http://cam.qcloud.com/groups/global/AllUsers`このグループは、リクエストが署名済みかどうかにかかわらず、誰でも権限なしにリソースにアクセスできることを表します。
  - 認証ユーザーグループ -`http://cam.qcloud.com/groups/global/AuthenticatedUsers`このグループは、Tencent Cloud CAMアカウント認証を経たすべてのユーザーがリソースにアクセスできることを表します。


### 操作 Permission

Tencent Cloud COSがリソースのACLにおいてサポートする操作は、実際には一連の操作の集合であり、バケットおよびオブジェクトACLにはそれぞれ異なる意味があります。

**バケットの操作**

次の表に、バケットACLで設定可能な操作のリストを列記しています。

| 操作セット       | 説明             | 許可される行為                                                   |
| ------------ | -------------------- | ------------------------------------------------------------ |
| READ         | オブジェクトのリストアップ             | HeadBucket，GetBucketObjectVersions，ListMultipartUploads |
| WRITE        | オブジェクトのアップロード、上書き、削除 | PutObject，PutObjectCopy，PostObject，InitiateMultipartUpload， UploadPart，UploadPartCopy，CompleteMultipartUpload， DeleteObject |
| READ_ACP     | バケットのACLの読み取り     | GetBucketAcl                                                 |
| WRITE_ACP    | バケットのACLの書き込み     | PutBucketAcl                                                 |
| FULL_CONTROL | 上記4種類の権限のセット   | 上記のすべての行為のセット                                           |

>! バケットのWRITE、WRITE_ACPまたはFULL_CONTROL権限の付与は慎重に行ってください。バケットのWRITE権限の付与は、被付与者に既存のあらゆるオブジェクトの上書きまたは削除を許可するものです。
>

**オブジェクトの操作**

次の表に、オブジェクトACLで設定可能な操作のリストを列記しています。

| 操作セット       | 説明               | 許可される行為                              |
| ------------ | ------------------ | --------------------------------------- |
| READ         | オブジェクトの読み取り           | GetObject，GetObjectVersion，HeadObject |
| READ_ACP     | オブジェクトのACLの読み取り     | GetObjectAcl，GetObjectVersionAcl       |
| WRITE_ACP    | オブジェクトのACLの書き込み     | PutObjectAcl，PutObjectVersionAcl       |
| FULL_CONTROL | 上記3種類の権限のセット | 上記のすべての行為のセット                      |

>?オブジェクトについてはWRITE操作セットの権限はサポートしていません。

### 既定ACL

COSでは一連の既定ACLによる権限承認がサポートされており、権限を簡単に記述できるようになっています。既定ACLを使用して記述する場合、PUT Bucket/ObjectまたはPUT Bucket/Object aclにx-cos-aclヘッダーを含め、必要な権限を記述する必要があります。同時にリクエスト本文にもXMLの記述内容が含まれる場合は、ヘッダー内の記述が優先的に選択され、リクエスト本文のXMLの記述は無視されます。

**バケットの既定ACL**

| 規定名           | 説明                                                               |
| ------------------ | ------------------------------------------------------------------ |
| private            | 作成者（ルートアカウント）はFULL_CONTROL権限を有し、その他の人は権限を持ちません（デフォルト）   |
| public-read        | 作成者はFULL_CONTROL権限を有し、匿名ユーザーグループはREAD権限を有します           |
| public-read-write  | 作成者と匿名ユーザーグループの両方がFULL_CONTROL権限を有します。通常はこの権限の付与は非推奨です |
| authenticated-read | 作成者はFULL_CONTROL権限を有し、認証ユーザーグループはREAD権限を有します           |

**オブジェクトの既定ACL**

| 規定名                  | 説明                                                                         |
| ------------------------- | ---------------------------------------------------------------------------- |
| default                   | 空の記述であり、この場合は各レベルのディレクトリに基づく明示的な設定およびバケットの設定によって、リクエストを許可するかどうかを決定します（デフォルト） |
| private                   | 作成者（ルートアカウント）はFULL_CONTROL権限を有し、その他の人は権限を持ちません                     |
| public-read               | 作成者はFULL_CONTROL権限を有し、匿名ユーザーグループはREAD権限を有します                     |
| authenticated-read        | 作成者はFULL_CONTROL権限を有し、認証ユーザーグループはREAD権限を有します                  |
| bucket-owner-read         | 作成者はFULL_CONTROL権限を有し、バケット所有者はREAD権限を有します                   |
| bucket-owner-full-control | 作成者とバケット所有者の両方がFULL_CONTROL権限を有します                   |

>? オブジェクトについてはpublic-read-write権限はサポートしていません。
>

## 事例
### バケットのACL
バケットを作成する際、COSはデフォルトのACLを作成し、リソース所有者に対しリソースの完全制御権限（FULL_CONTROL）を与えます。その例を次に示します。

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

**オブジェクトを作成する際、COSはデフォルトではACLを作成しません。この場合はオブジェクトの所有者がバケット所有者となります**。オブジェクトはバケットの権限を継承し、それはバケットのアクセス権限と一致します。オブジェクトにはデフォルトのACLがないため、Bucket Policyの中のアクセス者およびその行為に対する定義に従って、リクエストが許可されるかどうかを判断します。詳細については、[アクセスポリシーの言語概要](https://intl.cloud.tencent.com/document/product/436/18023)のドキュメントをご参照ください。

オブジェクトについてその他のアクセス権限を付与したい場合は、これを基本としてさらにACLを追加し、オブジェクトのアクセス権限を記述することができます。例えば匿名ユーザーに対し、単一オブジェクトの読み取り専用の権限を付与する場合の例は次のとおりです。

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




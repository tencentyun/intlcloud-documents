**デフォルトでは、Cloud Object Storage（COS）のリソース（バケットおよびオブジェクト）はすべてプライベートです**。Tencent Cloudルートアカウント（リソース所有者）でなければバケットおよびオブジェクトへのアクセス、変更を行うことはできず、他のユーザー（サブアカウント、匿名ユーザーなど）はいずれも権限承認がなければURLから直接オブジェクトにアクセスすることはできません。

Tencent Cloudサブアカウントを作成すると、アクセスポリシーによってサブアカウントに権限を付与することができます。非Tencent Cloudユーザーにリソースを開放したい場合は、リソース（バケット、オブジェクト、ディレクトリ）のパブリック権限（パブリック読み取り）を設定することで実現できます。

![](https://qcloudimg.tencent-cloud.cn/raw/d22047a7656e9524482def3ce67b61ed.png)

## アクセス制御の要素

アクセス権限の付与とは、どの人が、どのような条件下で、どのリソースに対して、具体的な操作を行うかという制御機能の組み合わせをユーザーが決定できることを指します。このため、1つのアクセス権限行為の記述には、通常**プリンシパル、リソース、操作、条件（オプション）**の4つの要素が含まれます。

![](https://qcloudimg.tencent-cloud.cn/raw/58d70d36503b2f1a61800b5b7a672442.png)

## アクセス権限の要素

#### Tencent Cloudのプリンシパル（Principal）

ユーザーがTencent Cloudアカウントを申請する際、システムはTencent Cloudサービスへのログインに用いるルートアカウントのIDを作成します。Tencent Cloudルートアカウントはユーザー管理機能によって、異なる職責を持つユーザーを分類し管理します。ユーザーのタイプには**コラボレーター、メッセージ受信者、サブユーザーおよびロール**などがあります。具体的な定義についてはCAMの[ユーザーのタイプ](https://www.tencentcloud.com/document/product/598/32633)および[用語集](https://intl.cloud.tencent.com/document/product/598/18564)のドキュメントをご参照ください。

>? 社内のある同僚への権限承認を行いたい場合は、まず[CAMコンソール](https://console.cloud.tencent.com/cam)でサブユーザーを作成し、[バケットポリシー](https://intl.cloud.tencent.com/document/product/436/45235)、[ACL](https://intl.cloud.tencent.com/document/product/436/30583)または[ユーザーポリシー](https://intl.cloud.tencent.com/document/product/436/45236)のいずれかまたは複数の手段を選択し、サブユーザーの具体的な権限を設定する必要があります。
>

#### COSのリソース（Resource）

BucketおよびObjectはCOSの基本リソースです。そのうちフォルダは特殊なオブジェクトであり、フォルダを通じてフォルダ下のオブジェクトの権限承認を行うことができます。詳細については、[フォルダの権限の設定](https://intl.cloud.tencent.com/document/product/436/35261)をご参照ください。

また、バケットとオブジェクトにはどちらもそれらに関連するサブリソースが存在します。

バケットのサブリソースには次のものが含まれます。

- aclおよびpolicy：バケットのアクセス制御情報です。
- website：バケットの静的ウェブサイトホスティング設定です。
- tagging：バケットのタグ情報です。
- cors：バケットのクロスドメイン設定情報です。
- lifecycle：バケットのライフサイクル設定情報です。

オブジェクトのサブリソースには次のものが含まれます。

- acl：オブジェクトのアクセス制御情報です。
- restore：アーカイブタイプのオブジェクトの復元設定です。

#### COSのアクション（Action）

COSではリソースに対する一連のAPI操作をご提供しています。詳細については、[操作リスト](https://intl.cloud.tencent.com/document/product/436/10111)のドキュメントをご参照ください。

#### COSの条件（Condition、オプション）

オプションです。vpc、vipなどの権限発効の条件についての詳細は、CAMの[発効条件](https://www.tencentcloud.com/document/product/598/10608)をご参照ください。

## プライベートの原則

>? デフォルトでは、Tencent Cloud COS内のリソースはすべてプライベートです。
>

- リソース所有者（バケットのリソースを作成したTencent Cloudルートアカウント）はこのリソースに対する最高権限を有します。リソース所有者はアクセスポリシーを編集および変更することができ、第三者または匿名ユーザーに対しアクセス権限を与えることができます。
- Tencent Cloudの[CAM（Cloud Access Management）](https://intl.cloud.tencent.com/document/product/598/10583)アカウントを使用してバケット作成またはオブジェクトのアップロードを行う場合、親アカウントにあたるルートアカウントがリソース所有者となります。
- バケット所有者のルートアカウントは他のTencent Cloudルートアカウントに対し、オブジェクトのアップロード権限を付与することができます（クロスアカウントアップロード）。この場合、オブジェクトの所有者は引き続きバケット所有者のルートアカウントとなります。

## アクセス制御の複数の手段

COSは複数の権限設定方式をご提供してアクセス制御を実現しています。これにはバケットポリシー、ユーザーポリシー（CAMポリシー）、バケットACLおよびオブジェクトACLが含まれます。

これらはポリシー設定の出発点に基づき、リソースベースとユーザーベースの2種類の方式に分けられます。また権限承認の方式に基づき、ポリシーとACLの2種類の方式に分けられます。

![](https://qcloudimg.tencent-cloud.cn/raw/ca32b98c546c2b039cd29ba842dc9755.png)

**分類方法1：リソースベース vs ユーザーベース**
![](https://qcloudimg.tencent-cloud.cn/raw/f92521c28d8a4841f71f267ca9964dcc.png)
- リソースを出発点とする場合：権限を具体的なリソースにバインドします。バケットポリシー、バケットACLおよびオブジェクトACLが含まれ、COSコンソールまたはCOS APIによって設定します。
- ユーザーを出発点とする場合：ユーザーポリシー（CAMポリシー）では権限をユーザーにバインドします。ポリシー作成時にユーザーを入力する必要はなく、リソース、アクション、条件などを指定し、[CAMコンソール](https://console.cloud.tencent.com/cam)で設定します。

**分類方法2：ポリシー vs ACL**
![](https://qcloudimg.tencent-cloud.cn/raw/e861ab92e54560071e26ac27a180c54b.png)
- ポリシー：ユーザーポリシー（CAMポリシー）とバケットポリシーはどちらも完全なポリシー構文に基づいて権限承認を行うものです。権限承認の動作は各APIの対応する動作に細分化され、許可/ 拒否のエフェクトを指定することができます。
- ACL：バケットACLとオブジェクトACLはどちらもアクセス制御リスト（ACL）をベースにして実装されます。ACLはリソースにバインドされた、被付与者と付与される権限を指定したリストです。整理され抽象化された権限に対応し、許可のエフェクトのみを指定することができます。


### リソースベースのポリシー

リソースベースのポリシーにはバケットポリシー、バケットACL、オブジェクトACLの3種類が含まれます。**バケット**と**オブジェクト**の次元でそれぞれアクセス制御を行うことができます。具体的には次の表をご参照ください。

| 次元   | タイプ                   | 記述方式 | サポートするプリンシパル                                       | サポートするリソース粒度       | サポートするアクション         | サポートするエフェクト    |
| ------ | ---------------------- | -------- | ------------------------------------------------ | -------------------- | ------------------ | ------------- |
| Bucket | アクセスポリシー言語（Policy） | JSON     | サブアカウント、ロール、Tencent Cloudサービス、他のルートアカウント、匿名ユーザーなど | バケット、オブジェクト、プレフィックスなど | それぞれの具体的な操作   | 許可/明示的な拒否 |
| Bucket | アクセス制御リスト（ACL）    | XML      | 他のルートアカウント、サブアカウント、匿名ユーザー                             | バケット               | 整理された読み取り/書き込み権限 | 許可のみ        |
| Object | アクセス制御リスト（ACL）    | XML      | 他のルートアカウント、サブアカウント、匿名ユーザー                             | オブジェクト                 | 整理された読み取り/書き込み権限 | 許可のみ        |

<span id="BucketPolicy"></span>
#### バケットポリシー（Bucket Policy）

バケットポリシー（Bucket Policy）はJSON言語を使用して記述され、匿名IDまたはTencent Cloudのあらゆる[CAM](https://intl.cloud.tencent.com/document/product/598/10583)アカウントに対し、バケット、バケット操作、オブジェクトまたはオブジェクト操作への権限付与をサポートしています。Tencent Cloud COSのバケットポリシーは、そのバケット内のほとんどすべての操作の管理に用いることができます。ACLでは記述できないアクセスポリシーを、バケットポリシーを使用して管理することをお勧めします。その他の内容については[バケットポリシー](https://intl.cloud.tencent.com/document/product/436/45235)のドキュメントをご参照ください。

>!Tencent Cloudのルートアカウントは、そのアカウント下のリソース（バケットを含む）に対する最大の権限を有しています。バケットポリシーではほとんどすべての操作を制限できますが、ルートアカウントは常にPUT Bucket Policy操作の権限を有しており、ルートアカウントがこの操作を呼び出す際、バケットポリシーのチェックは行われません。


以下は、匿名ユーザーに対し広州にあるバケットexamplebucket-1250000000内のすべてのオブジェクトへのアクセスを許可するポリシーです。署名のチェックは必要なく、そのままバケット内のすべてのオブジェクトをダウンロード（GetObject）できます。すなわち、URLを知っている匿名ユーザーは誰でもオブジェクトをダウンロードできます（パブリック読み取り方式に類似）。

```json
{
  "Statement": [
    {
      "Principal": "*",
      "Effect": "Allow",
      "Action": ["cos:GetObject"],
      "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
    }
  ],
  "Version": "2.0"
}
```

<span id="ACLPolicy"></span>
#### アクセス制御リスト（ACL）

アクセス制御リスト（ACL）はXML言語を使用して記述する、リソースにバインドされた、被付与者と付与される権限を指定したリストです。各バケットとオブジェクトにはそれぞれに、これらとバインドされたACLがあり、匿名ユーザーまたはその他のTencent Cloudのルートアカウントに対し、基本的な読み取り/書き込み権限を付与することができます。その他の内容については、[ACL](https://intl.cloud.tencent.com/document/product/436/30583)のドキュメントをご参照ください。

>! 発行されたACLにその記述があるかどうかにかかわらず、リソースの所有者は常にリソースに対してFULL_CONTROL権限を有します。
>

以下はバケットACLの例です。バケット所有者（ユーザーUIN：100000000001）の完全制御権限を記述しています。

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

以下はオブジェクトACLの例です。オブジェクト所有者（ユーザーUIN：100000000001）の完全制御権限を記述し、すべての人が読み取り可能な（匿名ユーザーのパブリック読み取り）権限を付与しています。

```xml
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
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


<span id="UserPolicy"></span>
#### ユーザーポリシー

ユーザーは[CAM](https://intl.cloud.tencent.com/document/product/598/10583)で、ルートアカウント下の異なるタイプのユーザーに対し、異なる権限を付与することができます。

ユーザーポリシーとバケットポリシーの最大の違いは、ユーザーポリシーはエフェクト（Effect）、アクション（Action）、リソース（Resource）、条件（Condition、オプション）のみを記述し、プリンシパル（Principal）は記述しない点です。このため、ユーザーポリシーの作成完了後、サブユーザー、ユーザーグループまたはロールに対しバインド操作を実行する必要があります。またユーザーポリシーは、匿名ユーザーへのアクションおよびリソース権限の付与はサポートしていません。

[プリセットポリシーを使用した権限のバインド](https://intl.cloud.tencent.com/document/product/598/10602)を行うことも、[ユーザーポリシーを自ら作成](https://intl.cloud.tencent.com/document/product/598/10603)した後に指定のプリンシパルにバインドすることで、アカウント下のユーザーに対するアクセス管理を実現することもできます。その他の内容については、[ユーザーポリシー](https://intl.cloud.tencent.com/document/product/436/45236)のドキュメントをご参照ください。

以下は、広州にあるバケットexamplebucket-1250000000のすべてのCOS操作権限を付与するポリシーです。ポリシーを保存した後、さらに[CAM](https://intl.cloud.tencent.com/document/product/598/10583)のサブユーザー、ユーザーグループまたはロールにバインドすることで発効します。

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```



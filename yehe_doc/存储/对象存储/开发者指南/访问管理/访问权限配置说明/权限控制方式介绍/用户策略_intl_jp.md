Tencent Cloudルートアカウントは[Cloud Access Management（CAM）](https://console.cloud.tencent.com/cam/overview)コンソールでCAMユーザーを作成し、ポリシーをバインドすることで、CAMユーザーに対しTencent Cloudのリソースを使用する権限を与えることができます。

## 概要

ユーザーは[CAM](https://intl.cloud.tencent.com/document/product/598/10583)で、ルートアカウント下の異なるタイプのユーザーに対し、異なる権限を付与することができます。これらの権限はアクセスポリシー言語で記述し、ユーザーを出発点として権限承認を行うため、**ユーザーポリシー**と呼ばれます。

#### ユーザーポリシーとバケットポリシーとの違い

ユーザーポリシーとバケットポリシーの最大の違いは、ユーザーポリシーはエフェクト（Effect）、アクション（Action）、リソース（Resource）、条件（Condition、オプション）のみを記述し、プリンシパル（Principal）は記述しない点です。このため、ユーザーポリシーの使用方法は次のようになります。
- ユーザーポリシーは作成完了後、さらにサブユーザー、ユーザーグループまたはロールに対しバインド操作を実行する必要があります。
- ユーザーポリシーは**アクションおよびリソース権限の匿名ユーザーへの付与をサポートしていません**。

#### プリセットポリシーとカスタムポリシー

ユーザーポリシーには、[プリセットポリシーとカスタムポリシー](https://intl.cloud.tencent.com/document/product/598/10601)の2種類が含まれます。[プリセットポリシーを使用した権限のバインド](https://intl.cloud.tencent.com/document/product/598/10602)、または[ユーザーポリシーを自ら作成](https://intl.cloud.tencent.com/document/product/598/35596)して権限のバインドを行うことができます。詳細については、CAMの[権限承認ガイド](https://intl.cloud.tencent.com/document/product/598/32668)をご参照ください。

## ユースケース
ユーザーが行えること、および推奨されるユーザーポリシーについてお知りになりたい場合は、CAMユーザーを検索し、その所属するユーザーグループの権限を確認することで、ユーザーが何を行うことができるかを知ることができます。次のようなケースで推奨されます。
- バケット作成（PutBucket）、バケットリストアップ（GetService）などの、Cloud Object Storage（COS）サービスレベルの権限を設定したい場合。
- ルートアカウント下のすべてのCOSバケットおよびオブジェクトを使用したい場合。
- ルートアカウント下の大量のCAMユーザーに同等の権限を付与したい場合。

## ユーザーポリシー構文

### ポリシー文法

バケットポリシーと同様に、ユーザーポリシーもJSON言語を使用して記述し、[アクセスポリシー言語](https://intl.cloud.tencent.com/document/product/436/18023)の統一ルール（プリンシパル、エフェクト、アクション、リソース、条件など）に従います。ただし、ユーザーポリシーはユーザー/ユーザーグループに直接バインドされるため、ユーザーポリシーではプリンシパル（Principal）の入力は不要です。

次の表はユーザーポリシーとバケットポリシーとの違いを比較したものです。

| 要素|ユーザーポリシー |バケットポリシー |
|---|---|---|
|プリンシパル |**入力不要**|入力必須|
|エフェクト |入力必須 |入力必須 |
|アクション |入力必須 |入力必須 |
|リソース |入力必須 |**このバケット内のリソース**|
|条件 |オプション |オプション |

### バケットポリシーの例

以下は、典型的なユーザーポリシーの例です。このポリシーは、広州にあるバケットexamplebucket-1250000000のすべてのCOS操作権限を付与するポリシーです。ポリシーを保存した後、さらに[CAM](https://intl.cloud.tencent.com/document/product/598/10583)のサブユーザー、ユーザーグループまたはロールにバインドすることで発効します。

```
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

## ユーザーポリシーによるサブアカウントへのCOSアクセス権限承認

### 前提条件

CAMサブアカウントを作成済みであることが必要です。作成方法については[サブアカウントの作成](https://intl.cloud.tencent.com/document/product/436/11714)をご参照ください。

<span id="カスタムポリシー"></span>
### 設定手順

CAMでは[プリセットポリシーとカスタムポリシー](https://intl.cloud.tencent.com/document/product/598/10601)をご提供しています。プリセットポリシーはCAMの提供するシステムプリセットポリシーであり、COS関連ポリシーについては[プリセットポリシー](#プリセットポリシー)をご覧ください。カスタムポリシーはユーザーがリソース、アクションなどの要素を自ら定義することができ、よりフレキシブルです。カスタムポリシーを新規作成し、サブアカウントへの権限承認を行う方法については以下でご説明します。

1. [CAMコンソール](https://console.cloud.tencent.com/cam)にログインします。
2. **ポリシー > カスタムポリシーの新規作成 > ポリシー構文で作成**を選択し、ポリシー作成ページに進みます。
3. 実際のニーズに応じて**空白テンプレート**を選択して権限承認ポリシーをカスタマイズするか、またはCOSにバインドされた**システムテンプレート**を選択します。ここでは**空白テンプレート**を例にとります。

4. **空白テンプレート**を選択し、ポリシー構文を入力します。次の基本要素を含める必要があります。
 - **resource：権限を承認するリソース**。
     - すべてのリソース（`"*"`）
     - 指定するバケット(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"`)
     - バケット内の指定するディレクトリまたはオブジェクト(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/test/*"`)
 - **action：権限を承認するアクション**。
 - **effect：エフェクト**。`"allow"`（許可）または`"deny"`（拒否）を選択します。
 - **condition：発効条件**。オプションです。

 COSはユーザーポリシーの例をご提供しています。次のドキュメントをご参照の上、ポリシーの内容をコピーして**ポリシー内容**のエディタボックス内に貼り付け、入力に間違いがないことを確認してから**完了**をクリックします。
 - [サブアカウントのCOSアクセス権限の承認](https://intl.cloud.tencent.com/document/product/436/11714)
 - [COS API権限承認ポリシー使用ガイド](https://intl.cloud.tencent.com/document/product/436/30580)
5. 作成完了後、[CAMコンソール](https://console.cloud.tencent.com/cam)の**ポリシー > カスタムポリシー**で、作成したカスタムポリシーを確認し、ポリシーをサブアカウントにバインドすることができます。

6. サブアカウントにチェックを入れ、**OK**をクリックして権限を承認すると、限定されたCOSリソースにサブアカウントを使用してアクセスできるようになります。


<span id="プリセットポリシー"></span>
## プリセットポリシー
1. CAMではいくつかのプリセットポリシーをご提供しています。[CAMコンソール](https://console.cloud.tencent.com/cam)の**ポリシー > プリセットポリシー**で確認し、「COS」を検索してフィルタリングすることができます。


2. ポリシー名をクリックし、**ポリシー構文 > JSON**に進み、具体的なポリシーの内容を確認します。プリセットポリシーのリソース（`resource`）はCOSのすべてのリソース(`"*"`)に設定されており、変更はサポートされていません。COSバケット、オブジェクトの一部について権限を承認したい場合は、JSONのプリセットポリシーをコピーし、[カスタムポリシー](#カスタムポリシー)を作成することができます。



表1と表2に、CAMがご提供するCOS関連のプリセットポリシーとその説明について列記します。

**表1：COSプリセットポリシー**

<table>
<tr>
	<th>プリセットポリシー</th>
	<th>説明</th>
	<th>JSONポリシー</th>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigRead</td>
	<td>この権限を有するユーザーはCOSバケット設定を読み取ることができます</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetBucket*",
                "cos:HeadBucket"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigWrite</td>
	<td>この権限を有するユーザーはCOSバケット設定を変更することができます</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutBucket*"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Data<br>FullControl</td>
	<td>COSバケット内のデータの読み取り、書き込み、削除、リストアップを含むアクセス権限</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetService",
                "cos:GetBucket",
                "cos:ListMultipartUploads",
                "cos:GetObject*",
                "cos:HeadObject",
                "cos:GetBucketObjectVersions",
                "cos:OptionsObject",
                "cos:ListParts",
                "cos:DeleteObject",
                "cos:PostObject",
                "cos:PostObjectRestore",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:DeleteMultipleObjects",
                "cos:AppendObject"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>

</table>

**表2：COSの操作とプリセットポリシーとの関係**

|説明 |操作 |QcloudCOS<br>Bucket<br>ConfigRead |QcloudCOS<br>Bucket<br>ConfigWrite |QcloudCOS<br>Data<br>FullControl |QcloudCOS<br>Data<br>ReadOnly |QcloudCOS<br>Data<br>WriteOnly |QcloudCOS<br>Full<br>Access |QcloudCOS<br>GetService<br>Access |QcloudCOS<br>ListOnly |QcloudCOS<br>Read<br>OnlyAccess |
|---|---|---|---|---|---|---|---|---|---|---|
|バケットリストアップ |GetService |❌ |❌ |✅ |❌ |❌ |✅ |✅ |✅ |✅ |
|バケット作成 |PutBucket |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|バケット削除 |DeleteBucket |❌ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|バケット基本情報取得 |HeadBucket |✅ |❌ |❌ |❌ |❌ |✅ |❌ |✅ |✅ |
|バケット設定項目取得 |GetBucket* |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|バケット設定項目変更 |GetBucket* |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|バケットアクセス権限取得 |GetBucketAcl |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|バケットアクセス権限変更 |PutBucketAcl |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|バケット内オブジェクトリストアップ |GetBucket |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|バケット内オブジェクトの全バージョンリストアップ |GetBucketObjectVersions |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|オブジェクトアップロード |PutObject |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|マルチパートアップロード |ListParts<br>InitiateMultipartUpload<br>UploadPart<br>UploadPartCopy<br>CompleteMultipartUpload<br>AbortMultipartUpload<br>ListMultipartUploads |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|オブジェクト追加 |AppendObject |❌ |❌ |✅ |❌ |❌ |✅ |❌ |❌ |❌ |
|オブジェクトダウンロード |GetObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |❌ |
|オブジェクトメタデータ確認 |HeadObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |
|クロスドメイン（CORS）事前チェック |OptionsObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |


## その他のユーザーポリシーの例

- [サブアカウントのCOSアクセス権限の承認](https://intl.cloud.tencent.com/document/product/436/11714)
- [COS API権限承認ポリシー使用ガイド](https://intl.cloud.tencent.com/document/product/436/30580)


## 操作シナリオ

Cloud Access Management（CAM）ポリシーを利用して、Cloud Virtual Machine（CVM）のコンソールで特定リソースの確認・利用権限をユーザーに付与します。本ドキュメントは特定リソースの確認・利用権限を例として、コンソールの特定部分のポリシーの利用方法をユーザーに提供します。

## 操作事例
### CVM の完全な読み書きポリシー
 CVM インスタンスを作成・管理する権限をユーザーに持たせることを希望する場合、このユーザーにQcloudCVMFullAccess のポリシーを利用させます。このポリシーはユーザーに CVM、VPC（Virtual Private Cloud）、CLB（Cloud Load Balance）と MONITOR のすべてのリソースの操作権限を持たせることにより、この目標を達成します。
具体的な操作手順は下記の通り：
[権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照して、プリセットポリシー QcloudCVMFullAccess をユーザーに認証します。

### CVM の読取専用ポリシー
ユーザーに CVM インスタンスのクエリー権限を持たせて作成、削除、起動/シャットダウン権限を持たせないことを希望する場合、ユーザーにQcloudCVMInnerReadOnlyAccess のポリシーを利用させます。このポリシーはユーザーに別々で次の操作によって目標を達成します、CVMですべて単語「Describe」を始まる操作とすべて単語「Inquiry」を始まる操作に操作権限を持たせます。具体的な操作手順は下記の通り：
[権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照して，プリセットポリシー QcloudCVMInnerReadOnlyAccess をユーザーに認証します。

### CVM 関連リソースの読取専用ポリシー
ユーザーに CVMインスタンス及び関連リソース（VPC 、CLB）へのクエリー権限だけ持たせて作成、削除、起動/シャットダウンなど操作権限を持たせないことを希望する場合、このユーザーにQcloudCVMReadOnlyAccess のポリシーを利用させます。このポリシーはユーザーに次の操作権限を持たせることにより、この目標を達成します。
- CVM で単語「Describe」を始まるすべての操作と単語 「Inquiry」を始まるすべての操作。
- VPC で単語 「Describe」を始まるすべての操作、単語 「Inquiry」を始まるすべての操作と単語「Get」を始まるすべての操作。
- CLB で単語「Describe」を始まるすべての操作。
- Monitor ですべての操作。

具体的な操作手順は下記の通り：
[権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照して，プリセットポリシー QcloudCVMReadOnlyAccess をユーザーに認証します。

### Elastic Cloud Block Storage関連のポリシー

CVM コンソールのCloud Block Storage情報を表示できるようにし、CBSの作成・利用などの権限をユーザーに持たせることを希望する場合、まず下記の操作をポリシーに追加してから、またこのポリシーをユーザーに関連することによって実現できます。
- **CreateCbsStorages：**CBSを作成します。
- **AttachCbsStorages：**指定されたElastic CBSを指定されたCVMにマウントします
- **DetachCbsStorages：**指定されたElastic CBSをアンマウントします。
- **ModifyCbsStorageAttributes：**指定されたCBSの名称或いは項目 ID を修正します。
- **DescribeCbsStorages：**CBSの詳細情報をクエリーします。
- **DescribeInstancesCbsNum：**CVMにマウント済のElastic CBSの数量とマウントできるElastic CBS数量の合計をクエリーします。
- **RenewCbsStorage：**指定されたElastic CBSを更新します。
- **ResizeCbsStorage：**指定されたElastic CBSをスケールアウトします。

具体的な操作手順は下記の通り：
1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づいて、CVM コンソール内のCBS情報を確認するとCBSを作成・利用するなどの権限のカスタマイズポリシーを作成します。
ポリシー内容は下記のポリシー文法を参照して設定できます：
```
{
    "version": "2.0"、
    "statement": [
        {
            "effect": "allow"、
            "action": [
                "name/cvm:CreateCbsStorages"、
                "name/cvm:AttachCbsStorages"、
                "name/cvm:DetachCbsStorages"、
                "name/cvm:ModifyCbsStorageAttributes"、
                "name/cvm:DescribeCbsStorages"
            ],
            "resource": [
                "qcs::cvm::uin/1410643447:*"
            ]
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列で、【ユーザ/グループの関連】をクリックします。
3.ポップアップされた「ユーザー/ユーザグループの関連」ウィンドウで、権限付与必要なユーザ/グループを選択し、【OK】をクリックします。


### セキュリティグループの関連ポリシー

 ユーザーがCVM コンソールのセキュリティグループを確認・利用できることを希望する場合、下記の操作をポリシーに追加してから、このポリシーをユーザーに関連することによって実現できます。
- **DeleteSecurityGroup：**セキュリティグループを削除します。
- **ModifySecurityGroupPolicys：**セキュリティグループのすべてのポリシーを置き換えます。
- **ModifySingleSecurityGroupPolicy：**セキュリティグループの単一ポリシーを修正します。
- **CreateSecurityGroupPolicy：**セキュリティグループポリシーを作成します。
- **DeleteSecurityGroupPolicy：**セキュリティグループポリシーを削除します。
- **ModifySecurityGroupAttributes：**セキュリティグループの属性を修正します。

具体的な操作手順は下記の通り：
1.  [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づいて、ユーザーが CVM コンソールでセキュリティグループの作成、削除、修正などの権限を持つことを可能にするのカスタマイズポリシーを作成します。
ポリシー内容は下記のポリシー文法を参照して設定できます：
```
{
    "version": "2.0"、
    "statement": [
        {
            "action": [
                "name/cvm:ModifySecurityGroupPolicys"、
                "name/cvm:ModifySingleSecurityGroupPolicy"、
                "name/cvm:CreateSecurityGroupPolicy"、
                "name/cvm:DeleteSecurityGroupPolicy"
            ],
            "resource": "*"、
            "effect": "allow"
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列で、【ユーザ/グループの関連】をクリックします。
3.ポップアップされた「ユーザー/ユーザグループの関連」ウィンドウで、権限付与必要なユーザ/グループを選択し、【OK】をクリックします。


### Elastic IPアドレスの関連ポリシー

ユーザーが CVM コンソールでElastic IPアドレスを確認・利用できることを希望する場合、まず下記の操作をポリシーに追加してから、このポリシーをユーザーに関連することによって実現できます。
- **AllocateAddresses：**アドレスを VPC 又は CVM にアサインします。
- **AssociateAddress：**Elastic IPアドレスをインスタンス或いはネットワークインターフェースに関連します。
- **DescribeAddresses：** CVM コンソールのElastic IP アドレスを確認します。
- **DisassociateAddress：**Elastic IPアドレスは、インスタンス或いはネットワークインターフェースの関連を取り消します。
- **ModifyAddressAttribute：**Elastic IPアドレスの属性を修正します。
- **ReleaseAddresses：**Elastic IPアドレスを解除します。

具体的な操作手順は下記の通り：
1.  [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づいて、カスタマイズポリシーを作成します。
このポリシーはユーザーが CVM コンソールでElastic IPアドレスをを表示でき、インスタンスにアサインすること、インスタンスを関連することを許可しますが、Elastic IPアドレスの属性を修正したり、Elastic IPアドレスの関連を解除したり、Elastic IPアドレスの権限をリリースしたりすることはできません、ポリシー内容は下記のポリシー文法を参照して設定できます：
```
{
    "version": "2.0"、
    "statement": [
        {
            "action": [
                "name/cvm:DescribeAddresses"、
                "name/cvm:AllocateAddresses"、
                "name/cvm:AssociateAddress"
            ],
            "resource": "*"、
            "effect": "allow"
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列で、【ユーザ/グループの関連】をクリックします。
3.ポップアップされた「ユーザ/ユーザグループの関連」ウィンドウで、権限付与必要なユーザ/グループを選択し、【OK】をクリックします。

### ユーザーに特定 CVM への操作権限を付与するポリシー
ユーザーに特定 CVM への操作権限を付与することを希望する場合、下記のポリシーをユーザーに関連することによって実現できます。具体的な操作手順は下記の通り：
1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づいて、カスタマイズポリシーを作成します。
このポリシーはユーザーに ID が ins-1、リージョンが広州 のCVM インスタンスへの操作権限を持たせることを許可します。ポリシー内容は下記のポリシー文法を参照して設定できます：
```
{
    "version": "2.0"、
    "statement": [
        {
            "action": "cvm:*"、
            "resource": "qcs::cvm:ap-guangzhou::instance/ins-1"、
            "effect": "allow"
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列で、【ユーザ/グループの関連】をクリックします。
3.ポップアップされた「ユーザ/ユーザグループの関連」ウィンドウで、権限付与必要なユーザ/グループを選択し、【OK】をクリックします。


### ユーザーに特定リージョンのCVM への操作権限を付与するポリシー
ユーザーに特定リージョンの CVM への操作権限を付与することを希望する場合、下記のポリシーをユーザーに関連することによって実現できます。具体的な操作手順は下記の通り：
1. [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)に基づいて、カスタマイズポリシーを作成します。
このポリシーはユーザーに広州リージョンの CVM への操作権限を持たせることを許可します、ポリシー内容は下記のポリシー文法を参照して設定できます：
```
{
    "version": "2.0"、
    "statement": [
        {
            "action": "cvm:*"、
            "resource": "qcs::cvm:ap-guangzhou::*"、
            "effect": "allow"
        }
    ]
}
```
2. 作成したポリシーを検索し、このポリシー行の「操作」列で、【ユーザ/グループの関連】をクリックします。
3.ポップアップされた「ユーザ/ユーザグループの関連」ウィンドウで、権限付与必要なユーザ/グループを選択し、【OK】をクリックします。


### サブアカウントに CVM のすべての権限を（支払い権限以外）付与する

仮に、企業アカウント（CompanyExample，ownerUin が12345678）が一つのサブアカウント（Developer）があります。このサブアカウントが企業アカウントのCVM サービスに対するすべての権限（例え作成、管理などすべての操作）を持たせることが必要であり、ただし支払い権限は含めません（注文できるが支払いできません）。
下記の二つのソリューションによって実現します：
- **ソリューション A**
企業アカウント CompanyExample は直接プリセットポリシー QcloudCVMFullAccess をサブアカウント Developerに付与します。権限付与方式は [権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)をご参照ください。
- **ソリューション B**
 1. 下記のポリシー文法に基づいて、[カスタマイズポリシー](#CAMCustomPolicy)を作成します。
```
 {
    "version": "2.0"、
    "statement":[
         {
             "effect": "allow"、
             "action": "cvm:*"、
             "resource": "*"
         }
    ]
}
```
 2. このポリシーをサブアカウントに付与します、権限付与方式は [権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)をご参照ください。


### サブアカウントにプロジェクト管理の操作権限を付与する
仮に、企業アカウント（CompanyExample，ownerUin 为12345678）は一つのサブアカウント（Developer）があります。プロジェクトを基づいてサブアカウントにコンソールでリソース管理権限を付与する必要があります。
具体的な操作手順は下記の通り：
業務権限に基づいてプロジェクト管理のカスタマイズポリシーを作成します
詳細情報は [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)をご参照ください。
2.  [権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照して、作成したカスタマイズポリシーをサブアカウントに付与します。
サブアカウントがプロジェクトを管理する時に、権限なしの提示があった場合は、例えば、スナップショット、イメージ、VPC、Elasticパブリックネットワーク IP などの製品を確認する時に権限なしを提示されました。サブアカウントに QcloudCVMAccessForNullProject、QcloudCVMOrderAccess と QcloudCVMLaunchToVPC のプリセットポリシーを付与できます。権限付与方式は[権限付与管理](https://intl.cloud.tencent.com/document/product/598/10602)をご参照ください。

<span id="CAMCustomPolicy"></span>
### カスタマイズポリシー

プリセットポリシーが要件を満たせないと予測した場合、カスタマイズポリシーを作成することによって目標を達成します。
具体的な操作手順は [ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)をご参照ください。
CVM関連のポリシー文法の詳細については、 [権限付与ポリシー文法](https://intl.cloud.tencent.com/document/product/213/10313)をご参照ください。。


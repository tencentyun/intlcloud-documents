## 基本構造

クロスリージョンルールの設定にはXML記述方法を使用します。クロスリージョンレプリケーションルールを設定することで、バケットへのクロスリージョンレプリケーションルールの設定と編集を行うことができます。Cloud Object Storage（COS）内の各バケットにつき、1つのクロスリージョンレプリケーションルールを設定できます。設定要素の基本構造は次のとおりです。

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
	<Rule>
	...
	</Rule>
</ReplicationConfiguration>
```

このうち、`<Role>`はクロスリージョンレプリケーションの開始者のIDを表すものであり、`<Rule>`は設定したクロスリージョンレプリケーションルールを指します。各ルールには次の内容が含まれます。

- Status：ルールの有効（Enabled）または無効（Disabled）のステータスを選択できます。
- ID：具体的なRuleの名前を表すために用いられます。
- Prefix：プレフィックスマッチングポリシーです。重複してはならず、重複した場合はエラーが返されます。プレフィックスが空の場合は、バケット内のすべてのオブジェクトをコピーすることを表します。プレフィックスに値がある場合は、プレフィックスの値を持つオブジェクトの内容をコピーします。
- Destination：ターゲットバケットの情報です。`Bucket`と`StorageClass`の2つの情報が含まれます。
	1. Bcuket：ターゲットバケットの命名およびストレージリージョンの情報です。
	2. StorageClass：オブジェクトをターゲットバケットにコピーした後のストレージタイプです。

## ルールの記述

### コピー内容の要素

#### バケット内の全オブジェクトの内容をコピーする

空の`<Prefix>`パラメータを指定すると、このクロスリージョンレプリケーションルールによってバケット内の全オブジェクトがコピーされます。

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### バケット内の指定のプレフィックスを持つオブジェクトの内容をコピーする

オブジェクトのプレフィックスを指定することで、プレフィックスの記述に該当する一部のオブジェクトに対してクロスリージョンレプリケーション操作を実行することができます。例えば、logs/をプレフィックスとするすべてのオブジェクトを設定する場合です。

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix>logs</Prefix>
        <Destination>
            <Bucket>qcs::cos:[Region]::[Bucketname-Appid]</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

### ターゲットバケットの要素

#### ターゲットバケットのリージョンと命名

`<Bucket>`パラメータを変更することで、異なるリージョンのバケットをターゲットバケットに指定することができます。ターゲットバケットはソースバケットとは異なるストレージリージョンになければならず、なおかつ現在COSではソースバケットとターゲットバケットが同一のアカウント下にある必要がある点にご注意ください。

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass></StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```

#### ターゲットバケット内のオブジェクトレプリカのタイプ

`<StorageClass>`パラメータを変更することで、ソースバケット内のオブジェクトをターゲットバケットにコピーした後のストレージタイプを指定することができます。現在COSでサポートするオブジェクトレプリカのストレージタイプは標準と低頻度の2種類です。ユーザーがレプリカをアーカイブタイプとして保存したい場合は、ターゲットバケット内のライフサイクルをご自身で有効化し、オブジェクトの管理を行う必要があります。COSでは、オブジェクトレプリカのストレージタイプは、デフォルトでソースバケットのオブジェクトのストレージタイプに追従します。

```
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:cn-south::sevenyousouthtest-7319456</Bucket>
            <StorageClass>Standard</StorageClass>
        </Destination>
	</Rule>
</ReplicationConfiguration>
```


## 存在する問題
お客様がTencent CloudでCloud Virtual Machine、Virtual Private Cloud、CDBなどのサービスを使用し、これらのサービスについてさまざまな人がクラウドアカウントのキーを共有しながら管理している場合、以下の問題が存在します：
- ご利用のキーは複数のユーザーによって共有されているため、漏えいのリスクが高くなります。
- 他のユーザーのアクセス権限を制限することはできませんので、誤操作によりセキュリティリスクが発生する可能性があります。

## 対処方法
この場合、サブアカウントを利用することにより、異なるサービスを異なる管理者に管理させることで、上記の問題を対処できます。デフォルトでは、サブアカウントにはCVMの権限またはCVM関連リソースを使用する権限ありません。従って、サブアカウントが必要なリソースまたは権限を使用できるようにするポリシーを作成する必要があります。

[CAM](https://intl.cloud.tencent.com/document/product/598/10583)（Cloud Access Management、CAM）は、Tencent Cloudが提供するWebサービスであり、主にユーザーがTencent Cloudアカウントのリソースへのアクセス権限を安全に管理するのに役立ちます。CAMを使用すると、ユーザー（グループ）を作成、管理、および廃棄でき、ID管理とポリシー管理を介して、Tencent Cloudリソースの使用が許可されるユーザーを指定し、制御できます。

CAMを使用する場合は、ポリシーを1人のユーザーまたは1組のユーザーグループと関連付けて、指定されたリソースを使用して指定されたタスクを完了することを許可または拒否できます。CAMポリシーのより詳細な基本情報については、[ポリシー構文](https://intl.cloud.tencent.com/document/product/598/10603)をご参照ください。

サブアカウントのCVM関連リソースへのアクセス許可を管理する必要がない場合は、このセクションをスキップできます。この部分をスキップし、ドキュメントの残りの内容の理解と利用には影響しません。

### クイックスタート
CAMポリシーは、1つ以上のCVM操作の実行を許可または拒否する必要があります。また、操作に利用できるリソース（すべてのリソースか、特定の操作の特定のリソース）を指定する必要もあります。ポリシーにはリソース操作に設定された条件も含めることができます。

>?
>- CAMポリシーを使用してCDBリソースを管理し、CDB操作を認証することをお勧めします。在庫量サブプロジェクト権限のユーザー体験は変わりませんが、サブプロジェクト権限を引き続き使用してリソースを管理し、操作を認証することはお勧めしません。
>- CDBは、現在、関連する有効化条件の設定をサポートしていません。

| タスク | リンク | 
|---------|---------|
|ポリシーの基本構造を理解する| [ポリシーの構文]（https://intl.cloud.tencent.com/document/product/236/14466）|
|ポリシーで操作を定義する| [CDBの操作](https://intl.cloud.tencent.com/document/product/236/14466) | 
|ポリシーでリソースを定義する| [CDBのリソースパス](https://intl.cloud.tencent.com/document/product/236/14466) |
|CDBがサポートするリソースレベルの権限|[CDBがサポートするリソースレベルの権限](https://intl.cloud.tencent.com/document/product/236/14467)|
|コンソール例|[コンソール例](https://intl.cloud.tencent.com/document/product/236/14468)|

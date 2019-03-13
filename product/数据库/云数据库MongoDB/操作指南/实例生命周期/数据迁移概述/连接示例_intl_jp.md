インスタンスが初期化された後、MongoDB shellまたは各言語ドライバーを介してデータベースにアクセスしてさまざまな管理操作を実行できます。CVMを使用して、プライベートネットワークを通してアクセスできます。現在、パブリックネットワークアクセス方式はサポートされていません。

## 詳細な説明
### クライアントのバージョン
TencentDB for MongoDBサービスに接続する最小ドライバーバージョンは3.2が必要です。最高の互換性を保証するために、shellスイート、java jarパッケージ、phpエクステンション、nodejsモジュールなどを含む**最新版**のクライアントドライバーを使用してください。詳細については、[MongoDBの公式Webサイトドライバーの紹介](https://docs.mongodb.com/ecosystem/drivers/)を参照してください。
### MongoDB shellの方式
mongo shellはMongoDBに付属しているインタラクションのJavaScript shellです。shellでコマンドラインを使用してMongoDBインスタンスとインタラクションできます。mongo shellを使用して、データを照合およびアップデートしたり、管理操作を実行したりできます。mongo shellはMongoDBディストリビューションの一部です。まずMongoDBをダウンロードまたはインストールして、その後はmongo shellを使用してMongoDBインスタンスに接続します。MongoDBディストリビューションのダウンロードアドレスについては、[接続](https://www.mongodb.com/download-center#community)をクリックしてください。具体的な接続手順は次のとおりです。
```
    cd <mongodb installation dir>
	./bin/mongo -umongouser -plxh2081* 172.16.0.56:27017/admin
```
> 上記の例で、-uパラメーターはユーザー名、-pパラメーターはパスワード、172.16.0.56と27017はそれぞれMongoDBインスタンスのIPとポートを指定します。

### URI方式
MongoDBサービスは伝統的なパラメーターの引き渡し方法で接続でき、同時に、ほとんどのドライバーは接続用のURI形式もサポートしています。MongoDBは、URIを使用してMongoDBサービスに接続することを正式に推奨しています。典型的なURIは次のとおりです。

例1
```
mongodb://username:password@IP:27017/admin
```
例2
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
例3
```
mongodb://username:password@IP:27017/somedb?authSource=admin&readPreference=secondaryPreferred
```

URIの各構成部分についての説明は以下の通りです。

| コンポーネント | 意味 | 必須かどうか |
|---------|---------|---------|
| mongodb:// | MognoDBプロトコルを表す特定の文字列 | 必須|
| username |MongoDBサービスログインに使用されるユーザー名 |必須、このページ「[デフォルトユーザー名](#.E9.BB.98.E8.AE.A4.E7.94.A8.E6.88.B7.E5.90.8D)」を参照してください|
| password | MongoDBサービスログインに使用されるユーザーパスワード |必須|
| IP:27017 | MongoDBサービスのIPとポート |必須|
| /admin | 認証するデータベースについて、TencentDB for MongoDBはadminに固定されています |必須、このページ「[認証データベース](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)」を参照してください|
| authMechanism=MONGODB-CR | 認証メカニズム |このページ「[認証メカニズム](#.E8.AE.A4.E8.AF.81.E6.9C.BA.E5.88.B6)」を参照してください|
| authSource=admin | 身元認証に使用されるデータベースについて、TencentDB for MongoDBはadminに固定されています |必須、このページ「[認証データベース](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)」を参照してください|
| readPreference=secondaryPreferred | スレーブデータベースから読み取る優先順位を設定できます |必須ではありません。このページ「[読み取り操作に対するマスタースレーブ優先順位](#.E8.AF.BB.E6.93.8D.E4.BD.9C.E7.9A.84.E4.B8.BB.E4.BB.8E.E4.BC.98.E5.85.88.E7.BA.A7)」を参照してください|
これは一部のMongoDBがURIに接続するパラメーターのリストです。詳細については、[MongoDBの公式Webサイトのドキュメント](https://docs.mongodb.com/manual/reference/connection-string/)を参照してください。

### デフォルトユーザー

TencentDB for MongoDBのリリースバージョンによって異なり、最新のインスタンスについて、「rwuser」と「mongouser」の2つのデフォルト内部構築ユーザーがあります。古いインスタンスはrwuserしかありません（このインスタンスをアップグレードするので、アップグレード前に連絡します）。ビジネスニーズを満たすために、TencentDB for MongoDBコンソールを使用してアカウントと権限を管理することもできます。

#### rwuser（MONGODB-CR認定）URIの例
**rwuserは、MONGODB-CR認証を使用している唯一のユーザーです**
```
mongodb://rwuser:password@10.66.100.186:27017/admin?authMechanism=MONGODB-CR
または
mongodb://rwuser:password@10.66.100.186:27017/somedb?authMechanism=MONGODB-CR&authSource=admin
```

#### mongouser（SCRAM-SHA-1認証）URIの例
**mongouserおよびクラウドコンソールで作成されたユーザーはSCRAM-SHA-1認証を使用します**
```
mongodb://mongouser:password@10.66.100.186:27017/admin
または
mongodb://mongouser:password@10.66.100.186:27017/somedb?authSource=admin
```

### 認証データベース
TencentDB for MongoDBはログイン認証用の認証データベースとして「admin」データベースを使用するため、認証データベースを指定するためにURIのポートの後に「**/admin**」を追加する必要があります。認証後、具体的なビジネスデータベースに切り替えて読み書き操作を実行します。URIの例：

```
mongodb://username:password@IP:27017/admin
```

もちろん、読み書きターゲットデータベースと追加の認証データベースパラメーター（authSource = admin）を直接指定することで、ターゲットデータベースに直接アクセスすることもできます。URIの例：

```
mongodb://username:password@IP:27017/somedb?authSource=admin
```

要約すると、adminを認証データベースとしてURIに代入する方法を選択する必要があります。

### 認証メカニズム
MongoDBはさまざまな認証メカニズムをサポートしており、公式の推奨は「SCRAM-SHA-1」です。
TencentDB for MongoDBは、「MONGODB-CR」および「SCRAM-SHA-1」2つの認証方法をサポートしています。
前述のように、TencentDB for MongoDBには「rwuser」と「mongouser」の2つのデフォルト内部構築ユーザーがあります。同時に、TencentDB for MongoDBコンソールで追加のユーザーを作成することもできます。このユーザーたちは2つのカテゴリに分けられ、それぞれ異なる認証メカニズムを採用します。分類は次のとおりです。

| ユーザー名 | 認証メカニズム | URI処理 |
|---------|---------|---------|
| rwuser | MONGODB-CR | パラメーター「authMechanism=MONGODB-CR」を追加する必要があります|
| Mongouserおよびクラウドコンソールで作成されたユーザー |SCRAM-SHA-1（推奨）|パラメーターを追加する必要はありません|

### 読み取り操作に対するマスタースレーブ優先順位
TencentDB for MongoDBは、レプリカセット全体にアクセスするためのCLB IPを提供します。スレーブデータベースから読み取るためのアクセスを指定する必要がある場合は、URIで「readPreference」パラメーターを設定してください。具体的な値の意味は以下のとおりです。

| 値 | 意味 | デフォルトかどうか|
|---------|---------|---------|
| primary |読み取り専用マスターノード | デフォルト方式|
| primaryPreferred |マスターノードが優先され、マスターノードが利用できない場合は、スレーブノードが読み取られます |　|
| secondary | 読み取り専用スレーブノード。スレーブノードが利用できない場合、エラーが報告されます|　|
| secondaryPreferred |  スレーブノードが優先され、スレーブノードが利用できない場合は、マスターノードが読み取られます|　|

スレーブノードから読み取る優先順位の設定、例によってURIをつなぎ合わせることができます。

```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

## 各言語の例

### Shell
[Shell接続の例](https://cloud.tencent.com/doc/product/240/Shell%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### PHP
[PHP接続の例](https://cloud.tencent.com/doc/product/240/PHP%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Node.js
[Node.js接続の例](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
 [mongooseの例](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B#node.js-mongoose-.E8.BF.9E.E6.8E.A5.E7.A4.BA.E4.BE.8B)
### Java
[Java接続の例](https://cloud.tencent.com/doc/product/240/Java%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Python
[Python接続の例](https://cloud.tencent.com/doc/product/240/Python%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### 再接続メカニズム
[再接続メカニズム](https://cloud.tencent.com/doc/product/240/4980)


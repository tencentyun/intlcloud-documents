## 基本概念

静的サイトとは静的コンテンツ（例えばHTML）またはクライアントシナリオのウェブサイトのことを指し、ユーザーはコンソールを通じてカスタマイズドメイン名をバインディングしたバケットに対し、静的サイトを構築できます。一方、動的サイトのコンテンツは、PHP、JSPまたはASP.NET等のサーバーのシナリオを含み、サーバーの処理に依存しています。Tencent Cloud COSは静的サイトのホスティングをサポートしますが、サーバーシナリオの作成をサポートしません。動的サイトを構成する場合、CVMサーバーのコードで構成してください。

## 例

ユーザーはexamplebucket-1250000000というバケットを作成し、下記ファイルをアップロードしました： 

```shell
index.html
404.html
403.html
test.html
docs/a.html
images/
```

### 静的サイト

**起動前**：下記デフォルトのアクセスドメイン名でバケットにアクセスし、ダウンロードのメッセージが表示され、`index.html`ファイルをローカルに保存できます。

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

**起動後**：下記アクセスノードでバケットにアクセスすれば、ブラウザにより`index.html`のページコンテンツを直接確認できます。

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

### HTTPSの強制

**起動前**：リクエスト元がHTTPである場合、ノードURLがHTTP未暗号化を保つ伝送プロトコルにアクセスします：

```shell
http://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

**起動後**：リクエスト元がHTTPまたはHTTPSを問わず、ノードが常にHTTPS暗号化を保つ伝送プロトコルにアクセスします：

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

### インデックスドキュメント

インデックスドキュメントは、静的サイトのホームページであり、ユーザーがウェブサイトのルートディレクトリまたは各サブディレクトリーにリクエストを出す時に返したウェブページです。通常、このページは`index.html`に命名されます。
ユーザーがバケットのアクセスドメイン名（例えば、`https://examplebucketbucket-1250000000.cos-website.ap-guangzhou.myqcloud.com`）により静的サイトにアクセスし、かつ特定ページをリクエストしていない場合、Webサーバーはホームページに戻ります。

ユーザーがバケットのルートディレクトリを含む各ディレクトリーにアクセスし、URLアドレスが`/`で終了する場合、優先的にこのディレクトリー下のインデックスドキュメントに自動的にマッチングします。ルートレベルURLの`/`は選択可能で、下記いずれのURLはインデックスドキュメントを返します。

```shell
http://www.examplebucket.com/
http://www.examplebucket.com
```

> !バケットにフォルダーを作成した場合、各フォルダーのレイヤーにインデックスドキュメントを追加する必要があります。

### エラードキュメント

エラードキュメントを構成する前、下記ページにアクセスする場合、404ステータスコードが返され、ページにはデフォルトのエラーページのメッセージが表示されます。

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

エラードキュメントを構成した後、下記ページにアクセスする場合、同様に404ステータスコードが返されますが、ページには指定のエラーページのメッセージが表示されます。

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

### リダイレクトのルール

#### エラーコードとリダイレクトの構成

webpage.htmlというドキュメントに**プライベート読み書き**のパブリックアクセス権限を設定した場合、ユーザーがこのドキュメントにアクセスする際、403エラーが返されます。
403エラーコードを構成し、403.htmlにリダイレクトした後：ブラウザは403.htmlのコンテンツを返します。
403.htmlドキュメントを構成していない場合、ブラウザはエラードキュメントまたはデフォルトのエラーメッセージを返します。
![](https://main.qcloudimg.com/raw/7dc917ba95af42438b6ab2c7604666d3.png)

#### プレフィックスマッチングの構成

1. フォルダーを`docs/`から`documents/`に再命名した後、ユーザーが`docs/`フォルダーにアクセスする場合、エラーが発生します。したがって、プレフィックス`docs/`のリクエストを` documents/`にリダイレクトできます。
![](https://main.qcloudimg.com/raw/e3b5c9004a67d020928bd0035b820715.png)
2. `images/`フォルダーを削除した場合（すなわち、プレフィックス`images/`付きのすべてのオブジェクトを削除した場合）、リダイレクトのルールを追加し、プレフィックス`images/`付きの任意のオブジェクトのリクエストを`test.html`ページにリダイレクトできます。
![](https://main.qcloudimg.com/raw/b6672acf43149267a837027911923f9b.png)

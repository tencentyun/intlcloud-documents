### COSBrowserツールとは何ですか。

COSBrowserはTencent Cloud Object Storage（COS）がリリースした視覚化インターフェースツールです。より簡単なインタラクションの使用を可能にし、COSリソースの確認、転送および管理を手軽に実現できます。現時点でCOSBrowserはデスクトップ端末（Windows、macOS、Linux）およびモバイル端末（Android、iOS）向けにご提供しています。詳細な説明については、[COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)をご参照ください。


### COSBrowserツールをダウンロードするにはどうすればよいですか。

ダウンロードアドレスおよび使用説明については、[COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)をご参照ください。

### CentOSのグラフィックインターフェースではダブルクリックしてもCOSBrowserのクライアントが起動しません。

端末で`./cosbrowser.AppImage --no-sandbox`コマンドを実行するとクライアントを起動することができます。


### サブアカウントでCOSBrowserにログインすると、ストレージパスが表示されないのはなぜですか。

1. サブアカウントにCOSアクセスに関する権限があるかどうか確認してください。関連ドキュメントは[サブアカウントのCOSアクセス権限の承認](https://intl.cloud.tencent.com/document/product/436/11714)をご参照ください。
2. サブアカウントに特定のバケットまたはバケット内の特定のディレクトリの権限のみが設定されている場合は、サブアカウントでCOSBrowserツールにログインする際、ストレージパスの追加とバケットの所在リージョンの選択を手動で行う必要があります。ストレージパスの形式はBucketまたはBucket/Object-prefixで、例えばexamplebucket-1250000000のようになります。
![](https://main.qcloudimg.com/raw/bf6b59f824af9413fbe83bb8968f926d.png)


### 大量のファイルがある場合に転送速度を上げるにはどうすればよいですか。

Windows版のCOSBrowserツールを例にとると、【高度な設定】に進み、【アップロード】、【ダウンロード】ファイルの同時実行数とパート数を調整することで転送速度を上げることができます。
![](https://main.qcloudimg.com/raw/d74eae3fb53dce13fee5c6b6e517e526.png)


### システムがmacOSですが、COSBrowserで「更新に失敗しました。権限が拒否されました」という表示がポップアップしました。どのように対処すればよいですか。
![](https://main.qcloudimg.com/raw/b07cd00819c3f27b05ac361ed561c52a.png)

**エラーの原因**
`/Users/username/Library/Caches/`ディレクトリに、`com.tencent.cosbrowser`および`com.tencent.cosbrowser.ShipIt`という2つのファイルがあります。これらのファイルの所有者がそれぞれrootユーザーとuserユーザーになっている場合、権限の問題によって更新に失敗したと考えられます。

**解決方法**
Mac端末で次のコマンドラインを実行します。
```plaintext
sudo chown $USER ~/Library/Caches/com.tencent.cosbrowser.ShipIt/
```

### エラー “no such file or directory, stat 'C:\Users\XXX\AppData\Local\Temp\cosbrowser\logs\cosbrowser.log'”がポップアップし、アプリケーションも使用できないのですが、どうすればよいですか。

![](https://main.qcloudimg.com/raw/42629a0686b7a892fef8946e547c9ef6.png)

**解決方法**：バージョン2.1.x以上のバージョンをダウンロードすることをお勧めします。

### cosbrowser.exeインストールパッケージの実行中にインストールが中止されましたが、どうすればよいですか。

**エラーの原因**
以前にCOSBrowserをインストールしたことがあり、システム内にこのアプリケーションが存在し、その後アプリケーションを手動で削除したがシステムトレースを消去していなかったため、再度インストールを実行した際にプログラムがトレースを発見し、実際にはアプリケーションが存在しないのにインストールを中止したことが原因です。

**対処方法**
COSBrowserアプリケーションのインストールトレースを手動で消去するか、またはクリーンアップツール（例えばTencent Securityのソフトウェア管理など）を使用してアンインストールと消去を行います。


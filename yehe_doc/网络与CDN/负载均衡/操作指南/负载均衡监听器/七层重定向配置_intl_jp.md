CLBはレイヤー7リダイレクトをサポートしています。この機能はユーザーのレイヤー7HTTP/HTTPSリスナー上でのリダイレクト設定をサポートします。
>?
>- セッション維持：クライアントが`example.com/bbs/test/123.html`にアクセスし、かつバックエンドCVMがセッション維持を有効にしている場合、リダイレクトを有効化すると、トラフィックを`example.com/bbs/test/456.html`にリダイレクトした際、元のセッション維持メカニズムは無効になります。
>- TCP/UDPリダイレクト：現在はIP + Portレベルのリダイレクトはサポートしていません。今後のバージョンで提供される予定です。
## リダイレクトの概要
- 自動リダイレクト
  - 概要
  すでに存在する`HTTPS:443`リスナーに、システムが自動的にHTTPリスナーを作成して転送を行います。デフォルトでは80番ポートを使用します。作成に成功すると、`HTTP:80`アドレスから`HTTPS:443`アドレスに自動的にリダイレクトしてアクセスすることができます。
  - ユースケース
 強制HTTPSリダイレクト、すなわちHTTPからHTTPSへの強制転送です。PC、スマホブラウザなどがHTTPリクエストによってWebサービスにアクセスしようとする場合、CLBはすべての`HTTP:80`リクエストを`HTTPS:443`にリダイレクトして転送を行います。
  - ソリューションの優位性
	 - 設定は一度のみ：1つのドメイン名、一度の設定で強制HTTPSリダイレクトが完了します。
	 - アップデートに便利：HTTPSサービスのURLに増減があった場合も、コンソールでこの機能を再度使用して更新するだけで済みます。
- 手動リダイレクト
 - 概要
1対1リダイレクトの設定が可能です。例えばあるCLBインスタンスで、`リスナー1/ドメイン名1/URL1`を`リスナー2/ドメイン名2/URL2`にリダイレクトするよう設定できます。
>?ドメイン名にすでに自動リダイレクトを設定したことがある場合は、手動リダイレクトを設定することはできません。
>
 - ユースケース
単一パスのリダイレクトです。例えばWeb業務を一時的にオフラインにする必要がある場合（ECでの完売、ページメンテナンス、更新・アップグレードなど）、従来のページを新しいページにリダイレクトする必要があります。リダイレクトを行わなければ、ユーザーのお気に入りや検索エンジンデータベース内の古いアドレスにアクセスすると`404/503`エラーページが表示されるだけになり、ユーザー体験を低下させ、アクセス数が無駄に失われることになります。

## 自動リダイレクト
Tencent Cloud CLBはワンクリックでのHTTPからHTTPSへの強制リダイレクトをサポートしています。
開発者がウェブサイト`https://www.example.com`を設定したいとします。開発者は、ユーザーがブラウザにURLを入力する際、それがHTTPリクエスト（`http://www.example.com`）かHTTPSリクエスト（`https://www.example.com`）のどちらであっても、HTTPSプロトコルによってセキュアにアクセスできるようにしたいと考えています。

### 前提条件
`HTTPS:443`リスナーが設定済みであること。

### 操作手順
1. [Tencent Cloud CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、CLBのHTTPSリスナーの設定を完了し、`https://example.com`のWeb環境を構築してください。詳細については、[HTTPSリスナーの設定](https://intl.cloud.tencent.com/document/product/214/32516)をご参照ください。
2. HTTPSリスナーの設定が完了すると、結果は下図のようになります。
![](https://main.qcloudimg.com/raw/6eaf2d1220d140bc37537f3388d78509.png)
3. CLBインスタンス詳細の「リダイレクト設定」タブで、**リダイレクト設定の新規作成**をクリックします。
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. **自動リダイレクトの設定**を選択し、設定済みのHTTPSリスナーおよびドメイン名を選択し、**次のステップ：パスの設定**をクリックします。
![](https://main.qcloudimg.com/raw/4481d9beac8fa51ee7f6c252c3714a41.png)
5. **送信**をクリックすると設定が完了します。
![](https://main.qcloudimg.com/raw/435e1389eadacc7bc90966480a29a131.png)
6. リダイレクト設定が完了すると、結果は下図のようになります。`HTTPS:443`リスナーに`HTTP:80`リスナーが自動的に設定され、なおかつHTTPのトラフィックがすべて自動的にHTTPSにリダイレクトされるようになっていることが確認できます。
![](https://main.qcloudimg.com/raw/c3249968deb68888fb591e59289194d9.png)

## 手動リダイレクト
Tencent Cloud CLBは1対1リダイレクトの設定をサポートしています。
例えば、業務でforsaleページを使用してキャンペーン運営を行い、現在のキャンペーンが終了すればキャンペーンページ`https://www.example.com/forsale`を新たなホームページ`https://www.new.com/index`にリダイレクトする必要がある場合などです。

### 前提条件
- HTTPSリスナーが設定済みであること。
- 転送ドメイン名`https://www.example.com/forsale`が設定済みであること。
- 転送ドメイン名およびパス`https://www.new.com/index`が設定済みであること。


### 操作手順
1. [Tencent Cloud CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、CLBのHTTPSリスナーの設定を完了し、`https://example.com`のWeb環境を構築してください。詳細については、[HTTPSリスナーの設定](https://intl.cloud.tencent.com/document/product/214/32516)をご参照ください。
2. HTTPSの設定が完了すると、結果は下図のようになります。
![](https://main.qcloudimg.com/raw/5c1fc217e1795a2f6a7b31c2a7ba3bfc.png)
3. CLBインスタンス詳細の「リダイレクト設定」タブで、**リダイレクト設定の新規作成**をクリックします。
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. **手動リダイレクトの設定**を選択し、元のアクセスのフロントエンドプロトコルポート`HTTPS:443`およびドメイン名`https://www.example.com/forsale`を選択し、リダイレクト後のフロントエンドプロトコルポート`HTTPS:443`およびドメイン名`https://www.new.com/index`を選択して、**次のステップ：パスの設定**をクリックします。
![](https://main.qcloudimg.com/raw/51106736b5ee61d6e87767652185d57a.png)
5. 元のアクセスパスに`/forsale`を、リダイレクト後のアクセスパスに`/index`をそれぞれ選択し、**送信**をクリックすると設定が完了します。
![](https://main.qcloudimg.com/raw/5f59b88ecc291d912b7faf2cf1d3770e.png)
6. リダイレクト設定が完了すると、結果は下図のようになります。`HTTPS:443`リスナーで、`https://www.example.com/forsale`が`https://www.new.com/index`にリダイレクトされるようになっていることが確認できます。
![](https://main.qcloudimg.com/raw/34364863bd44202df54e89ec3cb923f9.png)



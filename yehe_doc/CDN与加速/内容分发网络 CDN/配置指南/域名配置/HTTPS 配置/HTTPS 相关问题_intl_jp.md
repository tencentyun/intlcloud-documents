### HTTPSとは。
HTTPSとは、ハイパーテキスト転送プロトコル（Hypertext Transfer Protocol Secure）のことです。HTTPプロトコルに基づいて暗号化されたセキュリティプロトコルを転送し、データ転送のセキュリティを効果的に保証できます。HTTPSを設定する場合、ネットワーク全体でデータの暗号化転送機能を実現するために、ユーザーは、ドメイン名に対応する証明書を提供し、ネットワーク全体のCDNノードにデプロイする必要があります。

### CDNサービスはHTTPS設定をサポートしますか。
Tencent Cloud CDNは現在、HTTPS設定を完全にサポートしています。ユーザーは自分の証明書をアップロードしてデプロイするか、または[証明書管理コンソール](https://console.cloud.tencent.com/ssl )にアクセスして、TrustAsiaが無料で提供するサードパーティ証明書を申請することができます。

### HTTPS証明書はどう設定しますか。
CDNコンソールでHTTPS証明書を設定することができます。詳細については、[HTTPS設定](https://intl.cloud.tencent.com/document/product/228/35213)をご参照ください。

### CDNノードのHTTPS証明書は、オリジンサーバーのHTTPS証明書の更新と同期する必要がありますか。
ユーザーのback-to-origin方式によって決められます。
HTTP back-to-origin：同期する必要はありません。
HTTPS back-to-origin：オリジンサーバーの証明書が更新されると、CDNノードの証明書も同期的に更新される必要があります。クライアントとノード間の証明書は、ノードとオリジンサーバー間の証明書と同一である必要があります。そうでない場合、back-to-origin失敗を引き起こします。　

### ユーザーがHTTPSアクセスのみを許可し、HTTPアクセスを禁止する方法はありますか。
HTTPS 強制リダイレクト機能を使用できます。証明書が正常に設定されると、「HTTPSへの強制リダイレクト」スイッチが表示されます。有効にすると、ユーザーがHTTPリクエストを送信しても、HTTPSに強制的にリダイレクトしてアクセスします。
![](https://main.qcloudimg.com/raw/0352df67305e2e7f4c6df51b0b1afc09.png)


### CDNを設定した後、HTTPSにアクセスできないのはなぜですか。

次の手順に従って、ウェブサイトのHTTPS証明書をCDNにアップロードする必要があります。
1. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン名管理】をクリックして、ドメイン名管理画面に入ります。ドメイン名の右側にある【管理】ボタンをクリックして、管理画面に入ります。
![設定画面イメージ](https://main.qcloudimg.com/raw/9f5202ff57eb14f40dee3b15e4a37cdf.png)
2. 【高度な設定】をクリックして、HTTPS設定モジュールを見つけます。【設定へ】をクリックして証明書管理ページに移動し、証明書を設定します。設定手順の詳細については、[証明書管理](https://intl.cloud.tencent.com/document/product/228/35213#.E5.9F.9F.E5.90.8D.E9.85.8D.E7.BD.AE)をご参照ください。![設定画面イメージ](https://main.qcloudimg.com/raw/f8c4570d1a4847aab84c30ff0dc2e22d.png)
3.証明書が正常に設定されると、【HTTPSへの強制リダイレクト】スイッチが表示されます。有効にすると、ユーザーがHTTPリクエストを送信しても、強制的にHTTPSリクエストにリダイレクトしてアクセスします。
![設定画面イメージ](https://main.qcloudimg.com/raw/da5fb8ee7294231e27d65cd177dfd992.png)




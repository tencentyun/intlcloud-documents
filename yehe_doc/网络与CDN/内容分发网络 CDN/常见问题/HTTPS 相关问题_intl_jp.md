[](id:q1)
### HTTPSとは何ですか。
HTTPSとは、ハイパーテキスト転送セキュリティプロトコル（Hypertext Transfer Protocol Secure）である。HTTPプロトコルに基づいてデータを暗号化して安全性を確保するためのプロトコルです。HTTPSを設定する場合、ネットワーク全体でデータの暗号化転送機能を実現するために、ユーザーは、ドメイン名に対応する証明書を提供し、ネットワーク全体のCDNノードにデプロイする必要があります。  

[](id:q2)
### CDNサービスはHTTPS設定をサポートしますか。
Tencent Cloud CDNは現在、HTTPS設定を完全にサポートしています。ユーザーは自分の証明書をアップロードしてデプロイするか、または[証明書管理コンソール]（https://console.cloud.tencent.com/ssl）にアクセスしてTrustAsiaが無料で提供するサードパーティの証明書を申請することができます。

[](id:q3)
### HTTPS証明書を設定するにはどうすればよいですか。
[CDNコンソール](https://console.cloud.tencent.com/cdn)でHTTPS証明書を設定することができます。詳細については、[HTTPS設定](https://intl.cloud.tencent.com/document/product/228/35213)をご参照ください。

[](id:q4)
### オリジンサーバーのHTTPS証明書が更新されました。CDNに設定されている証明書は同時に更新する必要がありますか。
必要がありません。オリジンサーバーのHTTPS証明書を更新しても、CDNに設定されている証明書には影響しません。CDNに設定されている証明書の有効期限が近づいているか、​すでに切れている場合、HTTPS証明書を更新する必要があります。


[](id:q5)
### ユーザーがHTTPSアクセスのみを許可し、HTTPアクセスを禁止する方法はありますか。
[強制リダイレクト機能](https://intl.cloud.tencent.com/document/product/228/35214)を使用できます。HTTPS証明書を設定した後、「Http->Https機能」を有効にすることができます。有効にすると、ユーザーがHTTPリクエストを送信しても、HTTPSに強制的にリダイレクトしてアクセスします。　
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### CDNを設定したのに、HTTPSアクセスが機能しないのはなぜですか。

HTTPSアクセスを使用するには、以下の操作を行います。
1. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションウィンドウで【ドメイン名管理】を選択し、ドメイン名の右側にある【管理】をクリックして、その管理ページに入ります。
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2. 【HTTPS設定】をクリックし、HTTPS設定モジュールを見つけて、【設定に進む】をクリックして、証明書管理ページにジャンプし、証明書を設定します。設定手順については、[証明書の設定](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE)をご参照ください。
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
証明書が正しく設定されている​場合、HTTPSアクセスを有効にできます。




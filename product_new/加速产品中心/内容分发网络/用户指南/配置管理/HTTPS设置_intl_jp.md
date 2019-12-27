HTTPSとは、ハイパーテキスト転送セキュリティプロトコル（Hypertext Transfer Protocol Secure）を指します。HTTPプロトコルに基づいて暗号化されたセキュリティプロトコルを転送し、データ送信のセキュリティを効果的に保証できます。HTTPSを構成する場合、ネットワーク全体でデータの暗号化転送機能を実現するために、ユーザーは、ドメイン名に対応する証明書を提供し、ネットワーク全体のCDNノードにデプロイする必要があります。

>?
> - **Cloud Object Storage**または**万象YouTu**サービスにCDN加速がオンにされた後、デフォルトの「.file.myqcloud.com」の拡張子ドメイン名、または「.image.myqcloud.com」の拡張子ドメイン名は、証明書を構成する必要がなく、HTTPSリクエストを直接サポートすることができます。
>-Tencent Cloud CDNは現在、HTTP2.0プロトコルサポートに対して全面的に公開テストを行い、使用を直接にスタートすることができます。

## 構成ガイド
Tencent Cloud CDNは現在、2つの方法で証明書をデプロイすることをサポートしています。
-ユーザー保有の証明書：ユーザー保有の証明書、プライベートキーの内容をCDNにアップロードしてデプロイします。全プロセスで暗号化されて転送され、証明書が着地しないため、ユーザーの証明書のセキュリティを確保します。
-Tencent Cloudホスティングの証明書：[SSL Certificates Management](https://console.cloud.tencent.com/ssl)で複数のクラウド製品に使用されるように、既存の証明書をTencent Cloudにホスティングしてもいいし、このプラットフォームでアジア誠信により無料で提供されるサードパーティの証明書を申請してCDNに直接デプロイしてもいいです。


1. [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のディレクトリの【ドメイン名管理】をクリックすると、管理ページが表示されます。リストから編集するドメイン名の行を特定して操作バーの【管理】をクリックします。
![img](https://mc.qcloudimg.com/static/img/f92d2ef7e4be2b69185ab43228f025ef/1.png)
2. 【高度な構成】をクリックし、** HTTPS構成**モジュールを特定します。【構成へ】をクリックすると、**証明書管理**ページが表示されます。証明書を構成します。構成フローについては、[証明書管理](https://intl.cloud.tencent.com/document/product/228/6303)を参照してください。
![img](https://mc.qcloudimg.com/static/img/df38d5d35b266e96c99f4ab67732cfd8/2.png)
3.証明書が**構成が成功した**後、【強制的なHTTPSリダイレクト】スイッチが表示されます。デフォルトでは、強制的なHTTPSリダイレクトはオフ状態になっています。
![img](https://mc.qcloudimg.com/static/img/22b01df16d9b4d50397b612b60252cfa/3.png)
4. 【強制的なHTTPSリダイレクト】をオンにすると、ユーザーがHTTPリクエストをスタートしても、HTTPSリクエストに強制的にリダイレクトしてアクセスします。デフォルトでは、リダイレクトモードは302です。
【編集】をクリックしてリダイレクトモードを変更することができます。

## HTTP2.0構成

ドメイン名にHTTPS証明書を構成が成功した後、HTTP 2.0をオンにすることができます。
![img](https://mc.qcloudimg.com/static/img/72d122326ad99bb23f1ba66690bae91c/4.png)
更にHTTP2.0関連の特徴を理解するには、HTTP2.0の新しい特徴を参照してください。

> ? 「.myqcloud.com」拡張子加速ドメイン名はまだHttp2.0をサポートしていません。

## OCSPステープリング構成
**機能説明**
OCSPステープリング（OCSP Stapling、TLS証明書状態クエリー拡張）。OCSP Staplingサーバーは、クライアント自身がCAにリクエストを送信する代わりに、TLSハンドシェイク時に、検証のためにキャッシュされたOCSPクエリー結果をクライアントに送信します。OCSPステープリングにより、TLSハンドシェイク効率が大幅に向上し、ユーザーの認証時間が節約されます。

ドメイン名にHTTPS証明書を構成が成功した後、OCSPステープリングをオンにすることができます。


## HTTPSオリジンプルがサポートするのアルゴリズム

現在、HTTPSオリジンプルがサポートしているアルゴリズムは次の通りです（優先順位問わず）。

| ECDHE-RSA-AES256-SHA   | ECDHE-RSA-AES256-SHA384   | ECDHE-RSA-AES256-GCM-SHA384   |
| ---------------------- | ------------------------- | ----------------------------- |
| ECDHE-ECDSA-AES256-SHA | ECDHE-ECDSA-AES256-SHA384 | ECDHE-ECDSA-AES256-GCM-SHA384 |
| SRP-AES-256-CBC-SHA    | SRP-RSA-AES-256-CBC-SHA   | SRP-DSS-AES-256-CBC-SHA       |
| DH-RSA-AES256-SHA      | DH-RSA-AES256-SHA256      | DH-RSA-AES256-GCM-SHA384      |
| DH-DSS-AES256-SHA      | DH-DSS-AES256-SHA256      | DH-DSS-AES256-GCM-SHA384      |
| DHE-RSA-AES256-SHA     | DHE-RSA-AES256-SHA256     | DHE-RSA-AES256-GCM-SHA384     |
| DHE-DSS-AES256-SHA     | DHE-DSS-AES256-SHA256     | DHE-DSS-AES256-GCM-SHA384     |
| CAMELLIA256-SHA        | DH-RSA-CAMELLIA256-SHA    | DHE-RSA-CAMELLIA256-SHA       |
| PSK-3DES-EDE-CBC-SHA   | DH-DSS-CAMELLIA256-SHA    | DHE-DSS-CAMELLIA256-SHA       |
| ECDH-RSA-AES256-SHA    | ECDH-RSA-AES256-SHA384    | ECDH-RSA-AES256-GCM-SHA384    |
| ECDH-ECDSA-AES256-SHA  | ECDH-ECDSA-AES256-SHA384  | ECDH-ECDSA-AES256-GCM-SHA384  |
| AES256-SHA             | AES256-SHA256             | AES256-GCM-SHA384             |
| ECDHE-RSA-AES128-SHA   | ECDHE-RSA-AES128-SHA256   | ECDHE-RSA-AES128-GCM-SHA256   |
| ECDHE-RSA-AES128-SHA   | ECDHE-RSA-AES128-SHA256   | ECDHE-RSA-AES128-GCM-SHA256   |
| SRP-AES-128-CBC-SHA    | SRP-RSA-AES-128-CBC-SHA   | SRP-DSS-AES-128-CBC-SHA       |
| DH-RSA-AES128-SHA      | DH-RSA-AES128-SHA256      | DH-RSA-AES128-GCM-SHA256      |
| DH-DSS-AES128-SHA      | DH-DSS-AES128-SHA256      | DH-DSS-AES128-GCM-SHA256      |
| DHE-RSA-AES128-SHA     | DHE-RSA-AES128-SHA256     | DHE-RSA-AES128-GCM-SHA256     |
| DHE-DSS-AES128-SHA     | DHE-DSS-AES128-SHA256     | DHE-DSS-AES128-GCM-SHA256     |
| ECDH-RSA-AES128-SHA    | ECDH-RSA-AES128-SHA256    | ECDH-RSA-AES128-GCM-SHA256    |
| ECDH-ECDSA-AES128-SHA  | ECDH-ECDSA-AES128-SHA256  | ECDH-ECDSA-AES128-GCM-SHA256  |
| CAMELLIA128-SHA        | DH-RSA-CAMELLIA128-SHA    | DHE-RSA-CAMELLIA128-SHA       |
| PSK-RC4-SHA            | DH-DSS-CAMELLIA128-SHA    | DHE-DSS-CAMELLIA128-SHA       |
| AES128-SHA             | AES128-SHA256             | AES128-GCM-SHA256             |
| SEED-SHA               | DH-RSA-SEED-SHA           | DH-DSS-SEED-SHA               |
| DES-CBC3-SHA           | DHE-RSA-SEED-SHA          | DHE-DSS-SEED-SHA              |
| IDEA-CBC-SHA           | PSK-AES256-CBC-SHA        | PSK-AES128-CBC-SHA            |
| EDH-RSA-DES-CBC3-SHA   | ECDH-RSA-DES-CBC3-SHA     | ECDHE-RSA-DES-CBC3-SHA        |
| EDH-DSS-DES-CBC3-SHA   | ECDH-ECDSA-DES-CBC3-SHA   | ECDHE-ECDSA-DES-CBC3-SHA      |
| RC4-SHA                | ECDH-RSA-RC4-SHA          | ECDHE-RSA-RC4-SHA             |
| RC4-MD5                | ECDH-ECDSA-RC4-SHA        | ECDHE-ECDSA-RC4-SHA           |
| SRP-3DES-EDE-CBC-SHA   | SRP-RSA-3DES-EDE-CBC-SHA  | SRP-DSS-3DES-EDE-CBC-SHA      |
| DH-DSS-DES-CBC3-SHA    | DH-RSA-DES-CBC3-SHA       | -                             |

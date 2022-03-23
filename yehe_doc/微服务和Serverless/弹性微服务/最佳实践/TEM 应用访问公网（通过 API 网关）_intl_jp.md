
## 概要

TEMで実行されているアプリケーションは、通常、業務上のニーズなどに起因して、パブリックネットワークにアクセスする必要があります。一方、多くのシーンでは、これらのリクエストはすべてHTTP/HTTPSリクエストです。API Gatewayを使用して、パブリックネットワークにアクセスするHTTP/HTTPSリクエストを手軽に簡単に設定することができます。
>?パブリックネットワークへのアクセスのニーズにHTTP/HTTPS以外のものも含まれる場合は、[TEMアプリケーションのパブリックネットワークへのアクセス](https://intl.cloud.tencent.com/zh/document/product/1094/41888)を参照し、NAT Gatewayの設定によって行ってください。

##  前提条件

[環境の作成](https://intl.cloud.tencent.com/document/product/1094/40358)および[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/document/product/1094/40362)を先に完了させてください。

## 操作手順

### ステップ1：API GatewayでパブリックネットワークのHTTP/HTTPSリクエストをバインドする

1. [API Gatewayコンソール](https://console.cloud.tencent.com/apigateway)に進み、左側ナビゲーションバーで**サービス**をクリックし、サービスリストページに進みます。
2. TEMアプリケーションのデプロイリージョンと同一のリージョンを選択し、ページ左上隅の**新規作成**をクリックし、サービスを新規作成します。
    サービスを新規作成する際、フロントエンドのタイプはHTTP、HTTPS、HTTPとHTTPSのいずれかから選択することができます。アクセスモードはVPCプライベートネットワークを選択し、インスタンスのタイプは共有型を選択します。
    <img src = "https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png" style="width: 100%"> 
3. API GatewayサービスIDをクリックし、API管理ページに進みます。**APIの新規作成**をクリックします。
4. フロントエンド設定でAPI名を入力し、フロントエンドのタイプはHTTP&amp;HTTPS、パスは「/」、リクエスト方法はANYを選択してすべてのリクエストが含まれるようにします。 認証のタイプは「認証なし」を選択し、**次のステップ**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. バックエンド設定で、パブリックネットワークのURL/IPを選択し、アクセスしたいパブリックドメイン名およびパスを設定し（ここではTencent Cloud公式サイトを例とします）、**次のステップ**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/b695295cda52de71705b973c2de5a6ab.png)
6. アプリケーションのリターンタイプを設定します。ここではHTMLとし、RESTfulサービスはJSONを選択できます。クリックすると完了し、サービスをリリースします。

### ステップ2：パブリックリクエストの接続性の検証

1. API Gatewayサービスの基本設定ページに進み、サービスのプライベートネットワークVPCアクセスアドレスをコピーします。
![](https://qcloudimg.tencent-cloud.cn/raw/c7132945c851609b3c559295a9968925.png)
2. デプロイしたTEMアプリケーションのページを開き、アプリケーションインスタンスのwebshellに進み、API GatewayのプライベートネットワークVPCアクセスアドレスにアクセスしてネットワークの接続性を検証します。
![](https://qcloudimg.tencent-cloud.cn/raw/8bd3f68e322495c0416c68cdbccecf23.png)

## API Gatewayの紹介

Tencent Cloud API Gateway（API Gateway）はTencent CloudがリリースしたAPIホスティングサービスであり、作成、メンテナンス、リリース、実行、オフラインなどを含むAPIのライフサイクル全体の管理を提供することができます。詳細については[API Gateway公式サイトドキュメント](https://intl.cloud.tencent.com/zh/document/product/628)をご参照ください。

## 概要

ここでは主に、Tencent Cloud API Gatewayをすぐに使用してTEMアプリケーションにアクセスし、TEMアプリケーションのAPIを管理する方法についてご紹介します。API GatewayとTEMを組み合わせて使用することで、TEMのユーザーはAPI Gatewayの持つトラフィック制限、認証、キャッシュなどの高度な機能を利用し、業務の成功に役立てることができます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/81b3172279330bad5a9a7d57b7c4c2c7.png" width="650px">

##  前提条件

[TEMコンソール](https://console.cloud.tencent.com/tem)にログインし、まず[環境の作成](https://intl.cloud.tencent.com/document/product/1094/40358)および[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/document/product/1094/40362)を先に完了させてください。

## 操作手順

### ステップ1：TEMアプリケーションのためのVPCプライベートネットワークアクセス設定

1. [TEMコンソール](https://console.cloud.tencent.com/tem)にログインし、左側のナビゲーションバーで**アプリケーション管理**をクリックし、設定したいアプリケーションをクリックしてアプリケーション詳細ページに進みます。
2. 設定バーの**編集と更新**をクリックし、アプリケーションアクセス設定ページに進みます。
3. VPCプライベートネットワークアクセス（第4層に転送）を選択し、サブネット、プロトコル、コンテナポートおよびアプリケーション監視ポートを選択し、**サブミット**をクリックします。このとき、TEMは第4層に転送するVPCプライベートネットワークアプリケーションタイプのCLBを自動的に作成します。



### ステップ2：API Gatewayサービスの作成とTEMアプリケーションのバインド[](id:step2)

1. [API Gatewayコンソール](https://console.cloud.tencent.com/apigateway/service)にログインして、左側ナビゲーションバーで**サービス**をクリックし、サービスリストページに進みます。
2. TEMアプリケーションのデプロイリージョンと同一のリージョンを選択し、ページ左上隅の**新規作成**をクリックし、サービスを新規作成します。
   サービスを新規作成する際、フロントエンドのタイプはHTTP、HTTPS、HTTPとHTTPSのいずれかから選択することができます。アクセスモードはVPCプライベートネットワークおよびパブリックネットワークを選択できます。インスタンスのタイプは共有型、専用型を選択します。
	 <img src="https://qcloudimg.tencent-cloud.cn/raw/5f95e38cc91b5a4854c2048a93a7fe06.png">
3. API GatewayサービスIDをクリックし、API管理ページに進みます。**APIの新規作成**をクリックします。
4. フロントエンド設定でAPI名を入力し、フロントエンドのタイプはHTTP&HTTPS、パスは「/」、リクエスト方法はANYを選択してすべてのリクエストが含まれるようにします。 認証のタイプは「認証なし」を選択し、**次のステップ**をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/a945e3e3bd7d60383c47be24b7d884a5.png)
5. バックエンド設定で、VPC内リソースを選択し、TEMアプリケーションのデプロイ環境にあるVPCを選択します。バックエンドドメイン名を設定し、TEMアプリケーションによって自動作成されたCLB（名前は「cls-xxxdefault{TEMアプリケーション名}」）を選択し、対応するリスナー（前の手順で設定したポートのマッピング）を選択します。バックエンドアドレスを「/」と入力し、APIの作成を完了します。
   ![](https://qcloudimg.tencent-cloud.cn/raw/37a8a5b7bc18613de223419c978b7f8e.png)
	このうち、バックエンドドメイン名の設定は次のとおりです。
    <img src="C:\オーダー処理ドキュメント\TEM_2021-12-31_10-56-59\API Gatewayを使用してTEMアプリケーションにクイックアクセス_intl_zh\f1d8b0d080aab985df46ec9a224b8e07.png" width="500px">
6. これで、設定したAPIを確認できるようになり、API Gatewayの提供するデフォルトのドメイン名によってTEMアプリケーションにアクセスすることもできるようになります。


### ステップ3：API Gatewayを介したTEMアプリケーションへのアクセス

[ステップ2](#step2)で作成したAPI GatewayのAPIにアクセスすると、API Gatewayを介してTEMアプリケーションにアクセスすることができます。
   ![](https://main.qcloudimg.com/raw/70ca90f3a189c79f09f0c8e334507b22.png)

## 注意事項

- アプリケーションのAPI Gatewayへの侵入なしアクセスを保証するため、1つのAPI Gatewayサービスには1つのTEMアプリケーションのみバインドすることをお勧めします。フロントエンドアドレスとバックエンドアドレスは一致させ、どちらも「/」とすることですべてのAPIをブロックできます。サービスの中でアプリケーションの特定のAPIについて単独での設定を行うこともできます。
- [API Gatewayプラグイン使用ドキュメント](https://intl.cloud.tencent.com/zh/document/product/628/40214)を参照して、バックエンドにTEMのAPI Gateway APIバインドプラグインを接続することで、API Gatewayの持つ高度な機能を利用することができます。

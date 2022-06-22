本文では、Tencent Kubernetes Engine（TKE）についてわかりやすく説明します。ユーザーがこのガイドに従ってTKEを簡単に開始することができます。

## 1.テンセントクバネティスエンジンとは？


[テンセントクバネティスエンジン](https://intl.cloud.tencent.com/document/product/457/6759)（TKE）とは、ネイティブのKubernetesをベースに提供された、コンテナを中心として高い拡張性と性能を有するコンテナ管理サービスです。ホストされているCVMインスタンスクラスターで、アプリケーションを手軽に実行することができます。また、ユーザーが自由に選べるよう、Tencent Cloudは、[耐障害性コンテナサービス](https://intl.cloud.tencent.com/document/product/457/34040)（Elastic Kubernetes Service、EKS）と[エンジコンテナサービス]Tencent Kubernetes Engine for Edge（TKE）(https://intl.cloud.tencent.com/document/product/457/35390)（Tencent Kubernetes Engine for Edge、TKE）も提供しています。


テンセントクバネティスエンジンでは、[TKEコンソール](https://console.cloud.tencent.com/tke2/overview)、[Kubectl](https://intl.cloud.tencent.com/document/product/457/30639)によりクラスターとサービスを操作できます。




## 2.TKE料金について
TKEは当面、サービス料金がかかりません。ユーザーが実際に使用したクラウドリソースに応じて課金されます。TKEを使用しているときに関連製品で発生するリソース料金については、[課金概要](https://intl.cloud.tencent.com/document/product/457/6770)をご参照ください。




## 3.TKEの使用
#### 3.1登録および認証
テンセントクバネティスエンジンを使用する前には、[Tencent Cloudアカウント](https://intl.cloud.tencent.com/register)の登録を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了する必要があります。

#### 3.2 ロール権限授与
他のクラウドサービスリソースに正常にアクセスするには、現在のサービスロールに権限を授与してください。
Tencent Cloudコンソールで**クラウド製品**>**TKE**を選択し、[TKEコンソール](https://console.cloud.tencent.com/tke2/cluster?rid=1)に移動し、画面の提示に従って、TKE認証を行います。クラスターの作成を開始するには、サービス認証を完了して関連するリソースの操作権限を取得します。



####　3.3クラスターの作成
多種類のクラスターを使用するには、[耐障害性クラスターの作成](https://intl.cloud.tencent.com/document/product/457/34048)および[エッジクラスターの作成](https://intl.cloud.tencent.com/document/product/457/35385)ドキュメントをご参照ください。


####　3.4　ワークロードのデプロイ
TKEは、イメージデプロイおよびYAMLファイルオーケストレーションの両方の方法でワークロードをデプロイできます。
- イメージテンプレートを使用してステートレスロード（Deployment）をデプロイする場合は、[簡易Nginxサービスの作成](https://intl.cloud.tencent.com/document/product/457/7851)または[単一インスタンス版WordPressの作成](https://intl.cloud.tencent.com/document/product/457/7205)をご参照ください。
- カスタムイメージを使用してワークロードをデプロイする場合は、[Hello Worldサービスの手動構築](https://intl.cloud.tencent.com/document/product/457/7204)をご参照ください。




####　3.5クラスターの運用保守
コンテナサービスTKEは、クラスター、アプリケーション、ストレージ、ネットワークなどのモジュールの管理プラットフォームとして機能します。詳細な情報や実践的な作業が必要な場合は、以下を参照してさらに理解するうえで使用してください。

| 機能 | 参考ドキュメント |
|---------|---------|
| KubernetesコマンドラインツールKubectlを使用して、ローカルクライアントマシンからTKEクラスターに接続します。 | [クラスターを接続](https://intl.cloud.tencent.com/document/product/457/30639) |
| 実行中のKubernetesクラスターをアップグレードします。 | [クラスターのアップグレード](https://intl.cloud.tencent.com/document/product/457/30640) |
| 作成したKubernetesクラスターにインスタンスを追加します。 | [新規ノード](https://intl.cloud.tencent.com/document/product/457/30652) |
| Kubernetesクラスター内ノードを管理します。| [ノードプールの作成](https://intl.cloud.tencent.com/document/product/457/35901) |
| コンソールからのネイティブKubernetesオブジェクトを直接操作します。| [Kubernetesオブジェクト管理](https://intl.cloud.tencent.com/document/product/457/30658) |
| Service方式を使用してコンテナ群のために固定アクセスポータルを提供します。 | [Serviceの基本機能](https://intl.cloud.tencent.com/document/product/457/36833) |
| Ingressリソースを通じて異なる転送ルールを設定します。 | [Ingress管理](https://intl.cloud.tencent.com/document/product/457/37013) |
| コンテナサービスを使用したストレージ能力 | [ストレージ管理の概要](https://intl.cloud.tencent.com/document/product/457/37769) |
| クラスター内のコンテナのためにコンテナネットワークアドレス範囲内のIPアドレスを割り当てます。 | [コンテナネットワークの概要](https://intl.cloud.tencent.com/document/product/457/38966) |
| Kubernetesクラスター内のサービスログの保存と分析を実行します。 | [ログ収集](https://intl.cloud.tencent.com/document/product/457/32419) |
| コンテナイメージサービス内でホストされているプライベートイメージを使用してアプリケーションをデプロイします。 | [TCRエンタープライズ版のコンテナイメージを使用してワークロードを作成します。](https://intl.cloud.tencent.com/document/product/457/36838) |



















##　4.入門必読	

- ** 基本ネットワークで TKEを使用できますか？**
いいえ、TKEは現時点では プライベートネットワークのみをサポートしています。

- **既存のCVMをクラスターに追加できますか？**
はい、クラスターを作成した後、既存のCVMを追加できます。詳細については、[既存ノードの追加](https://intl.cloud.tencent.com/document/product/457/30652#.E6.B7.BB.E5.8A.A0.E5.B7.B2.E6.9C.89.E8.8A.82.E7.82.B9)をご参照ください。

- ** どうして、サービスはずっと起動中ですか？**
サービスのコンテナは動作し続けているプロセスがない場合は、サービスがずっと起動中の状態になります。サービスの起動に関する詳しい問題は、[イベントに関するよくある質問](https://intl.cloud.tencent.com/document/product/457/8187)をご参照ください。

- **クラスターを作成する前にネットワークを計画する方法は？**
クラスターを作成する際には、クラスターネットワークとコンテナネットワークのセグメントを重複させることはできません。通常、プライベートネットワークVPCのサブネットを選択して、クラスターのノードネットワークに使用することできます。詳細については、[コンテナネットワークとクラスターネットワークの説明](https://intl.cloud.tencent.com/document/product/457/38966)をご参照ください。

- **作成したサービスにアクセスするにはどうすればいいですか？**
アクセス方法によって、さまざまなアクセスポータルが提供されます。詳細については、[サービスアクセス方式](https://intl.cloud.tencent.com/document/product/457/36832)をご参照ください。

- **  コンテナはパブリックネットワークにどうアクセスするんですか？**
コンテナは存在するノードにブリックネットワークIP帯域幅がある場合、コンテナはパブリックネットワークに直接アクセスできます、コンテナは存在するノードにブリックネットワークIP帯域幅がいない場合、パブリックネットワークにアクセスするにはNATゲートウェイを使ってください。

- **イメージ作成はできません。コンテナサービスTKEを使用できますか？**
TKEが統合したHelm 3.0関連機能により、helm chart、コンテナイメージ、ソフトウェアサービスなどのさまざまな製品やサービスを作成することができます。作成したアプリケーションは、指定したクラスタで実行され、適切な機能が提供されます。詳細については[アプリケーション管理](https://intl.cloud.tencent.com/document/product/457/30683)をご参照ください。

- ** 私の業務に必要なテキストと環境変数が多いですが、管理はどうすればいいですか？**
コンフィグレーションファイルは、[設定項目](https://intl.cloud.tencent.com/document/product/457/30675)を使用して管理できます。

- ** 異なるサービス間で互いにアクセスしたいはどうすればいいですか？**
クラスターにおける同じNamespaceサービスは直接アクセスことができます。異なるNamespaceサービスは、互いにアクセスするために、<service-name>.<namespace-name>.svc.cluster.localの形式でアクセスしてください。

## 5.フィードバックと提案	

テンセントクバネティスエンジン製品およびサービスを使用する上で何らかの質問や助言がある場合は、以下の方法でフィードバックしてください。後ほど専門スタッフがお客様のお問い合わせに回答いたします：
- 製品のドキュメントの間違い等を発見した場合（リンク先、内容、API エラーなど）は、ドキュメントのページ右側の【ドキュメントに関するフィードバック】をクリックするか、または問題が存在するコンテンツを選択してフィードバックしてください。
- 製品に関連する問題が発生した場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してサポートを依頼してください。


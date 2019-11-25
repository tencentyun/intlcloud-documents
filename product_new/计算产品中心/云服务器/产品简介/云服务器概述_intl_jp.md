Cloud Virtual Machine（CVM）はTencent Cloudが提供する拡張可能なコンピューティングサービスです。 CVMを使用することで、従来型サーバーを使用する場合のリソース量の見積もることと先行投資が必要なくなり、短時間で任意数のCVMを迅速的に起動し、リアルタイムにアプリケーションをデプロイできます。
Tencent Cloud CVMを使用すると、CPU、メモリ、ディスク、ネットワーク、セキュリティなどはすべてユーザーがカスタマイズでき、要件の変化に応じて手軽に調整できます。

## 関連概念

CVMをご使用される前に、以下の概念を理解していただく必要があります。
- **インスタンス**：CPU、オペレーティングシステム、ネットワーク、ディスクなどの最も基本的なコンピューティングコンポーネントを含むクラウド上の仮想コンピューティングリソース。
- **インスタンス種類**：Tencent Cloudが提供するCVMの各種CPU、メモリ、ストレージ、およびネットワーク
- 。詳細については、[インスタンス仕様](http://intl.cloud.tencent.com/document/product/213/11518)を参照してください。
- **イメージ**：事前に構成されたオペレーティングシステムやプリインストールされたソフトウェアなど、CVMが動作するためのテンプレートです。 Tencent Cloud CVMは、WindowsやLinuxなどのさまざまな構成済みイメージを提供します。
- **ローカルディスク**：インスタンスと同じ物理サーバー上にある、インスタンスが永続ストレージとして使用できるデバイスです。
- **Cloud Block Storage**：インスタンスのシステムディスクまたは拡張可能なデータディスクとして使用できる分散式永続ブロックストレージデバイスを提供します。
- **Virtual Private Cloud**：Tencent Cloudが提供する仮想的な隔離ネットワークキャパシティーで、他のリソースと論理的に隔離されています。
- **IPアドレス**：Tencent Cloudは[プライベートIPアドレス](http://intl.cloud.tencent.com/document/product/213/5225)と[パブリックIP](http://intl.cloud.tencent.com/document/product/213/5224)を提供します。簡単に説明すると、プライベートIPアドレスはローカルエリアネットワーク（LAN）サービスを提供し、CVM間で相互にアクセスできます。パブリックIPアドレスは、ユーザーがCVMインスタンス上でインターネットサービスにアクセスする必要がある場合に使用されます。
- **Elastic IP**：ダイナミックネットワーク向けに設計された静的パブリックIPアドレスで、迅速なトラブルシューティングの要件に応えられます。
- **セキュリティグループ**：セキュリティグループは、状態検出とパケットフィルタリング機能を備えた仮想ファイアウォールとして捉えることができます。1台または複数台のCVMのネットワークアクセス制御に使用されて、ネットワークセキュリティ隔離の重要な手段です。
- **ログイン方法**：セキュリティの高い[SSHキーペア](http://intl.cloud.tencent.com/document/product/213/6092)と通常のパスワードの[ログインパスワード](http://intl.cloud.tencent.com/document/product/213/6093)。
- **リージョンとアベイラビリティーゾーン**：インスタンスおよびその他のリソースが配置された物理的な場所です。
- **Tencent Cloudコンソール **：Webベースのユーザーインターフェースです。


##CVMの使用方法 

Tencent Cloudは、以下のCVM構成方法と管理方法を提供します。

- **コンソール**：Tencent Cloudが提供しているCVMを構成・管理するためのWebベースのサービスインターフェースです。
- **API**：Tencent Cloudは、CVMを管理するためのAPIインターフェースも提供しています。 APIの説明については、[API概要](https://intl.cloud.tencent.com/document/product/213/15688)を参照してください。
- **SDK**：[SDK](https://intl.cloud.tencent.com/document/product/494) またはTencent Cloud [コマンドライン CLI](https://intl.cloud.tencent.com/document/product/1013/30220) ツールを使用してCVM APIを呼び出すことができます。



## CVMをすばやく購入して構築する

初めてCVMを購入した個人ユーザーの場合、Tencent Cloudは、提供されているクイックスタート構成案を利用することをお勧めします。詳細については、以下を参照してください。
- [Windows CVMクイックスタート](http://intl.cloud.tencent.com/document/product/213/2764)
- [Linux CVMクイックスタート](http://intl.cloud.tencent.com/document/product/213/2936)

ストレージメディア、容量、ネットワーク帯域幅、セキュリティグループ設定のカスタマイズ構成など、CVM構成に対してより高い構成要件がある場合に、以下を参照してください。
- [Windows CVMのカスタマイズ構成](http://intl.cloud.tencent.com/document/product/213/10516)
- [ Linux CVMのカスタマイズ構成](http://intl.cloud.tencent.com/document/product/213/10517)

## CVMの料金

CVMの料金については、[CVM Pricing（Linux）](https://intl.cloud.tencent.com/document/product/213/30011)を参照してください。

##　その他の関連製品

- Auto Scalingタイミングを使用するか、条件に基づいてサーバークラスターの数を自動的に増減できます。詳細については、[Flexible Flex Product Documentation](https://intl.cloud.tencent.com/document/product/377)を参照してください。
- Cloud Load Balancerを使用して、クライアントからリクエストトラフィックを複数のCVMインスタンスに自動的に割り当てることができます。詳細については、[Cloud Load Balancer製品ドキュメント](https://intl.cloud.tencent.com/document/product/214)を参照してください。
- Tencent Kubernetes Engineを利用して、CVMグループのアプリケーションライフサイクルを管理できます。詳細については、[Tencent Kubernetes Engine製品ドキュメント](https://intl.cloud.tencent.com/document/product/457)を参照してください。
- クラウド監視サービスを使用して、CVMインスタンスとそのシステムディスクを監視できます。詳細については、[クラウド監視製品ドキュメント](https://intl.cloud.tencent.com/document/product/248)を参照してください。
- CVM上でリレーショナルデータベースをデプロイするか、Tencent Cloudのクラウドデータベースを使用することができます。詳細については、[MySQL](https://intl.cloud.tencent.com/document/product/236)を参照してください。




### 全体アーキテクチャ
この節では、Tencent Kubernetes Engineシステムの設計および実装を紹介します。製品のアーキテクチャを次の図に示します：
![](https://main.qcloudimg.com/raw/8ecde8fe39d8f4cc65b9622823ab1058.png)

### アーキテクチャ説明
1.  Tencent Kubernetes EngineはネイティブKubernetesをベースに適応と追加を行い、ネイティブKubernetesの能力をサポートしています。
2.  Tencent CloudのKubernetesプラグインを提供し、ユーザーがTencent Cloud上でKubernetesクラスタを素早く構築するよう支援します。
3.  Tencent Kubernetes EngineはKubernetesの上位層で、クラスター管理、アプリケーション管理、CI/CDなどの進歩的な能力を提供しています。



### モジュールの説明
1. **コンテナサービスコンソールおよびクラウドAPI**：ユーザーがコンソール、Kubectl、またはAPIを使用してクラスタとサービスを操作します。
2. **イメージサービスCCRモジュール**：Tencent Cloudが提供するイメージサービスモジュールで、ユーザーはイメージをアップロードしたり、ローカルにダウンロードしたりすることができます。
3. **コンテナサービスTKEモジュール**：クラスタの増減・変更・検索、サービスの増減・変更・検索などを含む、コンテナサービスコアモジュール。



## ご購入時の注意事項



>? ご購入時の注意事項に従わないためにサービスが利用できない場合、対応するサービス利用不可時間は、サービス利用不可時間として計上されません。詳しくは、[TKEサービスレベル利用規約](https://intl.cloud.tencent.com/zh/document/product/457/12356?lang=zh&pg=#4.-release-of-liabilities)。

クラスターをご購入時に、クラスターパネルコンポネントの高負荷によるクラスター利用不可を回避するために、以下の推奨スペックを参考にして、業務に応じて適切なクラスター構成を選択してください。
例えば、1つのクラスターに50ノードをデプロイするが、Podを2000もデプロイする場合、最大管理ノードが50ではなく、100のクラスター構成を選択すべきです。

注意：PodにはNamespace配下のすべての状態のPodが含まれ、システムコンポーネント関連のPod（cni-agentなど）が含まれません。

| 最大管理ノード数 | 最大Pod数（推奨） | 最大ConfigMap数（推奨） | 最大CRD 数（推奨） |
| ---------------- | ------------------- | ------------------------- | ------------------- |
| 5                | 150                 | 32                        | 150                 |
| 20               | 600                 | 64                        | 600                 |
| 50               | 1500                | 128                       | 1250                |
| 100              | 3000                | 256                       | 2500                |
| 200              | 6000                | 512                       | 5000                |
| 500              | 15000               | 1024                      | 10000               |
| 1000             | 30000               | 2048                      | 20000               |
| 3000             | 90000               | 4096                      | 50000               |
| 5000             | 150000              | 6144                      | 100000              |


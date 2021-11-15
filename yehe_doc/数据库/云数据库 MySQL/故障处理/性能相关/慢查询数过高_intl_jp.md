## 現象の説明
スロークエリ現象が発生すると、通常、CPU使用率やスロークエリーの数など、複数の監視指標が同時に跳ね上がります。


## 考えられる原因
通常、SQLステートメントの実行効率はあまり高くないため、TencentDB for MySQLに大量のリクエストが蓄積されます。よくある原因は、以下の2つです。
- [](id:yy1)原因1：SQLステートメントがインデックスを使用していないか、またはより良いインデックスを使用していない。
- [](id:yy2)原因2：QPSのプレッシャーが、現在のインスタンスの負荷上限を超えている。

## ソリューション
考えられる2つの原因に対しては、さまざまな解決方法があります。
- ソリューション1：SQLステートメントを最適化して、SQLステートメントの実行効率を引き上げます。詳しくは[対策1](#cs1)をご参照ください。
- ソリューション2：TencentDB for MySQLの設定を引き上げます。詳しくは[対策2](#cs2)をご参照ください。

## 処理手順
### [対策1：SQLステートメントの最適化](id:cs1)
TencentDB for DBbrainを直接使用して、スロークエリを最適化することができます。DBbrainはSQLステートメントを分析し、インデックスを追加するための提案を行います。
1. [DBbrainコンソール](https://console.cloud.tencent.com/dbbrain/performance/analysis)にログインし、左側のナビゲーションで【Performance Optimization】を選択し、上部にあるデータベースを選択し、【 Slow SQL Analysis】タブを選択します。
2. 「SQL統計」チャートのスロークエリー（棒グラフ）をクリック（単一の時間帯を選択）またはプル（複数の時間帯を選択）します。下に集約されたSQLテンプレートと実行情報（実行数、合計実行時間、スキャンされた行数、返された行数などを含む）が以下に表示されます。
![](https://main.qcloudimg.com/raw/0659dcb5dfb47bf00c4df2646946f0ce.png)
3. 集約されたSQLテンプレート行をクリックすると、SQLの具体的な分析および統計データが右側にポップアップ表示され、対応するインデックスの提案を確認することができます。
![](https://main.qcloudimg.com/raw/f72dcf38d05fc7381007502e930f3014.png)

### [対策2：TencentDB for MySQLの設定の引き上げ](id:cs2)
各仕様に対応する[QPS公式負荷テストデータ](https://intl.cloud.tencent.com/document/product/236/8842)を確認し、現在のインスタンスのQPSデータと比較して、対応する[MySQL CPUとメモリ仕様](https://intl.cloud.tencent.com/document/product/236/19707)を調整します。
